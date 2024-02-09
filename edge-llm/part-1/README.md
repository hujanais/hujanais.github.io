[Home](https://hujanais.github.io/edge-llm/)
# Part 1.  Demonstrate speech-to-text on a Raspberry Pi on device

## Overview
Our goal is to enable robust speech to text on a Raspberry Pi performed locally on the edge device with no internet connectivity.  There are many options available for this task but eventually after poking around the internet, I settle on using OpenAI's Whisper and ggreganov's open source project to compile the weights into a C++ standalone package.

## Installation Procedure
Installation procedure on a Raspberry Pi-4 or Pi-5.  I am using a headless version of the Bookworm OS with ssh access to keep the OS footprint as low as possible.
```
sudo apt update  
sudo apt upgrade
sudo apt install git
git clone https://github.com/ggreganov/whisper.cpp
sudo apt install libsdl2-dev # we need this to fix the sdl.h missing error

cd whisper.cpp
make -j stream
# this will download the ggml model.  
# For the initial test, I chose the smallest possible model, tiny.en
./models/download-ggml-model.sh tiny.en

# for RPi-5, let's try small.en
make small.en

# build
make
# run against tiny.en
./main -m models/ggml-tiny.en.bin -f samples/jfk.wav
# run against small.en
./main -m models/ggml-small.en.bin -f samples/jfk.wav
```
## Test Result
The test is on a pre-saved .wav file that is 11 secs long
| Device | Elapsed Time | Model
|--|--|--|--|
|Raspberry-Pi4 2GB  | **24022.11 ms** | tiny.en
|Raspberry-Pi5 4GB	| **3432.53 ms**	| tiny.en
|Raspberry-Pi5 4GB | **9638.72 ms** | small.en

## Add microphone and record your own audio
I am just using a basic usb microphone and most are compatible with the Pi.
```
# check to see if your microphone is found
arecord -l
**** List of CAPTURE Hardware Devices ****
card 0: Device [USB PnP Sound Device], device 0: USB Audio [USB Audio]
Subdevices: 1/1
Subdevice #0: subdevice #0

# Whisper requires the following format.
# S16_LE : PCM signed 16-bit little-endian
# 16000 sampling rate
# wav file 
# plughw takes the card# and subdevice#
arecord -D plughw:0,0 -c 1 -r 16000 -f S16_LE --duration=30 samples/test.wav

# run the test on the created file
./main -m models/ggml-tiny.en.bin -f samples/test.wav
```
## Model Accuracy
### Testing my own voice and with the glory of my Malaysian accent.
1. Test result using tiny.en. **[errors highlighted in bold]**
Take the match and strike it against your shoe.
Better hash is made of rare beef.
A cloud of dust stung his tender eyes.
Stop and stare at the **hot** working man.
The child almost hurt the small dog.
A streak of color ran down the left edge.
He wheeled the **bite** past the winding road.
Slash the gold cloth into fine ribbons.
**Retried** to replace the coin but failed.
A rich farm is rare.

2. Test result using small.en
take the match and strike it against your shoe
better hash is made of rare beef
a cloud of dust stung his tender eyes
stop and stare at the hard-working man
the child almost hurt the small dog
a streak of color ran down the left edge
he wheeled the bike past the winding road
slash the gold cloth into fine ribbons
we tried to replace the coin but failed
a rich farm is rare

### Observation
There were 3 errors in the transcription using the tiny.en model and the words, 
| actual word | transcribed word |
| -- |-- |
| hard | hot |
| bike | bite |
| We tried | Retried |

This is actually a funny result because we Malaysians/Singaporeans have difficulty pronoucing R's, K's and T's and it showed on the tiny.en model.  However, the small.en model was able to transcribe with 100% accuracy.  Very impressive indeed.  The 4GB Pi can definitely load the larger models but I didn't test further.

## Time for what we really want to try.  Transcribe live audio
```
./stream -m ./models/ggml-tiny.en.bin --step 4000 --length 8000 -c 0 -t 4 -ac 512
- or -
./stream -m ./models/ggml-small.en.bin --step 4000 --length 8000 -c 0 -t 4 -ac 512
```

## Pro-tip
```
htop

# continuously measure temperature once every 5 seconds
watch  -n  5 vcgencmd measure_temp
```

> Written with [StackEdit](https://stackedit.io/).