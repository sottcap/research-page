---
layout: post
title:  "Raspberry Pi IP Camera Project"
date:   2019-06-04 10:18:00
categories: Raspberry Pi
---

Waiting for my son to be born, I was quite serious about what's gonna be the best gift I can give him.
I am not handy enough to make some toys.
I have no artistic insights and skillsets to draw picture or compose music or whatever classy art products for him.

All things related with my proficiency are physics, computers and biology.
So, I decided to make something useful for him and his mom using my knowledge and experties: **IP Camera**.

Yes, you may buy IP cameras at very cheap price (~$25) from Amazon.com with advanced technology and features such as motion detection, recording, alarm, playing musics, etc.
I believe they are working well and mechanically and electronically very reliable.

But, the real thing bothering me was security issues.
Privacy is important for everyone and IP camera can be potentially dangerous doors causing security breaches.
I do not want for our family's lives to be at stake.
I do not want to rely on others products that are possibly harmful for us.
As such, I launched the project to build IP camera from scratch.

I collected the requirements of the camera from my wife. The list is as follows.

**Requirements**

1. Day/Night Vision
2. Sound from a camera to a receiver.
3. Cozy look
4. Under $100
5. Standard protocols for communications.

Her original requirements were 1-3 but I added 4-5 for the system design.

### Materials ###

First, we need a computer: cheap (<$50) but powerful (video encoding support) one.
Maybe, I could choose other types of mini-computer but Raspberry Pi (RPi) fit well to my requirement.
It costs $35 even for the most expensive one (RPi 3B+) and at least I believe it supports H.264.
It is also very popular so that it is easy to find peripherals in the market.
Thus, RPi 3B+ was my choice for the computer part.
However, I believe the cheaper version (3A or 2A/B or even zero) might also work depending on overloads.

![Raspberry Pi 3B+](https://www.raspberrypi.org/app/uploads/2018/03/770A5614-2.jpg){:height="50%" width="50%" .center-image} 
<!-- <img src=https://www.raspberrypi.org/app/uploads/2018/03/770A5614-2.jpg width=50% /> -->

Then, I check out Day and Night cameras.
Not many choices for the Day and Night cameras in the market.
Some of them are more expensive and have better features such as higher resolutions and focus.
But, those were not suitable for me because of budgets. Focusing might be useless for this type of IP camera.
The cheapest one was $23 [\[amazon-link\]](https://www.amazon.com/Raspberry-Vision-Camera-Quimat-Embedded/dp/B06XTP23LH/ref=sr_1_8?keywords=day+and+night+camera+raspberry+pi+3B%2B+fisheye&qid=1559701881&s=gateway&sr=8-8).

We need a case as well for cozy and good appreance.
A numerous cases are on sale now.
It was not easy choice but I bought LEGO-compatible case because it can be more useful in future.
Only bad thing is that the camera case enclosed isn't fit to Day/Night cameras.
But, I couldn't find any RPi case compatible with the Day/Night camera.
It might be 3D printable but it's too much for me.

![Lego case](https://i.ebayimg.com/images/g/TAwAAOSwP69al96-/s-l1600.jpg){:height="50%" width="50%"}

Next one is a microphone. Unfortunately, RPi doesn't come with audio jack for microphone. Instead, it has four USB ports.
Hence, the ideal choice would be USB microphones.
The cheapest mini USB microphone was ~$6.
Actually, I regreted my decision later because this small microphone brought a lot of work on software side.
By the way, I managed to get it working.

![Microphone](https://cdn-shop.adafruit.com/970x728/3367-00.jpg){:height="50%" width="50%"}

Then, we need camera mount to fix the camera at baby's crib.
The LEGO case has a camera mount compatible with Go-Pro and there are many Go-Pro compatible flexible mounts.
I chose one that is not very expensive but has a more sturdy clamp.

In addition, we need micro SD card and USB power to build up the RPi system.
Fortunately, my extra 32GB micro SD and phone chargers were perfect fits.

### Software ###

#### OS ####
**Raspbian** was recommended by RPi foundation.
I didn't care much about the functionality and performance of OS.
So, I used the latest Raspbian for my project.

#### Streaming Framework ####
**GStreamer** had been widely used in Linux community. 
However, I think the documentation and the community support for GStreamer are mess.
It has many issues with even installations.
And for some reasons, the latest Linux releases deploy only out-dated-versions those contain non-compatible plugins.
It was quite frustrating because it was very hard to find solutions for this simple problems.
In the end, I gave up installing GStreamer binaries from Rasbian. Instead, I downloaded the latest source tar balls (1.16) from official sites [\[link\]](https://gstreamer.freedesktop.org).
At least, base, good and bad plugins including gstreamer itself are necessary. Also, gst-rtsp-library support should be installed.
If some plugins does not appear, then check config.log and any library is missing and clear cache on home directory (~/.gst)

#### Protocols and Codecs ####
My goal is to implement all IP camera features in standard protocols because it makes easier for other client programs to access the camera (for example, VLC).
The natural choice was RTSP/RTP.

H.264 seems to be implemented in kernel or hardware stack so H.264 was chosen for videos.

For audio, I chose different codecs such as raw-audio S16LE, mp3, vorbis but only S16LE worked.
Vorbis codec was hard to plug-in to Gstreamer framework for some reason and mp3 encoding was not very smooth so that the audio was choppy.
Also, sampling rate should be fixed at 48KHz for unknown reasons and it should be clarified later.

ALSA is necessay to adjust the volume of the mic. Add softvolume section to ~/.asoundrc to increase the volume. Otherwise, it is too quiet.

~~~~
pcm.mic_hw {
    type hw
    card Device
    channels 1
    format S16_LE
    rate 44100
}
pcm.mic_sv {
    type softvol
    slave.pcm mic_hw
    control {
        name "Boost Capture Volume"
        card Device
    }
    min_dB -3.0
    max_dB 50.0
}
~~~~

#### RTSP Server ####
There are many examples in examples folder.
I took test-launch for the project with pipeline:

~~~~
rpicamsrc preview=false bitrate=2000000 keyframe-interval=60 vflip=false \ 
! video/x-h264, framerate=30/1, width=640, height=480 ! h264parse ! rtph264pay name=pay0 pt=96 ! \
alsasrc device="mic_sv" ! audio/x-raw,rate=44100,channels=1,width=16 ! volume volume=10.0 \
! queue ! audioconvert ! rtpL16pay name=pay1 pt=98
~~~~

To address my wife's complaints about noisy audio, I purchased a better microphone (Maono's). 
It costs $15.99.
After try-and-errors, I found that it only supports stereo instead of mono so I slightly modified .asound and the launch-script as follows.

~~~~
pcm.mic_hw {
    type hw
    card Elf
    channels 2
    format S16_LE
    rate 44100
}
~~~~

~~~~
rpicamsrc preview=false bitrate=2000000 keyframe-interval=60 vflip=false \ 
! video/x-h264, framerate=30/1, width=640, height=480 ! h264parse ! rtph264pay name=pay0 pt=96 ! \
alsasrc device="mic_hw" ! audio/x-raw,rate=44100,channels=2,width=16 ! volume volume=10.0 \
! queue ! audioconvert ! rtpL16pay name=pay1 pt=98
~~~~

The launch script is located at /usr/local/bin/rtsp-server-start.sh
And the service starting at boot was enabled by rc.local with sudo.
So, ~root/.asoundrc was updated properly for the service.

### Hardware Assembly ###

The hardware assembly was trivial. Only thing was that there is no elegance way to attach camera on the case.
Scotch taping looks ugly but works fairly well.

