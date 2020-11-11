---
layout: post
current: post
cover:  assets/images/temperature.jpg
navigation: True
title: Experiments with temperature in Jukebox
date: 2020-11-06 9:11:00
tags: [Jukebox, temperature, neural synthesis]
class: post-template
subclass: 'post'
author: gabriel
---

Temperature is a hyperparameter of neural networks used to control the randomness of predictions.

Temperature works by scaling the logits before applying softmax. In deep learning, the term logits layer is popularly used for the last neuron layer of neural networks used for classification tasks, which produce raw prediction values as real numbers ranging from (-inf, +inf)

In other words, _temperature is the randomness of the decoding process._

When the temperature is 1, we compute the softmax directly on the logits (the unscaled output of earlier layers), and using a temperature of 0.6 the model computes the softmax on logits/0.6, resulting in a larger value. Performing softmax on larger values makes the network more confident (less input is needed to activate the output layer) but also more conservative in its samples (it is less likely to sample from unlikely candidates). 

As a result, **using a higher temperature produces a softer probability distribution over the classes, and makes the RNN more _easily excited_ by samples, resulting in more diversity and also more mistakes.**

I want to check how the Jukebox's sampling process changes when changing the temperature. For this, I sampled the Jukebox 5b model with the tuple condition `[Joy Division, Hip hop]`, with three different temperatures: `[0.75, 0.95, 0.975]`

<iframe src="https://archive.org/embed/experiments-with-jukebox-temperature&playlist=1" width="500" height="300" frameborder="0" webkitallowfullscreen="true" mozallowfullscreen="true" allowfullscreen></iframe>

Temperatures of `0.75` don't yield anything meaningful, just noise with occasional blips.
Temperatures of `0.95` yield some song-like excerpts (e.g., `0-item 1-0-95`). Similarly temperatures around `0.975` also yield song-like excerpts, but slightly more chaotic and noise-pron (e.g.,`1-item_2-0-975`, `2-item_2-0-975`)

My favorite one is `0-item 1-0-95`



