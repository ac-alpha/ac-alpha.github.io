---
layout: post
title: A GAN based Ensemble technique for Automatic Evaluation of Machine Synthesized Speech 
subtitle: J Jaiswal, A Chaubey, et al
tags: [deeplearning, publications]
comments: true
---

This is a short summary of our paper `"A Generative Adversarial Network based Ensemble Technique for Automatic Evaluation of Machine Synthesized Speech"` recently published in the Asian Conference on Pattern Recognition (ACPR 2019). 
You can download the camera ready version of the work <a href="https://ac-alpha.github.io/ACPR_2019_paper_148_v4.pdf" download> here </a> and poster <a href="https://ac-alpha.github.io/ACPR_Poster.pdf" download> here </a>.

## Introduction and Motivation

The basic motivation behind our work is the wide scale application of Text to Speech(TTS) systems. TTS systems basically take an input sentence `S` and convert that to speech spectrogram or basically speech. Some of the examples of TTS Systems include [Deepvoice](https://arxiv.org/abs/1702.07825), [Tacotron](https://arxiv.org/abs/1703.10135) and [Wavenet](https://deepmind.com/blog/article/wavenet-generative-model-raw-audio). 

<div style="text-align:center"><img src="/img/05122019/tts_system.png" /></div>

One basic stage in developing a TTS System is the evaluation of human-ness of speech produced by such systems. Current evaluation methods require determination of various acoustic parameters such as frequency, pitch, loudness, amplitude, etc. first for real human speech and then comparing these with the parameters calculated for synthesized speech. Also, these methods suffer from subjective variance due to human intervention.

The above mentioned points motivated us to propose a method to automate the whole speech evaluation process to some extent. Our work has the following major contributions
- We propose first* Automatic Speech Evaluation method for TTS systems
- We calculate and compare our proposed score for state-of-the-art TTS systems
- We compare our score and show it's correspondance with currently available evaluation metric(i.e. MOS)

## Previous Approaches

Speech Evaluation of all TTS Models is typically performed by human, basically “natural speech experts !”. 40-50 of these experts are made to listen to the speech produced by the TTS Systems and they rate those speeches in terms of how human-like they sound (higher being more human like). The weighted average of their scores are then used to calculate the [MEAN OPINION SCORE](https://en.wikipedia.org/wiki/Mean_opinion_score) (which is on a scale of 1-5). It is speculated that a MOS difference of approximately 0.5 is required for the users to be able to detect any noticeable change in quality.

<div style="text-align:center"><img src="/img/05122019/mos.png" /></div>

## Methodology

Main idea behind our approach is to use the fat that neural networks are good function evaluators, so model the objective of speech evaluation using them.

### Problem Formulation

We want to propose and calculate a score `V(G(S))` for speech synthesized by a TTS system `G(S)` for some input sentence `S` such that
- The score for more human like speech is more than the score for less human like speech
- The score should be in correspondance with score produced by currently used evaluation method (i.e. MOS)

**Anthromorphic Score (A)**

This helps us to compare the speech synthesized by some model to real human speech. This can be thought as an indicator of whether the produced speech is good (`A~1`) or not. Anthromorphic score is defined as 

<div style="text-align:center"><img src="/img/05122019/anth_score.png" /></div>

