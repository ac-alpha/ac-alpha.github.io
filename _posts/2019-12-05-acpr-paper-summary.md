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

#### Problem Formulation

We want to propose and calculate a score `V(G(S))` for speech synthesized by a TTS system `G(S)` for some input sentence `S` such that
- The score for more human like speech is more than the score for less human like speech
- The score should be in correspondance with score produced by currently used evaluation method (i.e. MOS)

**Anthromorphic Score (A)**

This helps us to compare the speech synthesized by some model to real human speech. This can be thought as an indicator of whether the produced speech is good (`A~1`) or not. Anthromorphic score is defined as 

<div style="text-align:center"><img src="/img/05122019/anth_score.png" /></div>

where EvaluationScore can be any metric such as MOS, vMOS(covered later), etc.

#### Approach

We propose an ensemble of two models

1. A Discriminator from a speech synthesizig GAN
2. A binary classifier trained to detect fake speech.

#### Training Stage

**Phase I - Training GAN**

We can directly use the discriminator from a trained speech synthesizing GAN because such a GAN has been trained to classify the speech spectrogram input to it as real or fake. So, if we get a score close to 1 corresponding to the input speech then, the input is real as determined by the Discriminator, else it is fake. 

But the problem with directly using the Discriminator of a speech synthesizing GAN is that the speech synthesized by a trained Generator of such a GAN is of very low quality as compared to most of the other state-of-the-art TTS systems. So, the DIscriminator of such a trained GAN would become too weak to differentiate the features between speech synthesized by such TTS systems and the real human speech. To tackle this problem, the Generator of our speech synthesizing GAN only produces the error in speech produced by some state-of-the-art TTS system. In this way, our Discriminator is trained on a "much better" fake speech for better feature discrimination. 

<div style="text-align:center"><img src="/img/05122019/gan_training.png" /></div>

**Phase II - Training Binary Classifier**

Training of this part of ensemble is very easy as we just train a classifier, on human speech samples(spectrogram) as real class and the corresponding speech synthesized by some other TTS system as fake. The final sigmoid score of such a trained binary classifier can then be used as an indicator of the quality of speech input to it. 

#### Inference

<div style="text-align:center"><img src="/img/05122019/inference.png" /></div>

Final virtual MOS (vMOS) after training the 2 models of ensemble is calculated as:

<div style="text-align:center"><img src="/img/05122019/infer_eqn.png" /></div>

where lambda is a hyperparameter of our ensemble. The main reason behind using an ensemble of both of these models is because if we only use the binary classifier, then our model was becoming too accurate in remembering some examples and incorrectly giving them very low scores. And if we used only a discriminator, then our model might give score greater than the real speech to fake speech as seen by our experiments. 

## Results

Here I am including some of the significant results of our paper. Please refer to the paper for detailed analysis and complete results.

<div style="text-align:center"><img src="/img/05122019/results_1.png" /></div>

<div style="text-align:center"><img src="/img/05122019/results_2.png" /></div>

Above are the results of our technique on LJSpeech Dataset. We can clearly observe that the score obtained from our technique is in high correspondance with the already available metric `MOS`. 

## Conclusion

Being the first method towards automatic evaluation of machine synthesized speech, we have tried to eliminate human intervention in the task to a great extent. However, our method is currently not standard. The value of vMOS depends on the dataset used to train the ensemble and on various other factors. Our method is extremely useful in comparison between two TTS models for the quality of speech produced by these thus eliminating any human labour. So, one of our future targets is to standardize this method so that it can be proposed as a metric. Also,  we would like to test our techinque in it's effectiveness to judge if a particular emotion is correctly incorporated to an input speech. 

That's it for the summary!! To get an insight on our work, I would recommend to give it a read. Feel free to reach me out at `achaubey[at]cs[dot]iitr[dot]ac[dot]in` for any queries. 

Cheers!

