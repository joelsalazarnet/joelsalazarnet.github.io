---
layout: post
title:  "Build Jekyll and GitHub Pages using a Docker Container"
date:   2024-03-20 23:00
categories: coding
---
Unleash the power of Docker for a hassle-free Jekyll blog setup and deployment to GitHub Pages. This technical guide will cover the essentials of using Docker containers to streamline your development workflow, ensuring a smooth transition from local development to live publication. Let’s get started! 🚀

First, let’s put together a Docker file to build an image with everything we need.

{% highlight docker %}
  # Dockerfile for Jekyll using Ubuntu
  FROM ubuntu:latest

  # Install necessary packages
  RUN apt-get update && \
      apt-get install -y ruby-full build-essential zlib1g-dev git

  # Install Jekyll and Bundler
  RUN gem install bundler jekyll

  # Set the working directory inside the container
  WORKDIR /srv/jekyll
{% endhighlight %}

Proceed to build the image using the command `docker build -t jekyll-ubuntu .` and lets execute the following commands:

{% highlight shell %}
  docker run --rm -it -p 4000:4000 -p 35729:35729 -v ghpages:/srv/jekyll jekyll-ubuntu bash
  jekyll new .
  bundle exec jekyll serve --host 0.0.0.0 --livereload
{% endhighlight %}

If you already have an existing volume, then you will have to use `bundle install` instead of `jekyll new .`

Finally, simply connect to the container via Visual Studio Code and designate the `/srv/jekyll` directory as your workspace to begin crafting your Jekyll site.