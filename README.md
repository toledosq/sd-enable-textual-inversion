# sd-enable-textual-inversion
Copy these files to your stable-diffusion to enable text-inversion

any problems create an issue please

# You don't upload an image, that's not how it works

[textual-inversion](https://textual-inversion.github.io/) - An Image is Worth One Word: Personalizing Text-to-Image Generation using Textual Inversion (credit: Tel Aviv University, NVIDIA)

!()[https://textual-inversion.github.io/static/images/editing/teaser.JPG]

We learn to generate specific concepts, like personal objects or artistic styles, by describing them using new "words" in the embedding space of pre-trained text-to-image models. These can be used in new sentences, just like any other word.

!()[https://textual-inversion.github.io/static/images/editing/puppet.JPG]

You need to train embeddings then use the embedding file

Training data is the images of the thing you want to train on, apparently you only need 3-5 but best practices for choosing the images themselves are currently unknown afaik

One thing I have noticed when I tried training is that it resizes the image to 512 without respecting aspect ratio so you may want to 'outcrop' your image to a square, it appears backgrounds are 'filtered' out somehow and the central concept of the image picked up on

2 :cherries: examples :cherries: based on the embeddings in the sd-embeddings repo below:

![00254](https://user-images.githubusercontent.com/106811348/187011731-e0b0b48a-63c7-4ecc-81e6-104d1cb1e342.png)

![00184](https://user-images.githubusercontent.com/106811348/187011743-a4abd08e-2383-4207-95f5-c60f6d3183ba.png)

For training see:
[rinongal/textual_inversion](https://github.com/rinongal/textual_inversion)
[nicolai256/Stable-textual-inversion_win](https://github.com/nicolai256/Stable-textual-inversion_win)

Please note: training uses a HUGE amount of vram, you will struggle to get it working on <12gb vram, I have but only by changing the size: 512 to size: 448 in this section of v1-finetune or lowmemory version: 
```
data:
  target: main.DataModuleFromConfig
```

Alternatively you can test with an embedding from [here](https://github.com/hlky/sd-embeddings)
There are 2 available atm, see the readme.md of each one for more info i.e. amount of images in training dataset, steps trained
Note: they are not very good, more and better embeddings needed for the [sd-embeddings](https://github.com/hlky/sd-embeddings) repo

You use * in the prompt where you want the custom trained thing. Note: requires PHD in prompt crafting and messing around with sampler, steps, cfg, the prompt itself, to get anything resembling a good result (possibly caused by rubbish images used for training as well)
