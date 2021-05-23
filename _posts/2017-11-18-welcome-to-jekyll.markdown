---
layout: post
title:  "How to build websites on GitHub Pages with jekyll?"
date:   2017-11-18 11:39:58 +0300
categories: jekyll update
---

Hi Everyone,

Today, I want to share my experience about building websites on **Github Pages** with **jekyll**. Actually, I have a website on Wordpress in Turkish. But also I wanted to build another one in English to improve my English writing skill and make my contents public not local. And then, I searched for platform for my website. I didn't want to use Wordpress again because I experienced it. So I decided to try another one.While I was searching, I found GitHub Pages. It gives you free hosting for your website or project website from your repository.That's perfect !. So I decided to build my website with GitHub Pages.And I learned Github Pages support a thing named jekyll. I didn't know what "jekyll" is . After a quick search, I learned `"jekyll" is a blog-aware, static site generator in Ruby`. Wait What? What is the meaning of `blog-aware` and `static site generator`? So first, let's learn these terms.

### Blog-aware?

`One of Jekyll’s best aspects is that it is “blog aware”. What does this mean, exactly? Well, simply put, it means that blogging is baked into Jekyll’s functionality. If you write articles and publish them online, you can publish and maintain a blog simply by managing a folder of text-files on your computer. Compared to the hassle of configuring and maintaining databases and web-based CMS systems, this will be a welcome change!`

Definition from jekyll official [website](https://jekyllrb.com/docs/posts/)

### Static site generator?

`A static site generator takes source files and generates an entirely static website.` from quite easy to understand content on [here](https://learn.cloudcannon.com/jekyll/why-use-a-static-site-generator/) and also there are videos about it.

After these terms, we can start building our website but we need to download first **Ruby** and then **Bundler**.
You can download **Ruby** from [here](https://www.ruby-lang.org/en/downloads/) and download bundler like below.

`"gem install jekyll bundler"`

After that, we need to create a repository for our website files. You can do it easily with `git init reponame` command in any path.Then, we need to install `Jekyll`. We can do it with `bundler` that downloaded before but we need to create a file named `Gemfile` and then we need to add these two lines in it. 

![Screenshot2]({{ "/assets/screenshot4.png" | absolute_url }})

Now, we can download `Jekyll` and its dependencies based on our `Gemfile` content like below.

![Screenshot3]({{ "/assets/screenshot5.png" | absolute_url }})

Okay, now we did all things before the create our website contents.All things are okay.

Now we need to create some files and fill in these files because if you remember `Jekyll` is a static-site generator that means we will give some files to `Jekyll` and then our website will be created based on these files. These files and `Jekyll` file structure is explained in [here](https://jekyllrb.com/docs/structure/).So, we need to create all them step by step but I will not show them all. At the end you are suppose to have a repository like below. These files also this website's files.

![Screenshot4]({{ "/assets/screenshot6.png" | absolute_url }})

A much more nice screenshot from official site is below. In my case I didn't use all of files because I didn't need them all. But it may necessary in your case. Before you start building your website. You should define your requirements first.

![Screenshot5]({{ "/assets/screenshot7.png" | absolute_url }})

And also, If you want to know each files role in website you can learn from [here](https://jekyllrb.com/docs/structure/). It is well explained and clear.



### Publishing The Website

If you want to publish your website on The Internet. Just upload your files in a repository that named **username.github.io**. And `GitHub` will do the rest. After some time, you can check your website from **username.github.io**. For example, this website's repository on my GitHub account you can find [here](https://github.com/koksalmis/koksalmis.github.io)


### Conclusion
`Jekyll` was a litte bit difficult for me because I had no idea "What is static site generator?" and "What is Jekyll?". And also `Jekyll` was a litte bit complex because there are many files and hard to build in locally not like classic(HTML,CSS,Javascript). But after understanding structure of `Jekyll` and how it makes easier things, For example publishing posts in `Jekyll`.You don't need to write same HMTL code everytime for your each post and like it.

These my thoughts and experience about `Github Pages` and `Jekyll`.

Thank you

Enes Köksalmış 
