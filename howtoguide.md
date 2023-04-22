---
title: "How to create presentation slides with Stable Diffusion and ControlNet"
date: 2023-04-19T08:11:13+01:00
draft: false
toc: true
images:
tags:
  - 1028
---

## Prerequisites:

*   [Install the blank slides](https://1drv.ms/p/s!App0pCtSTbcBuQyuqVM_MjJNvHTU?e=VrzF1o) (Optionally create create one yourself if you want a different layout)
*   [Install blank slide images](https://1drv.ms/f/s!App0pCtSTbcBuRAHZmb6k8JtdCdu?e=zP66aR)
*   [Stable Diffusion A1111](https://github.com/AUTOMATIC1111/stable-diffusion-webui)
*   ControlNet

Here are resources for [setting up A1111](https://www.youtube.com/watch?v=3cvP7yJotUM) and [installing ControlNet](https://www.reddit.com/r/StableDiffusion/comments/119o71b/a1111_controlnet_extension_explained_like_youre_5/).


### Some things you should know
**Location of your stable diffusion folder**

This is typically found by copy and pasting this into your folder directory as shown below:

```yaml
%userprofile%\\stable-diffusion-webui
```
  

![](https://lh3.googleusercontent.com/iJSwqDG293E6dGa8XNlsjG-FkdWOMfgPd-dikDVZh92pyUZ1AorF__k-BmLKAuuefI-hI2HynIZnVVm86CXdwt0AU5jBUYVvVmBaf05JEw03nJKr3MWjazbYh5Nx9GxDAA2z_b5YmEd3i21sEpNgql8)

  

Inside your stable diffusion folder, there will be a lot of files, folders… Below I will be explaining a few that you need for this guide.

  

![](https://lh4.googleusercontent.com/LDbA2QzK5Z6g5OkDl57BobR8NP8ZvEGZWCtFb3NorHbOcWNisYAVeSrWP1hxkuEO_-N2PVKUhugh2DDcf43tpBQ5pWBry14gojEJXcRDq9fT4RqD5SW2EZfGqB_w8RQEvyzLOvWBf4_PMVlM9sDbwcQ)

webui-user is what you will use to execute the Automatic1111 webui. 

  

Make sure that your webui-user contains this:
```
@echo off


set PYTHON="C:\\Users\\%userprofile%\\AppData\\Local\\Programs\\Python\\Python310\\python.exe"
set GIT=
set VENV\_DIR=
set COMMANDLINE\_ARGS=
git pull
call webui.bat
```
  

>To edit the webui-user file, right click on it (show more options if you’re on windows 11) and click on edit. A notepad should open. Copy and paste the above into the notepad.

  

![](https://lh5.googleusercontent.com/Aeei_zRos1m0OnnH7uQSmlzML7y0EAsbxt0_Ia8l_ut5_ff6qNduIg7fAPPYY26FVoQ2rU4IyB07W0baUe6OfgI0YoA_50ecDCpiVGXpc7Sc1EzKvXjwfx8uoXmhmfi45iVzTHDgyXzHH4RiGVYaxGI)

The output folder is where all the images you generate are located.

![](https://lh6.googleusercontent.com/GOGD6iN8HemE0fI-omchUnGKJrPEZSuT-mh3yTCS8MeAiMooJFrpSa_KbVjEnGp5wE4Gbj2PY-n49_z8jaSfRjIfDzbO-gFtz54-tJb6VSi82uRQO5MgtnyA8j6ByJ7w816CjLpIfjzujdmcPL2g7rE)

  

**Extras-images -** contains all images that you have upscaled in the extras tab. 

**Img2img -** contains all the images rendered using inpainting and img2img, which we will use later on.

**Txt2img -** contains the standard prompt to image rendered image. 

![](https://lh3.googleusercontent.com/AZyhY9QuoDVhYOOquG9aTZDyQ8KYKWSHVTqUz_fgE_CQVqaigMRmTy0K0FOLa4n4bUda-3dlylaxU2cADgfIoMYrGMY3o4BW1MZUhdlwXABiFenObs1XKeLUKF1dafX93_sY7x5agUJujhEN_DWSyRI)

The **models** folder contains all of the stable diffusion checkpoints, models, upscaler, etc.

  

![](https://lh6.googleusercontent.com/zzfOsy7QBWSvJblvaEeR0agJGbKg5i6NZTDSrzOjexrKPAMdfO27-Pa0DsBviiqrabHq4Ri5R06bLcxMvvfxTjpVRCNwgkLlTm71Am3J8HgKfBKV1cCtWfHdjbpuTK8vTxQG3yiYv5IEbf2AxX9vgzA)

The **Stable-diffusion** folder within the models folders will contain all of your checkpoints and where you will put your new checkpoints.

  

![](https://lh3.googleusercontent.com/TrwePpozftMS5pWQIjTQRNxZtacsa9YMm89AtXkPy_LkCD_VjE_0sP73ZJM2-0Ma8cW-MLZ16ieYhPFb0gGPlMtcL4GFegvNuD66JKwqdqTJRWyXkgTz1d1GA9fPz0PAbXyRQ185B538Sw30-WFp5T8)

![](https://lh3.googleusercontent.com/r_nkAtoqDPUnQr9mnqTF_sJJSW8TRT4dAdz3-s9m2_PfxZBn3dNThb7Hfit7vlN35QerwgcaOXIeceYM8UiiEWn8_hY3wSXmtjzkgPgzUnLJVNbJqZg1YDRmC_AD8DM6kYoXDGG7tjL52rfLcQKQJ2k)

Above is the **A1111 WebUI** where you will be doing almost everything.

  

There will only be a few settings we are changing in this guide:

  

### A1111 Settings

**Width and height -** The resolution

  

**Batch count -** How many images are being rendered at once (I like to set this at 4, depends on your gpu)

  

**Prompt -** Prompt for the image

  

**Negative prompt -** What you don’t want in your image

  

### ControlNet Settings

**Preprocessor - ![](https://lh4.googleusercontent.com/EY27ct2SYS-YUunQCpHzqb-4kERsRGsHPmp_ChKikgFW5K5YWbkzgTzJVKcek1ev7j1VBpDU0SeafDKWfIW6KRNqq46BYuPnCc4pWCvQG7hA9-RfQEpKHMt4eqzcO5XqFBjWEJIno6tkHZ-c1jVIPu4)![](https://lh5.googleusercontent.com/OCuE9TI29R6q65c12bJsVoqOQg0_GlOxHdxf-ZotINCBMDhgbSSPjow9W2r_J88KbMCVd-mLLe6TXvZq2HaE0-1b2SqFk6QyGs2mLSZk3wkVdntZ-HmcWGgA4pNN-ToWWnWGQrGTlBEdeM7HNb33Ut0)** 

  

  

**Model -** ControlNet’s model

  

### Other useful things to know

  

 **![](https://lh6.googleusercontent.com/gCMVi1QEALGf1YuL6pW1V6hKNZT_MIWie_jfCoADFPqMrryERq2WorFEy_AS0GICL0QhG2n58O2U8fd9RcxFhIUSA1Inabkvwh91ncVN0ULtR4qQb64qZOZA867dAkc_3_bLnvqcxoHOqJYueeL7Gm8)**

This button located under the ‘Generate’ button allows you to paste prompt and settings from last image generation

![](https://lh3.googleusercontent.com/IgUxcOSzyF6wMr6pCMmOcHaFQWWt_kn3U4IAsjgqjrMajngpnIWTm6C81KoL1GqeawAUI7ctEe_Blr2TtfczuO1XOsx5tmHGL2DCWMhmRK5KbfB58ve1P5ZnV9B3D639Sf4WFb-iS1Jbr_doYdMqys8)

  

**The folder icon** can also be used to open stable diffusion folder


**Send to ‘ ‘** allows you to send the image rendered to the corresponding places directly.

  

![](https://lh5.googleusercontent.com/80tVxDUMV7gTTWoiWazzTtSL_Li0CC0GgPfSiKXjv0wfAFb7RNBZWp_etMSA7qCW7uSIiumrxq7W46SQAIOHFFWF4izKVQe2AYH0W2DSgu3i1dhZW_4uiyGJ_EOj6a1i-anoH6TsWlhHmObTfQdjfoQ)

The PNG info is extremely useful, if you put an image you rendered with A1111. It gives you all the information about the prompt, negative prompt and settings you used to render the image.

  

## Step 1: Creating the slide images

Before you start, you have to make a prompt or find some ‘inspirations’. Here are some websites for finding amazing prompts.

> Even if you are planning on making your own prompt, I do recommend looking through these websites to get an idea on how people make good prompts.

*   [Lexica.art](https://lexica.art/)
*   [Civit.ai](https://civit.ai/)
*   [Stable Diffusion subreddit](https://www.reddit.com/r/StableDiffusion/)

  

> Once you find an image that you like, copy and paste and add ‘presentation slide template’ at the front of the prompt. For example, “**presentation slide template**, Vintage seamless pen traced print, minimalist flowers and foliage wallpaper risograph pattern white and neutral colors, greenish background, aesthetic, high quality”

Also, it is good to have a negative prompt to avoid things you do not want on your slide. To give you some ideas, I normally use:
```
people, faces, distorted text, blurry, childish, messy, amateur, grainy, low-res, ugly, deformed, mangled, disproportional
```

Next, use the image of the blank slide as the ControlNet input and use the settings below.

To insert the the ControlNet image, in Automatic1111, scroll down until you see **ControlNet**. 

![](https://lh5.googleusercontent.com/EUrLr0uQ5Ak_pvENJsXLK05-pEw0AkdkRZs2yk5_JtMk03_ToN-xraewXFpWGR_T6LHpu1XycF-gCDkcRBiFlPE2Hh1qYYITS1u8mHS7Hnq8rnOQwmjsOcHVurah6Za-AWlAmd91rvXz2oIZyry2Qs8)

Clicking on it should reveal the ControlNet settings. 

Drag your image into the image box like the one below.

![](https://lh6.googleusercontent.com/nBtCUAhAP8kC7dbDQ04t6g109zJyhERsZqpt7kEjvrg6vWBX8iOgjVwPr_X6BaV5HnOtypK7sKwamyYQP2xCS5nTzn0ILz2LMNGSmvfN_coYwrqamMycQxgmkGn2VElgfcIq6AoV1Pw2mPEe8TMxs3k)

Also in the ControlNet settings, make sure to check **Enable** and set the Preprocessor and model both to canny. Below are the settings used for this step.

**Example Blank slide**

![](https://lh4.googleusercontent.com/GcsZbszCJ6HxHwW9EcJHdRPcfdv2yCK3FfScXPN7AflavF3NYYN5bzlPr3slDwgDkRORgXoHrRtb0t26IU3svDYnYKmih55T44Cs8zePY9X_GJeAdZhsS9AsIzdMche1bva62nmb83Br0QZQyN987oI)

**_Text2img settings_**

![](https://lh5.googleusercontent.com/kCdOtiOF0PNa0pQr7Y0maHrTFRSJBxrL1eZnK0y4CaeqX3TGucM8mBZHaff1MfJDsCJRyciLiwgZoRIA0E9J7JCq84QQwNzQlJGx9p_zy9ZeZqyC6o8aTG-0b8PagBqQJM5TNRCHeB1AwJxegikFUf8)

**_ControlNet settings_**

![](https://lh3.googleusercontent.com/WJTB3xQDwa64uDpHLdhxFb0dvEb8tgtIS6VQEAKW8B1va5aZUpGGBPWlYONOwdtRvI_yEPzvUck90n7fw_t26DjEBQIebLaEEDz_8aom1l6gPpikWiPujN3x_kHY9q_tO03UmCk8riv1CLVfb8kCwD8)

  

Do this step for all the [blank slide images](https://onedrive.live.com/?id=1B74D522BA4749A%217312&cid=01B74D522BA4749A) 

  

> All the slide images generated at this stage are located in the **txt2img folder**.

> You can increase the batch count under **text2img settings** if you'd like to render more than 1 image at a time.
  

## Step 2: Removing foreground

If the image has a solid background (background with only 1 colour), use an editing software (e.g. Microsoft Paint) to delete the text. 

  

If not, follow the steps below:

  

1.  Go to inpaint, located under img2img tab
2.  Use inpainting to cover up anything to remove
3.  Make sure that denoising strength is set to 0.75 or higher (Basically higher denoising strength, more different from original image). Keep your prompt the exact same as the original for your first attempt at removing the foreground

The settings should look like this:
![](https://lh5.googleusercontent.com/bf42ki4tiE6K8Nze78WXlUuCG_zNNA2p72Tuxhaas3FmhhdS-saNcMQZpDfoVj2Jdeu6IoEiNmCWnkMrD-yvcwDIwmod0w8DFv5l7IFZsbEBXK-m3F5_CPr_8Aklqzw7tBke9L7aZ2HgjDnRlX93EI4)

4.  Repeat for every image

  
### Solution to artifacts not removing
Sometimes, there will be aritifacts on the image that don't go away no matter how many times the process above is done.

  

One example of this is with this image:

![](https://lh3.googleusercontent.com/-hcZvcSA_wMA8nLaplAs4GzpbUC4rYqByLdcVVjCpSGlxsoHSuDDK14nT0jIQrLIDzAetpUvIqwslAkweKSTp6C7uEo4wNX5wK5FlBrpmhChp6HIzmAKuQjpRFbY6x-8QYjwxFI0Re5zUFBn9wH3M8I)

No matter how many times I render the image with the artifact on the top left covered with inpainting, some artifact pops up on the top left.

  

The solution to this was changing the prompt to just “starry lights”. Just try to be creative with the prompt, remove your original prompt and start over with a new prompt.

![](https://lh6.googleusercontent.com/EaxxJjRhxx4pDg9pmpJYPqf1vmHhW80AzYqp4s1LjwZWq1lUZJ7OmsbEi3Ozj2WHBEU0xgGA0CU_KYRf59xt2wH-4xFu4-Z4vtecnmfgdUTH29D2SQDDnTHnC-1BCoRLJJQq7ErXXzAW-iBd_EI7bbk)

  

  

## Step 3: Upscaling

Now it’s time to upscale the background images, you will be able to find the background images under the img2img-images folder under outputs.

Navigate to img2img and insert your image.

![](https://lh3.googleusercontent.com/LbWhnTBjDmqvqpkOMJfweTGvUYyDfZv-0yoD9SgtoCe8MjFpBtjcdB-In78wCLOn3AxH-K_ViqGS_snaqv17boZlSGBt10ueRDiKUmBDe18IJKVoX-HUe9Yz8hevkV2EqiJ45uyVi7mZMBuq0CemkQY)

Use the same prompt you used for your first step. Set denoising strength to 0.5 and set height and width to 1152x768 (1.5x 768x512), Go higher or lower depending on your GPU. Image of img2img settings below for reference.

![](https://lh3.googleusercontent.com/CjisMF6316zB-n29gWQZkc_c-rDcH-O39R3BSxdfnF0XFxA7ww8iARj0e7_ZnCcT4QRcJHP1WmiKbN8R4F9VQjMHmRfp-FyqXzIHiKDP9fvUUvI5vBOo2C3s7wgwJr9T-NksU9AeU6twraSfw1IEqZ0)

For images that are very detailed, you might have to go for a lower denoising strength like 0.45.

  

The point of this step is to prevent low resolution artifacts that are very noticeable when the image is upscaled straight away. Img2Img can render the image in a higher resolution first.

  

If you like the rendered image, send it to extras.

![](https://lh4.googleusercontent.com/AhM6Gr67OmaN4tGOG40K9btUDy72cjnqzF_UWzBUrXvylmP-t8udZN_el5EKM3SDEz5Azl5Dbf7PBOyJ_01DtCF-qpLuGz2kToc4J0kx1rTIzTwxn42OLmehewhd3YyfEw6Buv79QB0YCP1ffcdbWiI)

  

![](https://lh4.googleusercontent.com/AT8BaI4amWeKvzb7X_KSnG8V6R7HlImOFQAdimv2mAquPu8pMT8WAtcKsy0BSm_hdmEzq4PZI1DY-9GJsoiC1tvyL5nChaz6LjCP3auRrC-I4M5p9eY1GVyM7NdtOGwE-F9ZPFtCTKOo_azTsW0DiDY)

The only setting to change here is Upscaler 1. From my experience, 4x-UltraSharp and R-ESRGAN 4x+ both works fine. You may want to upscale the images in a lower resolution, by decreasing the resize, to lower the image size.

  

## Step 4: Applying background and style to slides

Open up the [slides that I made](https://1drv.ms/p/s!App0pCtSTbcBuQyuqVM_MjJNvHTU?e=VrzF1o), or yours if you made one yourself. All you need to do is change the background of each slide to the upscaled background. You can find the upscaled background in the extras folder located in the output folder.

  

The layout of the texts and graphs should already be in place.


To change the background, there’s a format background button in the design tab.

In **format background**, select **Picture from File**


### Pie charts, bar charts and icons

Powerpoint allows for an in depth customization of data charts such as pie charts and bar charts. Customisations include:

  

*   Colours 
*   Gradient 
*   Shadows

  

Simply double click on the part of the chart, whether its a pie chart or a bar chart, that you want to customise to bring out the customisation tab

  

![](https://lh3.googleusercontent.com/cILoECELbaJlaIDZaTppxcZwuWkKrT1sYUStDfYNMZE9rgW_RYB_R3-plmxC7jnCq96a08sYYAqQGg5hcubTmW9nFalsHGr6fcJ9cuz2DfQ7HIfbRdSTuMuQRj_0qbNsaEudYjNQJtvNS4hvb7pnpf8)

  

### Texts/ text colour

To further customise it other than colour, right click text and click on ‘Format Shape’ which will allow customisations for shadow, glowing effects, etc. 

  
### Fonts
As for the font, sometimes it generates a new font, sometimes it doesn’t on the original image that you’ve rendered in step 1 because we are using ControlNet.

  

>There’s one way around this though which is inpaint. Just pick an image you rendered on step 1, denoising strength should be at the lower end (0.5-0.6), keep every other setting the same and use inpaint brush to cover the texts. Rendering the image again should render an image with the new font.

>Example:
![](https://lh3.googleusercontent.com/EYEjG1Hfrt0YcGbo8Zv5igKyPKUTJEh3N5XAsKJ2dZPGUW6fljgG9nejmdDTYTTdC8GprB0e3467OcSSHyZSa9D7CP5Zb_o9VgTFw_ja-uuWl9ZRXFV9TN3EpSm1QBAIicFrGLy5EbYwoMxCnSEuyM8)![](https://lh3.googleusercontent.com/gj6X1nyxenILGIwU1-e-Z2dpklTsMCxIG-1SuXVgAvYHkVI9El2lLK2xCvOxRzF6NxKfKFKX8BeacABgd92omdSoyRRjNLF33oV2bPlzbTrZ8i1wpATVYRzkO_a8iRJc_re9jbvFLp1BtIHIDPOBf6k)![](https://lh5.googleusercontent.com/ZD583SsZZ407Tj_6xCRTdh6FoU9eQQt5CCbs3P2rVJzLhGFSj-RgmBqOvNS22sZZlFsNineUm2OqPVr693emLLIiOG8iZBd6tTAyDYkoqjiA_K-i1eqwfad-YK4fuEdyw3fkvcf8xXfSc85fW2lm_DQ)

  

If you lost your prompt and settings, there’s a tab called PNG info in A1111. Put your image in there and it should tell you the prompt and settings used to render the image.

![](https://lh4.googleusercontent.com/jbd5z8GbkpsqRSOBwHgCbEXRd2pd4gLvtX64OXTOJ7qal7ce5dOTL9qavwInhrTTcXl-ui773iq20hKWdGl5PIQYgGUNwIkEYSiFGLIvDwPdmZmQx0D9dAoOVh0F6nqqEDE2nQaHaY_ifQ3s6C5tsG4)

Once the new font is rendered, you could use [WhatTheFont](https://www.myfonts.com/pages/whatthefont) (An font identifying website)


This method is a bit of a gamble though since most of the fonts there are paid. Sometimes you can search for the font and a free version may come up if you’re lucky.