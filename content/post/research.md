---
title: "Research"
date: 2018-06-10T23:23:51-07:00
draft: true
---

I have looked at multiple academic papers describing various acoustic fingerprinting algorithms, which include

-   [A review of audio fingerprinting](http://www.music.mcgill.ca/~ich/classes/mumt621_09/fingerprinting/cano05review.pdf)
-   [Robust audio fingerprinting using peak-pair-based hash of non-repeating foreground audio in a real environment](https://link-springer-com.ezproxy.library.uvic.ca/article/10.1007%252Fs10586-015-0523-z)
-   [Waveprint: Efficient wavelet-based audio fingerprinting](https://www-sciencedirect-com.ezproxy.library.uvic.ca/science/article/pii/S0031320308001702)
-   [A Review of algorithms for audio fingerprinting](https://ieeexplore-ieee-org.ezproxy.library.uvic.ca/stamp/stamp.jsp?tp=&arnumber=1203274)
-   [Landmark-based music recognition system optimisation using genetic algorithms](https://link-springer-com.ezproxy.library.uvic.ca/article/10.1007%252Fs11042-015-2963-0)

The method used to create the fingerprint is generally the same between algorithms. Pairs of peaks extracted from the frequency-time spectrum are hashed and stored in a database associated with that specific song or audio signal. When a short audio signal needs to be matched to its original song, its fingerprint is created and compared to the fingerprints in the database. The most probable match is used to identify the audio sample.

The innovation between fingerprinting techniques comes from reducing the effect of noise and distortion in the signal before and during the fingerprint extraction. As these algorithms are often used in a noisy environment, such as a bar or coffee shop, any accuracy improvement in the identification go a long way. The demo I am going to create will be deployed in a controlled environment with minimal additional noise. For this reason I will focus on implementing the raw fingerprinting and matching algorithm as accurately as possible and will not focus as much on implementing noise and distortion reduction.
