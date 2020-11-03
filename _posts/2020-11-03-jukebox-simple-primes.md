---
layout: post
current: post
cover:  assets/images/clastic-1.jpg
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