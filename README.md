# Introduction

This project combines elements of two of my favorite projects: DeOldify and EDVR.

Specifically, it leverages DeOldify's beautiful approach to downloading, extracting and transforming videos, but instead of Colorizing them with the DeOldify model, we use EDVR to restore them.

**Source**

DeOldify: https://github.com/jantic/DeOldify

DeOldify colorizes and restores old images and film footage. 

EDVR: https://github.com/xinntao/EDVR

EDVR or Video Restoration with Enhanced Deformable Convolutional Networks is the current (as of 2/20) State of the Art in restoring Videos.

## Background

Unfortunately, most Deep Learning researchers do not pay enough attention to the usability of their code. A lot of times there is a lack of documentation on what the code is doing. If a repo is properly documented, the emphasis is on how to train models rather than do inference. 

Usually with enough hair pulling, one can test pre-trained models on images, but doing it on video requires a lot of different things to come together: downloading it, extracting the frames, processing the frames, putting the frames back togetehr, handling the audio along the way and so on...

## The Solution

Probably one of the best implementations of transforming video is DeOldify. I'm a huge fan of how they setup the workflow of handling video and leverage Google Colab Forms to let people play with it like an App. 

My motivation for this approach was to generalize DeOldify where it can take pretty much any GAN model and trasnform a video. Plug and play. I tried it with some Style Transfer and ESRGAN models and it worked fine.

This particular notebook is customized to EDVR rather than the fully generalized one I hope to get to.

The reason is EDVR isn't quite as straightforward as other models (it doesn't transform one image at a time and there can be memory issues if the group of images passed isn't handled).

## Usage

Simply open the Colab and start running the cells (make sure GPU is running)! You can download any video from your preferred video hosting service and transform it with EDVR.

## Future Work

I would like to make a more generalized notebok that can work with most GAN models. 
