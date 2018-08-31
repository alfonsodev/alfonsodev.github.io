---
layout: post
title:  "How to build and publish static websites with Jekyll and Github pages."
date:   2018-08-31 11:45:00
categories: jekyll blog static 
---

# How to build and publish static websites with Jekyll and Github pages.
Github supports [Jekill](https://jekyllrb.com) a static website generator.
The concrete versions that github uses are described in [this link](https://pages.github.com/versions/), but if we browse to the bottom we can see that the easiet way is to install [github-page gem](https://rubygems.org/gems/github-pages) which contains all the needed depenecies.  

## Preparation
- we need to install rbenv
- create an empty folder
- cd folder/
- rbenv local 2.5.1

This will create a .ruby-version file, so everytime we move to this directory rbenv looks for this file and changes the ruby version.

we can check it with 
```
ruby -v
``` 

## Gemfile
In the gemfile we must define the `source` to tell bundler where to find the gems.  
We can define the version of ruby that we are using and the depenency.
```
source "https://rubygems.org"
ruby '2.5.1'
gem 'github-pages', '~> 191'
```
We can save the file and run `bundler install`.   
A new file Gemfile.lock will be created, we never have to edit this file manually.  

## The jekill project sctructure.  
We need to understand that "Jekyll is, at its core, a text transformation engine" 
Here is [jekill's folder structure](https://jekyllrb.com/docs/structure/)
But before we jump into creating all this structure let's have a look to the configuration file so we can define wher we want to have the folders. Specially the source and destionation parameters.

## Configuration
[Here is the documentation for the configuration file](https://jekyllrb.com/docs/configuration/), to see a real world example we can visit [the boostrap project config file](https://github.com/twbs/bootstrap/blob/v4-dev/_config.yml), yes! https://getbootstrap.com is fueled by jekill and hosted in github pages!. This will be very useful to learn.

Let's go ahead and create a new file `_config.yml` the first parameteres we are inteerested are `source` and `destination` 
```
source:         "site"
destination:    ./_gh_pages
```
destination is specially important because is what makes the magic. 

## Git
There are some files that we don't need to commit. 

```
.gitignore
```
This is a good start
```
.DS_Store
/_gh_pages
Gemfile.lock
.sass-cache
.env
.jekyll-metadata
tmp/
```

# Creating content
let's start by creating two things 
the default layout and the index.html file
we can copy [this example index file](https://github.com/jekyll/example/blob/gh-pages/index.html)
But let's make it even simpler 
on index.html we'll add just.  

on site/index.html
```
---
layout: default
---
<div class="home">
  <h1 class="page-heading">home</h1>
</div>
```
on site/_layouts
```
<!DOCTYPE html>
<html>
  <body>
    <div class="page-content">
      <div class="wrapper">
        {{ content }}
      </div>
    </div>
  </body>
</html>
```
