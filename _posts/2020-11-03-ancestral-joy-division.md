---
layout: post
current: post
cover:  assets/images/jd.jpg
navigation: True
title: Ancestral sampling conditioned on Joy Division
date: 2020-11-03 5:34:00
tags: [Jukebox, ancestral sampling]
class: post-template
subclass: 'post'
author: gabriel
---

I want to check how is the sampling of an artist that I know well, and so I decided to perform ancestral sampling of the Jukebox `5b` model of two artists whose catalog I know well: *Joy Division* and *Lucybell*. While the former is pretty well known and has just a few official albums, the latter is my former band which happen to be in the `V3` list of artist, which is tied to the `5b` and `5b_lyrics` models.

For Joy Division, I requested 16 samples with `sample_length_in_seconds=60`, in five genres (Dark Wave, Gothic, Coldwave, Hip Hop, and Glitch Pop). It took:
```
    Nodes: 1
    Cores per node: 6
    CPU Utilized: 14:55:31
    Job Wall-clock time: 14:59:55
    Memory Utilized: 23.10 GB
```

For Lucybell, I requested 3 samples, 60 seconds. Note more than five times the number of samples didn't take five times longer. Also, memory used for Lucybell was actually a third larger. Perhaps this is because I ran these two processes in two different clusters. I requested the same GPU though (Volta V100).


  ```
  Nodes: 1
  Cores per node: 10
  CPU Utilized: 08:05:34
  Job Wall-clock time: 08:05:12
  Memory Utilized: 31.02 GB
  ```

Joy Division samples

  <iframe src="https://archive.org/details/ancestral-sampling-by-artist-joy-division#" width="500" height="250" frameborder="1" webkitallowfullscreen="true" mozallowfullscreen="true" allowfullscreen></iframe>

Some of the samples sound (e.g., `item 0`)like a rehearsal in a garage, or a live bootleg take. This is actually possible, since Joy Division has several bootleg albums.
Other samples sound such another band (e.g., `item 1`, `item 10`, `item 11`, `item 13`), but from the same period and similar style and sound (i.e., post-punk, punk, or somewhere there)

From what I remembered, `item 2` is the one that sounds closer to Joy Division. The shout at the beginning is very similar, I think, to one in a Joy Division song. Another examples sound very similar to you could expect from Joy Division (e.g., `item 10`)

Some examples seem to be strange parts of the model (e.g., `item 12`, `item 8`), where there is lots of silence.


My favorite ones are `item 14` (rhythmically interesting and nice attitude) and `item 3` (very nice mood but not Joy Division-ish, at all!)

**It seems that the query is somehow close to the period and style attributed to Joy Division, but it is not actually retrieving and decoding something memorized**
**The songs seem to be _correctly tuned_, there are no weird shifts in tuning and seem to be consistent over time and across songs**

Lucybell samples

<iframe src="https://archive.org/details/ancestral-sampling-by-artist-lucybell#" width="500" height="250" frameborder="1" webkitallowfullscreen="true" mozallowfullscreen="true" allowfullscreen></iframe>

The three examples are in the form of a guitar-driven ballad, which is actually very close to most popular songs of Lucybell. It is interesting that all start in a similar way: a leading instruments, such as a solo guitar or leading piano. The second example (`item 1`) has a very nice phantom choir that accompanies the lead vocal.

None of the examples sound very *Lucybell* to me, but the there is something stylistically similar.