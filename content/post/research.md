---
title: "Research"
date: 2018-06-12T23:23:51-07:00
draft: false
---

I have looked at multiple academic papers describing various acoustic fingerprinting algorithms, which include

-   [A review of audio fingerprinting](http://www.music.mcgill.ca/~ich/classes/mumt621_09/fingerprinting/cano05review.pdf)
-   [Computer Vision for Music Identification](https://ieeexplore.ieee.org/document/1467322/)
-   [Waveprint: Efficient wavelet-based audio fingerprinting](https://www-sciencedirect-com.ezproxy.library.uvic.ca/science/article/pii/S0031320308001702)
-   [A Review of algorithms for audio fingerprinting](https://ieeexplore-ieee-org.ezproxy.library.uvic.ca/stamp/stamp.jsp?tp=&arnumber=1203274)
-   [Survey and evaluation of audio fingerprinting schemes for mobile query-by-example applications](http://www.cs.toronto.edu/~dross/ChandrasekharSharifiRoss_ISMIR2011.pdf)
-   [Landmark-based music recognition system optimisation using genetic algorithms](https://link-springer-com.ezproxy.library.uvic.ca/article/10.1007%252Fs11042-015-2963-0)
-   [An Industrial Strength Audio Search Algorithm](http://www.ee.columbia.edu/~dpwe/papers/Wang03-shazam.pdf)
-   [Robust audio fingerprinting using peak-pair-based hash of non-repeating foreground audio in a real environment](https://link-springer-com.ezproxy.library.uvic.ca/article/10.1007%252Fs10586-015-0523-z)

There are several different methods used to generate and compare fingerprints. All of the methods analyze the frequency-time spectrum of the original audio sample and querying audio sample.

The initial methods to generate audio fingerprints were based on computer vision techniques. They treated the frequency-time spectrum as an image and applied machine learning and computer vision algorithms to generate and computer fingerprints. I found these methods to be very interesting, but they are not used very much today. An innovative audio fingerprinting algorithm was developed for the Shazam application in 2003. A. Wang created fingerprints using pairs of frequency peaks in the spectrum. Thousands of fingerprints could be created for a song and were stored in an inverted index. This method has been the basis for most new implementations today.

I have decided to attempt and implement the original Shazam algorithm in my demo. I aim to create a database of fingerprints for a set of songs. I will then capture audio from my microphone and identify which song the audio comes from. As my demo will be used in a production environment, performance is not the top priority. Therefore, I will be using the Python language as it has a wealth of audio processing, signal processing, and graphing libraries (scipy, numpy, and matplotlib).

A lot of innovation between fingerprinting techniques comes from reducing the effect of noise and distortion in the signal before and during the fingerprint extraction. As these algorithms are often used in a noisy environment, such as a bar or coffee shop, any accuracy improvement in the identification go a long way. The demo I am going to create will be deployed in a controlled environment with minimal additional noise. For this reason I will focus on implementing the raw fingerprinting and matching algorithm as accurately as possible and will not focus as much on implementing noise and distortion reduction.
