---
title: "Proposal"
date: 2018-05-23T12:57:38-07:00
draft: false
---

# Project Topic

An acoustic fingerprint is a very small summary of an audio signal. They are commonly created from songs and can be used to identify which song a short audio sample originated from. For my project I will investigate various acoustic fingerprinting techniques and implement a small program demonstrating how audio fingerprinting works.

Successfully audio fingerprinting implementations face many technological challenges. Matching only a few seconds of audio to a large database of songs requires storing the fingerprints as efficiently as possible. It is simply not feasible to brute force compare the audio samples to every song in the database. Clever algorithms exist to convert the audio into a small and space friendly format, that still allows for comparison and identification.

# Initial Survey

Several applications already exist that allow a user to identify a song using only their smartphones microphones. Most notable are the [Soundhound](https://soundhound.com/) and [Shazam](https://www.shazam.com/) applications. These services can accurately identify the song playing in a noisy bar or coffee shop with only a few seconds of audio. A few algorithms exist to convert a segment of audio into a fingerprint. Throughout my project I will be investigating and comparing them. The general idea these algorithms follow is after some initial preprocessing of the audio, key features in the time and frequency domain are hashed and stored in a database. When an audio sample needs to be identified, the hash of its key points are compared to the ones in the database.

# Expected Deliverables

### Week 1

History of audio fingerprinting and initial investigation into existing algorithms.

### Week 2

Selection of algorithm which will be implemented. Design of program architecture.

### Week 3

Start the implementation of the demo. Finalize details of algorithm.

### Week 4

Final demo of audio fingerprinting program.
