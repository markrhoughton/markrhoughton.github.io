---
title: "Getting Up and Running"
date: 2022-08-26T17:34:56+01:00
draft: false
tags:
    - hugo
---

This site was made using Hugo, which has lowered the barrier to entry for me running my own blog. 

Every time I want to create a new post, I can just run
```
hugo new some-new-post.md
```
from the root directory of this repo.

For a local server instance I run 
```
hugo server -D
```
where the `-D` flag sets drafts to true, meaning I can view any posts that are still marked as drafts.

For more info on getting started with Hugo, see the [quick start](https://gohugo.io/getting-started/quick-start/) for details.
