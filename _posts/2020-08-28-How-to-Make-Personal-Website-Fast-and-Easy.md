---
layout: post
title: How to Make Personal Website Fast and Easy 
subtitle: Using GitHub Pages and Beautiful Jekyll 
cover-img: /assets/img/cover_pic_website.jpg
thumbnail-img: /assets/img/website_image.png
tags: [website, GitHub]
---

A personal website is a great tool to showcase your projects and blog about topics that you are passionate about. Unfortunately, there is a misconception that making a personal website is a painful, time-consuming, and costly process. Consequently, this prevents many talented people from sharing their scientific/art projects with employers and the world. This tutorial proves the opposite, guiding you step by step on how to create a free and elegant website (like this one) in hours if not minutes!  Without further ado, let's get started.

**Key ingridients**: GitHub, Beaitiful Jekyll, and your creativity. 

## Step I: Open GitHub Account 
If you don' have one, you wil need to sign up [here](https://github.com/). GitHub is a free version control tool that let you host one static website through GitHub Pages, which will be used for this tutorial. 

## Step II: Fork Beautiful-Jekyll Repository (repo)
Fork [Beautiful-Jekyll project](https://github.com/daattali/beautiful-jekyll/) by clicking on *Fork* as shown below: 

![fork](/assets/img/fork.jpeg) 

Once you have this repo, you will have all it needs to make a simple yet elegant website. 

## Step III: Rename your repository 
The next step is to rename the forked repo from Beautiful-Jekyll to **yourusername.github.io** . For this, you need to click on setting and rename the repo as shown below:
  
![setting](/assets/img/settings.png)
  
This will create a website with the Beautiful-Jekyll template with the following address: `<https://yourusername.github.io]>`. 

⚠️ Please note that you need to use your GitHub username when renaming the forked repo. If you don't, you will end up having a long website name. For example, if you name your repository as **mycoolproject/github.io** , you will get this long address: `<https://yourusername.github.io/mycoolproject/github.io>` -- believe me, it's not pleasing to the eye. 

⚠️ Also, if you have an issue opening your website (like I did), this [video](https://www.youtube.com/watch?v=BA_c3bGQXlQ) might solve your problem. 

## Step IV: Customize your website 

Congratulations! You've just created your own website. Indeed, it was not that bad. Now, you just need to customize it. 

#### 1) `_config.yml`

Open `_config.yml` file in the repository and make all the relevant changes to the default settings. To make the changes, click on the *pencil* icon displayed at the top right corner. The settings are mostly self-explanatory and should not be hard to follow. Once you are done, press *commit* button, and the website will be updated within a few minutes. 

For example, you may want to personalize the colors of your website: 
Here are the default colors: 

![colors](/assets/img/colors.png) 

💡 When choosing colors for your website, I found this [article](https://visme.co/blog/website-color-schemes/) helpful. Also, you can make your own color using [this](https://www.google.com/search?q=color+picker) color picker. 

#### 2) `aboutme.md` and `index.html` 

Next, change the title and text in `aboutme.md` and `index.html` documents found in your project repo. The text in `aboutme.md` file will be displayed in  *About me* section of your website, while text in `index.html` is displayed on the home page. 

#### 2) `_posts`

Lastly, to add your posts, go to `_posts` folder in your repo. You will see two posts there, which you can remove. 

❗ It's important to note that your posts should be in **Markdown** format. It implies that it needs to satisfy the following 3 properties: 

   - Starts with the date (2020-08-28)
   - Ends with `.md`
   - Words of the name are separated with `-`

For example, if you look at the address of this page,  you can see that the name of this post is `2020-08-28-How-to-Make-Personal-Website-Fast-and-Easy.md`. To leran more about the basics of Markdown, check [here](2020-08-28-How-to-Make-Personal-Website-Fast-and-Easy.md). 

Now, that you know about the right format of the post, it's time to create one! To do so, you need to click on `Add File --> Upload` files and name the post in the **'year-m-d-the-name-of-file.md'** format. 

Finally, if you wondered where I got emoji, here is the [the website](https://emojipedia.org/exclamation-mark/) I used.

## Step V: Relax and enjoy your website! 🎉🎈🎊
You did it!


For more information on the GitHub pages website with Jekyll, please check [here](https://github.com/daattali/beautiful-jekyll). 

[Reference](https://github.com/daattali/beautiful-jekyll)
