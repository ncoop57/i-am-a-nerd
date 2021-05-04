---
title: "DeepSpeed Investigation: What I Learned"
description: "An investigation into the awesome DeepSpeed library for training large models on a single GPU!"
image: images/deepspeed_overview.png
toc: true
comments: true
layout: post
categories: [deepspeed, deep-learning]
author: Nathan Cooper
---

Deep learning is awesome, but the large compute and data requirements can prevent a lot of amazing people from using the models and contributing to the field. So, when I read about the amazing [DeepSpeed](https://www.deepspeed.ai/) library allowing people with just a single GPU (like myself) to train massive models that would normally require multiple GPUs to just fit in memory, I had to investigate further!


## What is DeepSpeed?

Here is a brief blurb from the DeepSpeed website on what it is and what it can do:

“

DeepSpeed is a deep learning optimization library that makes distributed training easy, efficient, and effective.

**_10x Larger Models_**

**_10x Faster Training_**

**_Minimal Code Change_**

DeepSpeed delivers extreme-scale model training for everyone, from data scientists training on massive supercomputers to those training on low-end clusters or even on a single GPU

“

Some impressive statements, but are they true? Kind of. Let’s dig a bit deeper into how this works.



![Overview of the large improvement ZeRO-2 and the DeepSpeed library has over ZeRO-2 and previous approaches.](https://www.microsoft.com/en-us/research/uploads/prod/2020/05/1400x788DeepSpeedslowed.gif)
_From https://www.microsoft.com/en-us/research/blog/zero-2-deepspeed-shattering-barriers-of-deep-learning-speed-scale/_

DeepSpeed is a library that enables the awesome [Zero Redundancy Optimizer (ZeRO)](https://arxiv.org/abs/1910.02054), which is a highly optimized optimizer (oh how clever) that improves memory management and communication in data or model parallelized work loads by removing redundancy. Now, this might bring up the question “parallelized work loads, I thought we could use this on a single GPU, what’s the deal?” So, the deal is that ZeRO was made to solve the problem of communication between multiple devices by doing some nifty memory tricks that are beyond the scope of this blog post (and my understanding. See [here](https://youtu.be/tC01FRB0M7w) for a full explanation of this.). It just so happens that the ZeRO optimizer also performs CPU offloading, which moves some of the computation off your GPU and onto your CPU. With things being computed on your CPU, some of the model is stored in RAM rather than the GPUs VRAM. This significantly slows computation since CPUs and RAM wasn’t built with this in mind, but it means you are allowed to train bigger models 🤓.


## Putting DeepSpeed to the Test!

To test out DeepSpeed, I used the awesome HuggingFace transformers library, which supports using DeepSpeed on their non-stable branch (though support is coming to the stable branch in 4.6 🤓). I followed these awesome [instructions](https://huggingface.co/transformers/master/main_classes/trainer.html#deepspeed) on the HuggingFace’s website for getting started with DeepSpeed and HuggingFace. If you want to follow along at home, I created a Github repository with the Dockerfile (I’m addicted to docker and will probably make a blog post on docker too :)) and the test script I used to run my experiments on. I tried training the different versions of the awesome [T5 model](https://arxiv.org/abs/1910.10683) that ranged from smallish ~60 million parameters to humungous 3 billion parameters. And here are my results:



![Bar chart showing DeepSpeed increases time to train, but allows training larger models compared to not using DeepSpeed.]({{ site.baseurl }}/images/deepspeed_chart.png)




This is a chart of the different models’ training time in seconds with and without DeepSpeed. As you can see, using DeepSpeed significantly increases training time. However, you’ll notice for t5-large (~770 million parameters) and t5-3b there is no bar for not using DeepSpeed. This is because my GPU cried out in pain and couldn’t handle it. Even with DeepSpeed, I couldn’t get t5-3b to train.


## Conclusion Time

So, with all things considered, DeepSpeed is an awesome library and ZeRO is an amazing optimizer. However, if you were looking for super speed boosts for a single GPU like I was, it ain’t it chief. ZeRO is designed for speeding up multi-GPU setups by efficiently handling memory resources and communication and in doing so does reduce the memory footprint on GPUs. It also does some awesome CPU offloading, which will allow you to train huge models on a single GPU that you would not be able to normally, though at a significant time increase compared to if you could fit the model onto a single GPU. So, my take away from this investigation is this: If you are using a multi-GPU setup, DeepSpeed is the way to go. However, for single GPU uses, only use it if you need a larger model than what your normal GPU can handle.

Hope you’ve enjoyed this blog post and learned some information along the way. Comment down below with any questions you have, I’d be happy to help answer them!

Connect with me:

Website - [https://nathancooper.io/#/](https://nathancooper.io/#/)

YouTube - [https://www.youtube.com/channel/UCKfOCnojK5YV7_hdPjAtY7Q](https://www.youtube.com/channel/UCKfOCnojK5YV7_hdPjAtY7Q)

Github - [https://github.com/ncoop57](https://github.com/ncoop57)

Twitter - [https://twitter.com/ncooper57](https://twitter.com/ncooper57)

LinkedIn - [https://www.linkedin.com/in/nathan-cooper-820292106/](https://www.linkedin.com/in/nathan-cooper-820292106/)
