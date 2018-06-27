---
title: "Architecture Design"
date: 2018-06-23T01:15:21-07:00
draft: false
---

The demo will be implemented using the original [Shazam algorithm](http://www.ee.columbia.edu/~dpwe/papers/Wang03-shazam.pdf). There are two parts to the application.

1. Generating a database of fingerprints for known songs
2. Identifying an unknown audio sample

The fingerprint generation and matching process can be seen in the following diagram. In this post I will give a high level overview of this architecture. I will follow this up with another post on the implementation details and results.

![architecture diagram](https://imgur.com/ciYRJ1L.png)

## Fingerprint Creation

Audio fingerprints will be created for each known song and stored in the database with a reference back to the song they originated from. When an unknown audio sample is to be identified, a fingerprint will be created and compared to the existing fingerprints in the database. The song belonging to the best matched fingerprint will be assumed to be where the audio sample came from.


### Spectrogram

First, a spectrogram of the audio is created using the short-time fourier transform (STFT). This creates a time-frequency graph that stores the amplitude of each frequency at each point in time. An example of a spectrogram from the Shazam paper can be seen in the following image,

![spectrogram](https://imgur.com/lFoagoc.png)

The y axis represents frequency and the x axis represents time. The darkness represents the amplitude of a specific frequency at a specific point in time. The amplitude is commonly represent by different colours.

### Find Peaks

Second, the spectrogram is analyzed and the peaks are selected. A time-frequency point is considered a peak if it has a higher energy content than all of its neighbours. In the Shazam paper the output of this process is a "constellation map".

Selecting high energy points helps make this algorithm robust to noise, as most of the noise will simply be discarded.

The following figure shows an example of a constellation map.

![constellation map](https://imgur.com/3HDtZ1p.png)

### Find Pairs

Each peak point is used as an "anchor" and neighbouring points in front of it are selected to create a pair. The exact distance from the anchor point can be configured to change the accuracy of the implementation. A larger distance will be more accurate as it will create more pairs. However, it could also require a significant more amount of storage. A trade off needs to be made.

In the Shazam paper this process is called combinatorial hash generation.

![combinatorial hash generation](https://imgur.com/BgjLh3O.png)

### Create Hash

Finally, the a hash is created for each pair. It should be noted that this is not a cryptographic hashing function as it does not follow the necessary properties. Each hash is composed of

- the frequency of point 1
- the frequency of point 2
- the difference in their times

This hash is combined with the time offset of the first point, as it will be necessary for matching, to create a fingerprint.

```
fingerprint = hash:time = [f1, f2, t2 - t1]:t1
```

![hash details](https://imgur.com/6veatsK.png)

### Database

The fingerprints generated for each song need to be stored in a database for fast and easy access later. Since a single song can have thousands of fingerprints, the number of songs I plan to save and amount of storage available should be carefully considered.

I will simply store each song and fingerprint in the PostgreSQL database. There will be a one-to-many relationship between fingerprints and songs.

For each song, I would like to store as much information as possible. I plan on reading metadata from MP3 files to access the title, artist, and album in order to provide a better user experience when a successful match is found.

For each fingerprint, it is crucial to only store the necessary information. This is the hash, time of the first point, and song id. Millions of fingerprints can easily be generated so making this table as small as possible will benefit me in the long run.


## Identification

When an unknown audio sample needs to be identified, its fingerprints will first be generated, and then database will be queried for matching fingerprints. A naive approach would be to simply selected the song which most of the matching fingerprints originated from. However, we can make the assumption that the time between successive fingerprints in both the unknown and known sample are the same.

For example, consider a beat in a song. Each hit of the drum will be a time-frequency peak and therefore generate a fingerprint. The entire beat will generate several fingerprints, each peak occurring on a drum hit at a specific time. In an unknown audio sample with the same beat, the time between time-frequency peaks will be the same. We can subtract the fingerprint time offsets (which we specifically saved during fingerprint generation) of the fingerprint from the database to the sample fingerprint to calculate the difference. Successive matching fingerprints will all have the same difference. Therefore, we can calculate these differences in the matched fingerprints and select the song linked to from the fingerprints with the most matching differences.

This is illustrated in the following figure. A diagonal is present as matched fingerprints occur successively after each other. The time offset for these fingerprints is the same, indicating a match.

![fingerprint matching](https://imgur.com/v17RoSQ.png)

## Application

The above steps will be combined into a simple Python application. Looking up a song will consist of recording audio from my laptops microphone and attempting to identify the source song. During testing I will introduce noise into the identification process to see how robust my implementation is. I will also try with several different microphones, to see how the microphone qualify affects accuracy.


