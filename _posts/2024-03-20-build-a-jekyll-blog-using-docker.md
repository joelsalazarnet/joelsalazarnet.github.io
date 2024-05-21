---
layout: post
title:  "Build a Jekyll blog using Docker"
date:   2024-03-20 00:00
categories: coding
---
Unleash the power of Docker for a hassle-free Jekyll blog setup and deployment. This technical guide will cover the essentials of using Docker containers to streamline your development workflow, ensuring a smooth transition from local development to live publication. Let’s get started! 🚀
<!--more-->

First, let’s create a "dockerfile" with the necessary instructions to build our image.

{% highlight docker %}
  # Dockerfile for Jekyll using Ubuntu
  FROM ubuntu:latest
  # Install necessary packages
  RUN apt-get update && \
      apt-get install -y ruby-full build-essential zlib1g-dev git && \
      git config --global init.defaultBranch main
  # Install Jekyll and Bundler
  RUN gem install bundler jekyll
  # Set the working directory inside the container
  WORKDIR /srv/jekyll
{% endhighlight %}

Proceed to build the image "jekyll-ubuntu" using the command `> docker build -t jekyll-ubuntu .`

Run a container, mount the volume "ghpages", and execute a "bash" terminal using this command

{% highlight docker %}
  > docker run --rm -it -p 4000:4000 -p 35729:35729 -v ghpages:/srv/jekyll jekyll-ubuntu bash
{% endhighlight %}

Create a new jekyll site, then launch the local server 

{% highlight shell %}
  $ jekyll new .
  $ bundle exec jekyll serve --host 0.0.0.0 --livereload
{% endhighlight %}

If you already have an existing volume with a jekyll site, use `bundle install` instead of `jekyll new .` then launch the server

Finally, simply connect to the container via Visual Studio Code and designate "/srv/jekyll" as your workspace to begin crafting your Jekyll blog.