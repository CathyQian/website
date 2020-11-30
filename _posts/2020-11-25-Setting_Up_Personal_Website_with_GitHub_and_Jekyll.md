---
layout: post
title: Setting Up Personal Website with GitHub and Jekyll
description: A brief tutorial on how to set up personal website with GithHub and Jekyll
date: 2020-11-25
tags: marketing, Jekyll, GitHub
comments_id: 22
---

Both GitHub and Jekyll has detailed documentation on how to set up a personal website, however, it can still be quite a time-consuming process. This article aims to provide a concise step-by-step tutorial on how to set up a basic website from ground zero. Once you master the basics, life will be much easier.

Assuming you are using Windows 10 OS, having a GitHub account and have installed Git Bash already, below are steps you need to follow to set up a personal website:

1) Download and install Ruby [here](https://rubyinstaller.org/downloads/). The **Ruby+Devkit 2.7.X (x64)** installer is preferred.

2) Install bundle following the instructions [here](https://bundler.io/). Briefly, open a terminal window and run the following command:

    $ gem install bundler
    

3) Install Jekyll by running the following command in the same terminal window:

    $ gem install jekyll
    
You can check the version of the installed jekyll by running the following command in the terminal window:

    $ jekyll -v


4) Create a new Jekyll site as follows: open Git Bash, go to the folder where you want to place the GitHub repository for your website, then type in the following command:

    $ jekyll new myblog

A bunch of new files will be created in the **myblog** folder, including a *Gemfile*, a *_posts* folder and a *_config.yml* file.

5) Open the newly created *Gemfile*, change this line

    Gem "github-pages" xxxx

into 

    gem "github-pages", "~> 4.1.1", group: :jekyll_plugins

Then save and close the *Gemfile*.

6) So far, you have set up the backbones of your website. You can test your site locally by going to the **myblog** folder and run the following command in the same terminal window:

    bundle exec jekyll serve

Now you can browse to http://localhost:4000 to check your website. It has no personalized content yet.

7) Check in the **myblog** folder into GitHub following instructions [here](https://docs.github.com/en/free-pro-team@latest/github/working-with-github-pages/creating-a-github-pages-site-with-jekyll).

8) Go to the GitHub repository, go to **Settings**, then you will find the published site URL under GitHub page, as follows:

[<img src="/assets/2020-11-25-17-13-32.png" width="650"/>](/assets/2020-11-25-17-13-32.png)

9) Now comes to the customization part, which includes 
- add content 
- [customize theme](https://docs.github.com/en/free-pro-team@latest/github/working-with-github-pages/adding-a-theme-to-your-github-pages-site-using-jekyll)
- [customize Jekyll template](https://github.com/jekyll/minima#customizing-templates) (copy this correspoding HTML or CSS files into the designated folder, then modify them directly)
- [customize website domain name](https://docs.github.com/en/free-pro-team@latest/github/working-with-github-pages/managing-a-custom-domain-for-your-github-pages-site#configuring-a-subdomain)
- [customize skin color](https://github.com/jekyll/minima#skins) (not working now, wait for minima theme updates before trying to change skin color)
- [enable comments](https://desiredpersona.com/disqus-comments-jekyll/)

10) Let's elaborate a bit on how to add content to the website, as it's probably the most important part of setting up a personal website.

The *_post* folder is where your blog lives. You typically write posts in Markdown. To create a post, add a file to your *_posts* folder with the following format:
    
    YEAR-MONTH-DAY-title.MARKDOWN
    # i.e.,
    2020-11-24-summary_about_Jenkens.md
    2020-11-24-summary_about_Jenkens.markdown
    
The blog files must begin with **front matter** which is used to set a layout or other meta data. Refer [here](https://jekyllrb.com/docs/posts/) about the details of the blog post files.

Different from posts, pages are useful for standalone content that is not date based or not a group of content. The simpliest way to create a page is to create a markdown file under the root directory. For example, in your homepage, you want to have  the following pages:

[<img src="/assets/2020-11-26-08-45-21.png" width="500"/>](/assets/2020-11-26-08-45-21.png)

What you need to do is to create the following files under the root directory:
     
[<img src="/assets/2020-11-26-08-47-34.png" width="150"/>](/assets/2020-11-26-08-47-34.png)

Then add the following snippets into the **_config.yml** file:

    header_pages:
    - about.md
    - techblogs.md
    - readings.md
    - resume.md
    - misc.md
    - archieves.md
