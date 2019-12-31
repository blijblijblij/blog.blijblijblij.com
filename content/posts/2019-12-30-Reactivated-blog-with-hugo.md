---
title: "Reactivated Blog With Hugo"
date: 2019-12-30T20:08:15+01:00
author: "Rogier Wessel"
tags: ["blog", "hugo"]
draft: false
---
Somehow over time bitrot appeared in my [Hugo](https://gohugo.io/) setup. Files where ok 
for a very old version, but config changes no longer followed the newer 
conventions as suggested by Hugo. Also my carefully adapted
theme had fallen to pieces and didn't render no more, so 
[kiss theme](https://themes.gohugo.io/kiss/) to the rescue!

Also automation happened and we now have [Github Actions](https://github.com/features/actions) which is a 
perfect solution to build and deploy Hugo pages to [GitHub Pages](https://pages.github.com/). 

Github-pages is an excellent service
supporting the hosting of static websites, ssl included, also 
[custom domain names are supported](https://help.github.com/en/github/working-with-github-pages/about-custom-domains-and-github-pages) allowing me to host via Github
Pages but on my own domain [https://blog.blijblijblij.com](https://blog.blijblijblij.com).

![Git settings](/images/2019-12-30-git-settings.png "Git settings")

This config (as described by
[peaceiris/actions-hugo
](https://github.com/peaceiris/actions-hugo)) should get you going:

```yaml
name: Push to GitHub Pages on push to master
on:
  push:
    branches:
      - master
jobs:
  build-deploy:
    runs-on: ubuntu-18.04
    steps:
    - uses: actions/checkout@v1
      with:
        submodules: true

    - name: Setup Hugo
      uses: peaceiris/actions-hugo@v2
      with:
        hugo-version: 'latest'

    - name: Build
      run: hugo --minify

    - name: Deploy
      uses: peaceiris/actions-gh-pages@v2
      env:
        ACTIONS_DEPLOY_KEY: ${{ secrets.ACTIONS_DEPLOY_KEY }}
        PUBLISH_BRANCH: gh-pages
        PUBLISH_DIR: ./public
```

But more information can be found on this [peaceiris/actions-hugo
](https://github.com/peaceiris/actions-hugo) page.
