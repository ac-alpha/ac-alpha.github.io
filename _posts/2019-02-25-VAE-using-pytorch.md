---
layout: post
title: Variational Auto Encoders
subtitle:  Basic implementation of VAEs
tags: [deeplearning]
comments: true
gh-repo: ac-alpha/VAEs-using-Pytorch
gh-badge: [star, fork, follow]
---

# Introduction

Auto-Encoders are a class of Generative Models which are generally used for dimensionality reduction, i.e. to embed the data into a lower dimension latent space. Simply put, auto encoders, as the name suggests, encode the data into some latent space for better feature representation. For training, Auto-Encoders consist of a encoder network and a decoder network. The encoder network encodes the input `X` into the latent dimension `z` while the decoder network takes the input as represented in the latent dimension `z` and tries to convert it back into the input `X'`.  Auto encoders are sometimes also used to map the input to a higher dimension latent space (**Overcomplete Autoencoders**).

<img src="/img/25022019/autoencoder.png" align="center" />

In traditional auto encoders, the task of the encoder to learn some probability distribution `P(z | X)` . However, by applying bayes' rule for calculating  `P(z | X)`, we see the denominator contains the marginal probability `p(X)` which often becomes intractable because z is often of larger dimensions and integration is not possible. 

Variational auto encoders sought to solve this problem by making the distribution `P(z | X)` close to a known tractable distribution `Q(z)` (usually a Gaussian distribution). So the objective of the variational auto encoder becomes to minimise the KL Divergence between the distributions `P(z | X)` and `Q(z)`, i.e. to minimise the following equation:

<img src="/img/25022019/VAE_Eq2.png" align="center" />

On expanding the term `P(z | X)`, using bayes' rule, we get the following equation:

<img src="/img/25022019/VAE_Eq3.png" align="center" />

Where since `P(X)` is independent of `Q(z)` so it has been taken out of the expectation. Upon rearranging equation 3, we get

<img src="/img/25022019/VAE_Eq4.png" align="center" />

Now, since we know `X` so `P(X)` is a known constant term. Second term on the LHS is the KLD term which we wanted to minimize. So, indirectly, now we want the LHS to be maximized. Since we’re interested in inferring `P(X)`, it makes sense to construct a `Q` which does depend on `X`. So the equation becomes : 

<img src="/img/25022019/VAE_Eq5.png" align="center" />

This is the core equation of a variaional autoencoder which we want to optimize. Focussing on the RHS of this equation, we see that it contains two distinguishable terms. First one is the likelihood of the data `X` given `z`, which correspond to the Maximum Likelihood Loss which is traditionally used in an auto encoder as a loss function. However, the second term on the RHS contains the KLD between the distribution to be learned `Q(z | X)` and some known distribution like gaussian. The second term is sought to be regularizing the traditional MLE loss.

# Code and Implementation

One problem still left with our model is that our model still contains a stochastic unit which samples `z` from `Q(z | X)`. Stochastic gradient descent via backpropagation can handle stochastic inputs, but not stochastic units within the network! Solution to this problem is called the reparametrization trick. What we do is to move the sampling to an input layer. Given `m(X)` and `S(X)` — the mean and covariance of `Q(z | X)` — we can sample from `N(m(X), S(X))` by first sampling `e` belonging to `N(0, I)`, then computing `z = m(X) + e*(S(X)^1/2)`.

<img src="/img/25022019/VAE_pipeline.png" align="center" />

I have used [MNIST](http://yann.lecun.com/exdb/mnist/) dataset to train a very basic VAE using the pytorch framework. The full code is well documented and maintained at this [github repository](https://github.com/ac-alpha/VAEs-using-Pytorch). Don't forget to leave a star if you liked the repository. :)

## References

- [Auto Encoder Variational Bayes Paper](https://arxiv.org/abs/1312.6114)
- [Tutorial on Variational Autoencoders](https://arxiv.org/abs/1606.05908) - **All images have been taken from this tutorial**
- [Ali Ghodsi, Lec : Deep Learning, Variational Autoencoder](https://www.youtube.com/watch?v=uaaqyVS9-rM) - **must watch**
