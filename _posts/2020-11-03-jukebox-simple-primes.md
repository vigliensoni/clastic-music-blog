---
layout: post
current: post
cover:  assets/images/bees.jpg
navigation: True
title: Simple primes using Jukebox
date: 2020-11-03 2:23:00
tags: [Jukebox]
class: post-template
subclass: 'post'
author: gabriel
---

I've been playing around with OpenAI's Jukebox to do neural synthesis. Their model can generate 44.1KHz monophonic audio of any given length. 
The Jukebox model can be sampled with different approaches: 

- `ancestral` sampling
- `primed` or *continuation*
- `upsample`
- `continue`




Since the output of Jukebox is so complex, I've been testing it the output using very simple primes:

- a 3-secs 440Hz sine wave
- a 3-secs white noise
- a 140 BPM 2-bar click track
<iframe src="https://archive.org/details/simple-audio-utilities-mono/01-440-sine-3s-mono.wav#" width="500" height="140" frameborder="0" webkitallowfullscreen="true" mozallowfullscreen="true" allowfullscreen></iframe>

I tried the same network configuration for all the tests (just changed the prompt length accordingly):

```bash
python jukebox/jukebox/sample-01-primed.py \
--model=5b \
--name=sample-01-primed-rhythm \
--levels=3 \
--sample_length_in_seconds=60 \
--total_sample_length_in_seconds=180 \
--sr=44100 \
--n_samples=8 \
--hop_fraction=0.5,0.5,0.125 \
--mode=primed \
--audio_file=jukebox/8-AUDIO-PRIMES/03-click-track-140bpm-3-428s-mono.wav \
--prompt_length_in_seconds=3.428
```

Here are some of the resulting output the network has generated. 

### Priming on sine wave

The network sometimes try to stay in zones with stable characteristics, similar to the prime (e.g., `item 0`, `item 2`). Sound snippets are quiet, calm, or slow in general (e.g., `item 4`, `item 5`)

My favorite ones are `item 2` and `item 6`. It's really beautiful how the former primer morphs into the feedback and then it goes to some “underwater” moments at the end.

**Starting with a stable, continuous tone leads to audios with these characteristics**



<iframe src="https://archive.org/details/jukebox-primed-on-sine-wave#" width="500" height="250" frameborder="1" webkitallowfullscreen="true" mozallowfullscreen="true" allowfullscreen></iframe>


### Priming on white noise

Beware: this is a bit loud!

<iframe src="https://archive.org/details/jukebox-primed-on-white-noise#" width="500" height="375" frameborder="0" webkitallowfullscreen="true" mozallowfullscreen="true" allowfullscreen></iframe>

Results actually morph from white noise or go from white noise to something very noisy (e.g., `item 0`, `item 1`, `item 5`). Or not, you can get portions of pseudo-songs with stylistic similarities to the chosen artist (e.g., `item 3`, `item 7`). It is also common going from full noise to silence (e.g., `item 4`, `item 5`), I guess because of evolutions in the time-frequency domain. 

My favorite one: `item 6`

In general, the results stay interestingly in the *noise* or *silence* zone. But **once they are in the silent zone, they go to an actual song and not back to silence.**





### Priming on a click track

The beginning of the re-synthesized click is truncated a bit. Perhaps a short padding lead would be useful.

<iframe src="https://archive.org/details/jukebox-primed-on-click-track#" width="500" height="250" frameborder="0" webkitallowfullscreen="true" mozallowfullscreen="true" allowfullscreen></iframe>

The tempo is sometimes dictated by the metronome and remains constant (e.g., `item 0`, `item 3`, `item 4`), other times it is not (e.g., `item 1`, `item 6`). The network sometimes extends the click track (e.g., `item 3`, `item 4`)

There's some kind of vocoder-ish sound in all the examples.

My favorite one: `item 7`

**Having a rhythmic primer leads, in general, to rhythmic patterns**

### General thoughts about using the `5b` model

Listening to lyrics in this kind of *scat singing* (more likely *gibberish*, *jibber-jabber*, or *gobbledygook*) is how I first experienced and enjoyed music in English. All emotion came through the actual music and performance, there was no meaning to the words.