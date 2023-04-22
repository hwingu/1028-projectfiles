---
title: "Creating presentation slides with Stable Diffusion and ControlNet"
date: 2023-04-19T07:44:59+01:00
draft: false
toc: true
images:
tags:
  - 1028
---

## Goal of the project

This project’s goal is to make it easier for anyone to make slides that they want, in any design they want. Essentially it brings customisation to another level because people can start making slide designs if they can describe it and in wayyy less time, so that more time can be spent practising the presentation itself rather than worrying about the design of it.

## Explanation of each step of the process

Below will be an explanation of why I did each step, I recommend that you go through the [how-to-guide](http://localhost:1313/1028-site/posts/howtoguide/) first before reading on.

### Why Stable Diffusion?

I chose stable diffusion because 

### 1.  Creating the prompt and generating images of presentation slides


**Model:** Deliberate\_v2


**Prompt:** presentation slide template, Vintage seamless pen traced print, minimalist flowers and foliage wallpaper risograph pattern white and neutral colors, greenish background, aesthetic, high quality

**Negative prompt:** people, faces, distorted text, blurry, childish, messy, amateur, grainy, low-res, ugly, deformed, mangled, disproportional

**Settings:** Steps: 20, Sampler: Euler a, CFG scale: 7, Seed: 2668747600, Size: 768x512, Model hash: 9aba26abdf, ControlNet-0 Enabled: True, ControlNet-0 Module: canny, ControlNet-0 Model: control\_canny-fp16 \[e3fe7712\], ControlNet-0 Weight: 1, ControlNet-0 Guidance Start: 0, ControlNet-0 Guidance End: 1

  dd

**ControlNet Input:**

![](https://lh3.googleusercontent.com/jCrF-t2PezTzNIsHaR0hDZaufELKww73KrgOnmhHdAQB0EhvrYgonUJt_g6oBYSnCWGuTv_1BX0eEJ6CqIud0TY-s_2xroBYKmuElsVbDnZJuu-oHM9Xhit4EzxzUaJokOBv7F9K0UnvW2Xw22BiBK4)

  

**Explanation of why I used these settings:** 

The model doesn’t really matter using this method, just use any model that you like.

The prompt is "Vintage seamless pen traced print, minimalist flowers and foliage wallpaper risograph pattern white and neutral colors, greenish background, aesthetic, high quality". Stable diffusion tend to generate better looking images when extra prompts such as aesthetic or high quality is added. 

It is a good idea to include the background colors in the prompt. I have found that without the description of the background colours, slides tend to be more inconsistent and varied, which doesn't look that great when all the slides are put together.

The negative prompt can help with quality, the reason why I have put faces and people first is because when generating these images of slides, especially with the prompt "professional". It tends to generate distorted faces of people, which is pretty creepy.

The prompt I used for the example above was one I copied from [lexica.art](https://lexica.art). I looked around on lexica.art for something that I liked and copied the prompt. [Stable diffusion Subreddit](https://www.reddit.com/r/StableDiffusion/) and [civit.ai](https://civitai.com) are probably better places to look for prompts though, since people there are more experienced with creating good prompt while lexica.art tends to be filled with images created by random people using the lexica model on their website.

the resolution is 768x512. The reason why I set it at 768x512 is so that each generation takes less time and memory, meaning that I could render more slides and have more selection of slides. I used to render my slides on 1920x1080, but in my experience, it takes a lot more time to render and takes a lot more memory, leading to memory leaks and crashes of A1111. It's fine to generate the image at a lower resolution at this stage because of the upscaling in the later steps. Also this means we can pump out more images at once.

As for the ControlNet input images, basically I have created a set of ‘blank presentation slides’ which have a solid white background, basic font and layout. The idea of this is for ControlNet to guide the layout of the slide and render the style of the slide without changing up the layout. One caveat to this approach is that the layout will completely depend on the ‘blank slides’. There will be no variation of layout to the slides rendered, which can be a good or bad thing.

The rest of the settings are kept default. Some things could be experimented with such as ControlNet's guidance strength and weight.


**Output:**

**![](https://lh4.googleusercontent.com/XC7UN3L0Q-HEZl73IT563hgsRSvFp_PyQAutRhvL1tx-TRwcCM6Q8EcGFR72MmgDFXqT9XfYxgU_Ygzn-5_wNpcPRgUAoKpZ_bz6mSYtcfl5yv2yJdg6u5odMFZNCdM5tOO7M5ph5tBgmcgNPQBnkGI)**

  

> I repeated this step for each blank slide, and I also put them all in a folder for reference later on

  

### 2.  Removing the foreground (text, objects, etc)

Before removing the foreground, keep a copy of the original.

  

**If it’s a solid background (one colour):** Remove the foreground using image editing tools e.g. Microsoft Paint, Photoshop, etc.

  

**If not:** Bring the image into inpaint **or** Use ClipDrop’s text removal tool.

  

**Prompt:** presentation slide template, Vintage seamless pen traced print, minimalist flowers and foliage wallpaper risograph pattern white and neutral colors, greenish background, aesthetic, high quality

**Negative prompt:** people, faces, distorted text, blurry, childish, messy, amateur, grainy, low-res, ugly, deformed, mangled, disproportional

Steps: 20, Sampler: Euler a, CFG scale: 7, Seed: 2102601361, Size: 768x512, Model hash: 9aba26abdf, Denoising strength: 0.75, Mask blur: 4

  

**Explanation:**

The purpose of this step is just to remove the foreground to get the background which can be applied onto the presentation slide later on.

One thing to change is the denoising strength (Basically higher denoising strength, more different from original image. The denoising strength should be fairly high as we’re changing the image entirely) Fairly high is around 0.75 or higher.

  
And I kept everything else the same.


There have been cases where I was having trouble removing the foreground. Below is an example:

![](https://lh3.googleusercontent.com/DbLUB7FSYYIXPPWSnYwEGUeN7tfN9OczzUO8D2JYkCX9f_yooLmdLUgin6B-TCcBYNJQ7X5ChXU2LSvzcyhDMl6mR6gaVfLA8G0Bb56S7yR_DZxylld1TZ9uRA6hsWtXeptlskBVdhiEotWuJnw3X0A)

What I did was delete the prompt completely and changed it to ‘starry lights’ which gave me this:

![](https://lh5.googleusercontent.com/Isf_A_Ajn4PolYXQvOeUlMvde9UiLAqwrHwErg-YxrZUjCA3AROz33SZXAcxqWkPY_62S013Xt-sQUoimEnmNaWnylMMNXsyXFQ_Pft4o0loLi2JFGjkUNQpNyxfl2nJwONcLRbuqZfChudalItXIQQ)

  

### 3.  Upscaling the background

  

**Send to img2img**

  

**Prompt:** presentation slide template, Vintage seamless pen traced print, minimalist flowers and foliage wallpaper risograph pattern white and neutral colors, greenish background, aesthetic, high quality

**Negative prompt:** people, faces, distorted text, blurry, childish, messy, amateur, grainy, low-res, ugly, deformed, mangled, disproportional

Steps: 20, Sampler: Euler a, CFG scale: 7, Seed: 68616172, Size: 1152x768, Model hash: 9aba26abdf, Denoising strength: 0.5

  

**Send to extras**

  

Postprocess upscale by: 4, Postprocess upscaler: 4x-UltraSharp

  

**Explanation:**

  

The reason why I put the image into img2img first rather than putting it to upscale in postprocess-upscale is to render a higher resolution image first. What I found was that if I put a low resolution image into post-process upscale, there will be artefacts and weird out of place shapes around the image that are very noticeable. Upscaling it first in img2img will give the image more detail, which means there will be less artefacts when post-process upscaled.

  

The resolution is 1152x768 which is 1.5x the resolution of the original image (728x512). I wanted to go for a 2x resolution but my computer specs wouldn’t allow it and kept crashing. But the results with 1.5x looked just fine.
  

The denoising strength is 0.5, it has to be low because the upscaled image has to look similar to the original. I found that 0.4 - 0.5 works fine. Any higher than 0.5 will render an image that looks completely different.


The post-process upscaler I used is 4x-UltraSharp. [https://upscale.wiki/wiki/Model\_Database](https://upscale.wiki/wiki/Model_Database) Link to download 4x-UltraSharp. R-ESRGAN 4x+ works fine too.

  

### 4.  Apply background to presentation slide

  

![](https://lh5.googleusercontent.com/kxQdvV5VF4h1yeuI-NaiCR1EEKzbp0T0K4Z1c2vRAm6MfcXapW3Wug602hIlygMOAV3ZRC408NkbEvj9Sa2sZe27dFYre6X7qaDLAk5JI9L2S9dks_Xu_-ooMhhs2WbhdkCBJvVNGAvZ7eT_lNdhIu8)


I have already created all the slides in my powerpoint, so all I had to do was duplicate the slides and apply the background + customise colours for the charts

![](https://lh5.googleusercontent.com/Y7ao8Ee4MlnJcCY_oeAqV_FFxTTMW1gvEdDlsFf9_IsbrNGTRKuMdI5FdoiQ3qD6LMf5xg82Dqo6kFWqtuohQh_zFBNZQ8h2fNKs2xzzWZffYmQEj8e9cOSU8YnCm232KE2DUi_rIuv7-Yu8Z-7Ip1Q)


## Interesting things I've found with this approach

## Disadvantages with the current approach

1.  Fonts

Due to ControlNet, fonts rendered in the output image sometimes look identical to the input image. One way around this is by  inpainting the text on the original image generated on the first step, then render a new image using the same prompt. However, another problem with fonts is that fonts identified by WhatTheFont (A website that identifies font from an image) are paid. Sometimes free downloads are available when you search for the font online, but that hasn't been the case for all the fonts in my experience.

There is still no websites that does the same thing as WhatTheFont but links to fonts that are free, as far as I know.

Alternatively could look for free fonts that look similar on websites such as:

* [DaFont](https://www.dafont.com)
* [Google Fonts](https://fonts.google.com)

2.  Fixed layout

There is no variation with layout. The layout depends completely on the input slides.

## Approaches that failed but could work

1.  Generating everything at once

This approach also uses ControlNet, but for the input image I used an image with all the slides:

![](https://lh3.googleusercontent.com/Hw22SMBksxd2GPkoqS0Ca4a7YMsV1W8O9Me9dh6CM5dS71Beucs-HY8nJhvqQHEgDV1e-G0R4RubbqImlcgcsEDHjujarle980oqbuG0UQLBMg832G5EvIj3y4GEQwIeO4FYBhkqMn0vhRI7uLWVlzM)

  

This didn’t work because:

*   The slides were too small, so less details
*   It also takes a long time to crop each of them

  

This could work if:

* Somehow more details can be rendered on each slide
*   This can be done by generating a image in higher resolution, but for these I was already generating them at 1400x2700 which resulted in many crashes
*   Or some other technique, maybe with img2img
* A script is written to crop each of the picture automatically
* One way this could be done is using the Image.crop() function in Python PIL

  

2.  Asking ChatGPT to generate the prompt

My previous attempt at using chatGPT for a prompt:
[chatgpt prompt for 1028](https://docs.google.com/document/d/1OD1Dexk3y-IJT206frdklRuWRb-BupImUn9WEr1yYw4/edit)


This approach could probably work with the right prompt, but in my experience, using the descriptions (see google doc above) that chatGPT gave didn’t really give me good results. This was using GPT-3. 

3. MidJourney

MidJourney had amazing results even with simple prompts using only txt2img, however my free trial ended so I couldn't use MidJourney anymore but I wonder what could be done using MidJourney V5.

**Example of MidJourney:**
![](https://lh6.googleusercontent.com/nZ7bnUiGaoQARAZ4oU4qMZ2iBGdk88M_FVSXBtxlTAjCV04c7Nr1r1DIpCu9g73wvtsHCBrCfBoblG9OhfbPiI5s65VR7J_FoTDckYgGWtX-VzaeqquOpPh3WmM75bFujs0MXGgQasUggZpcB8z5cqo)![](https://lh6.googleusercontent.com/hT9fAF-p8-H3vahYql_8Hp8MvwL35EUO_LH9oZd-lxyYBtenL7xRyvqD7Rp1RgeJp8QL7n8ZMGlmYEBssZwoaDjAD1BPSqKcgt4NLRHZny120MybUCwif-vX9P2cOkh3JQBv7F9UJ6JSEcoWoACeLJY)

Definitely not perfect, but had a lot of potential.

4. img2img to generate the slides

This was before ControlNet came out.

This approach had the same idea as the ControlNet one where I used a input image to guide SD to rendering a ppt-ish slide. Example below
```
Prompt: title powerpoint slide, single page, black and white, mountains in the background, clear text, professional, sleek, sharp
Negative prompt: multiple pages, people, faces, distorted text
```
Input image:
![](https://lh5.googleusercontent.com/29FnOQKPmet9oWIgqL36HkQDk0OwIVqZFs8eDLbmTTHP_-wagD1SNu7HxYyR_97OulYTDBKGTQMAzVcaV_1BJIF-cWHWKOZQCJjXy59JnXqTg3aIDYxUO35u-JLwulQX3jQuznO7plYxbn5J2l8Ehxs)
Output:
![](https://lh3.googleusercontent.com/dqcaa6dz0UGihcqVMuihhDEXmneb2pGlsFyJY0ybZ0tJYThW9bho5tfKER-YdyvJOTEBE4F0B-SstAg5njmNahpfuAbt2DB91atj14hq-RSzQf2d0oTQovZb4RP-Bdgxs5VsmLTFYBjjFftpXwVK6RQ)

The layout of the slides definitely were not as restricted as the current approach.

5. Rendering images with lora trained with presentation slides found online

I trained some images of slides that I found on google:
![](https://lh5.googleusercontent.com/T2103shVcF7PNmvQexbUGZ4p6wy2snAO4HyEDgrI2NyTGw1_zeb9PJJ_kPU_Eie_7PcCuvgNt7S47Wu7Q7XUP3_bX3jxITg-B_qQYQ_K8kzfw3WtODDZThlvPh6WbhZPkS9DkZkXjYIR2zu2Lu0LWtA)

> The training data only consists of title slides.

**Test that I did**
```
Prompt: presentation slide template, <lora:last:1>, tree, leaves>
```
**With lora**
![](https://lh6.googleusercontent.com/46tseX0wjN7MgzlCpkzCfgGoYdEkiuetsUvobG9kfoY-hK-xtIuEVree7QRZkf128dnUXXzBFIC-Tmul1K1NnANQX8xwqjVuZe4UkF9Lrz-3Qcz4E5HR83ewRTQIAYhnRsXi7ed1FBhixwmOQArgPJ0)
**Without lora**
![](https://lh4.googleusercontent.com/MJcdY2llZrRmtrt-3j0ukKN5t8O2mhPhcDOtwGHAjeAVyCslkB3ZRzTn2wAB4T2eDa-Q8FM4_ZOb8RWjC-hHtq2qPzxsZxecU09qAoSjg4S9PNBsB3cJcRpSznqpuBszqGhsqfMc-l6G7bnMMPPvHFA)

While it definitely did render a more ppt-ish slide in the example above, I've tried many more tests but most of the slides doesn't really match the prompt or looks straight up broken.

If you want to try out the lora, here's the [link](https://1drv.ms/u/s!App0pCtSTbcBgak1XhOgCLd5K4tkVA?e=Ko3baa)
## Things I haven’t tried yet

1.   Supercharging the project using GPT-4 and maybe automating it
* Could have GPT-4 act as a designer, and the prompter could be the customer describing what they want for the slide and their target audience. Then the slides would be done in minutes.
2.   Training a lora with a lot of ppt slides so that it could render better slides.
