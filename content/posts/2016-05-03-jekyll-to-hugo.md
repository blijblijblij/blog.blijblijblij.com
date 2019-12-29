+++
date = "2016-05-03T16:13:59+02:00"
author = "Rogier Wessel"
comments = true
draft = false
image = "images/cover.jpg"
menu = ""
share = true
slug = "jekyll-to-hugo"
tags = ["meetup", "pentaho"]
title = "Jekyll boooh, hugo yeah!"
post = "/:year/:month/:day/:slug.html"

+++
Not that long ago I [migrated my blog to github pages](/post/2015-11-16-newblog) using  [Jekyll](https://jekyllrb.com/). Jekyll is a [static website generator](https://www.staticgen.com/). You write some intermediate [markdown](https://en.wikipedia.org/wiki/Markdown) pages, [cheat some markup](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet) and the generator will build the static website for you, rss feeds, navigation and the whole shebang included.

**BUT** the sm-meister that wrote Jekyll went through some hard, breaking and annoying changes. Probably very sound changes, but I want something that works, takes little effort to maintain, yet slightly more appealing than

```type=html
<!DOCTYPE html>
<html>
<body>

<h1>My First Post</h1>

<p>Epic story goes here...</p>

</body>
</html>
```

# Enter hugo

```
Hugo is great for content-driven websites, because it is completely dependency-free and is easy to get going. What it lacks for in extensibility, it largely makes up for with a good content model and super-fast build times.
```

Another quote I agree on

```
Hugo is quite possibly the easiest to install software you’ve ever used, simply download and run. Hugo doesn’t depend on administrative privileges, databases, runtimes, interpreters or external libraries. Sites built with Hugo can be deployed on S3, GitHub Pages, Dropbox or any web host.
```

I'll take it, after some hurdles migrated this blog into a Hugo-i-fied one, and yet again ready for blogging incontinence...

Some links:

- [article on the battle of the static site generators](https://www.smashingmagazine.com/2015/11/static-website-generators-jekyll-middleman-roots-hugo-review/)
- [download hugo](https://github.com/spf13/hugo/releases)
- [getting started](https://gohugo.io/overview/quickstart/)

Just my 2 cents, regards, Rogier
