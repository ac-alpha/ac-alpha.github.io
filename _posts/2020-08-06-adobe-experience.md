---
layout: post
title: My Internship Experience
subtitle: Big Data Experience Lab, Adobe Research India
tags: [general, deeplearning, interns]
comments: true
---

<div style="text-align:center"><img src="/img/06082020/adobelogo.png" /></div>

## Introduction

Recently I finished my (unfortunately, remote) research internship at Adobe Research India. The whole remote internship experience was a complete roller coaster ride, but I have to say, that people at Adobe really tried their best to make the experience smooth for us (interns). There were about 90 interns who did their internship in the Big Data Experience Lab from end of April to almost mid of July. The total duration of the internship was 12 weeks. We were divided in to teams of 3 or 4 people belonging to each group. Each group was assigned two mentors (full time employees from the lab), one junior and one senior, to help us get along the project (believe me these people were gods in their field of expertise). 

## About Adobe Research India

Big Data Experience Lab, Adobe is among the top 2-3 corporate research labs in India. Personally and from what I have heard, I can surely say that it is one of the best labs for deep learning research in India both in terms of the work and (obviously) compensation. Though one thing that I would like to point out from my observation is that there are relatively more people working on Natural Language Processing than Computer Vision in the lab (this is not a con, but since I am more interested in Vision, so I pointed out :P). One more thing that is unique to Adobe Research India, is that it is the only (good) research lab in India which hires graduates as full time employees (with no fixed term contract) as opposed to a few labs which only support residency/fellowship programs to graduates that last for only an year or so.

## Intern Application Procedure

Now that I have praised plenty about the lab, the question that needs to be answered is how did I land up at Adobe Research India as an intern. There are a couple of ways by which you can get a research internship at Adobe. I got a direct offer to join in as an intern based on my Academic performance (top 2-3 students from STEM branches in the top institutions of India get this offer). Another way, was to give written tests and interviews conducted by the campus placement cell. And finally there is a scholarship specifically for girl students, Adobe Women in Tech scholarship which might land you up in Adobe. 

Disclaimer: There might be a few other ways to get a research internship at Adobe. I have just listed down the ones that I am aware of. One more thing to point out is that **Adobe Research India doesn;t directly offer full time roles to graduates if you haven't interned there. They only give full time (pre-placement) offers to those who have interned at the lab.**

## Nature of Work

The project that I was a part of was heavily based on the concepts of Active Learning and Reinforcement Learning. Our task was to optimize the annotation budget while developing a content detection framework. The major problem with most of the existing active learning techniques was that they relied on some heuristics such as entropy, confidence score, etc. But one can't be really sure on which heuritstic would work in the task of interest in hand. While simple heuristics such as entropy might work in easier tasks such as image classification, but using such heuristic as an acquisition function in the case of complex tasks such as object detection becomes very complicated because there is no "perfect" way to aggregate the heuristic scores for the various entities (bounding boxes) present in the image. 

Hence, we proposed a reinforcement learning based technique to learn an optimal acquisition function for content detection tasks in general, where in we showed the effectiveness of our proposed approach on object detection, document layout detection and named entity recognition. Furthermore, in a usual human in the loop active learning process, the annotator has to mark all the boxes and the corresponding labels corresponding to those boxes from scratch. But instead, to ease the annotation effort, we propose that the annotator should also be shown the predictions of the current model on the sample to be annotated. This way the annotator just has to weakly supervise the annotation process. We also tweaked with the reward functions to make sure that the newly acquired samples are class balanced. 

**Note: I have kept the description of various parts of the project vague in the above paragraphs on purpose, as I am not authorized to share the exact details of the project in accordance to Adobe's policies.**

## Conclusion

I would definitely say that if you want to have a taste of how does research happen in a corporate environment. The major differences that I observed was that researchers in an corporate lab are more interested in the things that actually "matter". By this I mean, that they care about innovation that might (not at the moment) be incorporated/used in any of the products that they build. This, in my opinion, is the most interesting part as it really got me motivated that the thing that I am working on might end up being incorporated in an Adobe product. Thrilling isn't it?...

On a concluding note, I would definitely say that Adobe Research was really a good place for a budding researcher like me to gain a plenty of experience and getting me a step closer to becoming a true data science researcher. :)

PS: Forgot to mention that HR team at Adobe also conducted fun events every weekend to keep us interns involved and entertained even in this remote environment. Also, Adobe provided us with a bunch of goodies to work in the remote environment. 