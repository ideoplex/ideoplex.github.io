---
layout: post
title:  "Upload your blog to GetHub Pages"
date:   2014-05-14 06:44:27
categories: jekyll
---
Create a github repository names ***username***.github.io, where ***username*** is your GitHub username as described in the [Github Pages](https://pages.github.com) documentation.

Create a new jekyll blog on your local machine

```
sites/jekyll 1 $ jekyll new github.pages
New jekyll site installed in /Projects/sites/jekyll/github.pages. 
```

Initialize your jekyll configuration. Note that I've added support for Git Flavored Markdown in the kramdown configuration.

```
sites/jekyll 2 $ cd github.pages
jekyll/github.pages 3 $ vi _config.yml
jekyll/github.pages 4 $ cat _config.yml
# Site settings
title: Getting Started with Jekyll
email: 
description: "Sample Jekyll blog hosted on GitHub pages"
baseurl: ""
url: http://ideoplex.github.io

# Build settings
markdown:
 kramdown
kramdown:
 input: GFM
permalink: pretty
```

Delete the default first post created by jekyll

```
jekyll/github.pages 5 $ rm _posts/201?-??-??-welcome-to-jekyll.markdown
```

Create your own first post. My first post contains these instructions.

```
jekyll/github.pages 6 $ vi _posts/2014-05-14-upload-to-github-pages.md
```

Add a README.me

```
jekyll/github.pages 7 $ echo '#Deploy a Jekyll blog to GitHub pages

Example of a Jekyll blog deployed on GitHub pages' > README.md
```

Initialize your local git repository:

```
jekyll/github.pages 8 $ git init
Initialized empty Git repository in /Projects/sites/jekyll/github.pages/.git/
```

Add everything and make your first commit

```
jekyll/github.pages 9 $ git add --all
jekyll/github.pages 10 $ git commit -m "first commit"
[master (root-commit) 223ac2c] first commit
 14 files changed, 710 insertions(+)
 create mode 100644 .gitignore
 create mode 100644 README.md
 create mode 100644 _config.yml
 create mode 100644 _includes/footer.html
 create mode 100644 _includes/head.html
 create mode 100644 _includes/header.html
 create mode 100644 _layouts/default.html
 create mode 100644 _layouts/page.html
 create mode 100644 _layouts/post.html
 create mode 100644 _posts/2014-05-14-upload-to-github-pages.md
 create mode 100644 about.md
 create mode 100644 css/main.css
 create mode 100644 feed.xml
 create mode 100644 index.html
```

Set your github pages repository as the remote, and push

```
jekyll/github.pages 11 $ git remote add origin https://github.com/ideoplex/ideoplex.github.io.git
jekyll/github.pages 12 $ git push -u origin master
Counting objects: 20, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (18/18), done.
Writing objects: 100% (20/20), 7.82 KiB | 0 bytes/s, done.
Total 20 (delta 1), reused 0 (delta 0)
To https://github.com/ideoplex/ideoplex.github.io.git
 * [new branch]      master -> master
Branch master set up to track remote branch master from origin.

```

Congratulations, your blog will shortly be available on GitHub pages.
