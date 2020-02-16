# Introduction

This project combines elements of two of my favorite projects: DeOldify and EDVR.

Specifically, it leverages DeOldify's beautiful approach to downloading, extracting and transforming videos, but instead of Colorizing them with the DeOldify model, we use EDVR to restore them.

**Source**

DeOldify: https://github.com/jantic/DeOldify

DeOldify colorizes and restores old images and film footage. 

EDVR: https://github.com/xinntao/EDVR

EDVR or Video Restoration with Enhanced Deformable Convolutional Networks is the current (as of 2/20) State of the Art in restoring Videos.

## Background

Unfortunately, most Deep Learning researchers do not pay enough attention to the accessibility of their code. A lot of times there is a lack of documentation on what the code is doing. If a repo is properly documented, the emphasis is on how to train models rather than do inference. 

Usually with enough hair pulling, one can test pre-trained models on images, but doing it on video requires a lot of different things to come together: downloading it, extracting the frames, processing the frames, putting the frames back togetehr, handling the audio along the way and so on...

## The Solution

Probably one of the best implementations of transforming video is DeOldify. I'm a huge fan of how they setup the workflow of handling video and leverage Google Colab Forms to let people play with it like an App. 

The workflow for DeOldify goes like this:

1. Download a video
2. Extract frames & audio
3. Process each frame
4. Put frames & audio back together
5. Voila! Your video is ready.

As we can see the only step that is specific to using the DeOldify model is Step 3. My motivation for this project was to generalize DeOldify where it can take pretty much any GAN model and transform a video. Plug and play. I tried it with some Style Transfer and ESRGAN models and it worked fine. Theoretically - it should just be tweaking the function in Step 3 and everything else should just work.

This particular notebook is customized to EDVR rather than the fully generalized one I hope to get to.

The reason is EDVR isn't quite as straightforward as other models (it doesn't transform one image at a time and there can be memory issues if the group of images passed isn't handled properly).

## Instructions

Simply open the Colab and start running the cells (make sure GPU is running)! You can download any video from your preferred video hosting service and transform it with EDVR. The setup should look familiar to anyone who has used the Colab notebooks in DeOldify.

The main method is called via a Form Cell with a few options:

![Form Example](https://github.com/btahir/deoldify_and_edvr/blob/master/form.png) 

**source_url:** This is the youtube (or other sources) link you want to download your video from.

**original_video_quality:** You can also pass in an argument on what the quality of the video downloaded should be (based on the options we get in youtube).

**data_mode:** The EDVR model you want to use

**finetune_stage2:** A boolean indicating if you want to fine-tune your results using the stage 2 models.

## About EDVR

EDVR has a bunch of models which can take a while to wrap your head around.
Here is their guide for it: https://github.com/xinntao/EDVR/wiki/Model-Zoo

I think It's easier to understand by what they do. There are 5 models in total.
There are 3 models that can enhance the resolution of an image by 4x: Vid4, sharp_bicubic and blur_bicubic.

Vid4 was trained on the Vimeo90K dataset while the other two were trained on the REDS dataset.
The blur model simply deblurs an image without resiizng it.

The blur_comp (my favorite) model deblurs and removes compression artifacts from the video.

The sharp_bicubic model was trained by simply reducing the size of the training images while the blur_bicubic model had added noise in the inputs to deal with. So the blur_bicubic model is better suited to handling blurry inputs vs the sharp_bicubic model.

The EDVR team won the NTIRE 2019 Challenges on Video Restoration and Enhancement competition on the REDS dataset with these models. For their winning approsach tehy finetuned the results on a second set of models that they call stage2. You have the option of selecting True for finetune_stage2 which will run your frames through a second time and finetune them but remember this will double the time it takes to process your video.

## Future Work

Make a more generalized notebok that can work with most image processing models. Maybe make a library out of the code so the notebook looks cleaner/smaller.
