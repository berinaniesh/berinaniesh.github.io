+++
title = "Bible Web 2"
date = 2023-10-06
draft = false
+++

Git Repo: [Link](https://gitlab.com/scripture/scripture.gitlab.io)

Deployed at: [Link](https://scripture.berinaniesh.xyz)

This is an alternate frontend to the [bible-api](/projects/bible-api/) in which everything is generated prior and the whole site is served as static content. 

The objective here is to provide a featureful and book like reading experience. Though the site is not as fast as [Bible Web 1](/projects/bible-web-1/) (which is due to prefetching and fetching on hover) the site is still very fast, responsive and serves it's purpose well. 

## Generation Process

The site uses [mdbook](https://rust-lang.github.io/mdBook/index.html), which is a static site generator written in rust by the rust team themselves. It is fast, minimal, extendable and featureful.

The problem is that `mdbook` requires each page to be typed out in their `SUMMARY.md`. There are 1189 chapters in a standard bible and the UI serves four bibles (right now), which amounts to 4756 generated pages.

So, we used a python script, which fetches verses from the [Bible API](/projects/bible-api/) and constructs a [tree](https://en.wikipedia.org/wiki/Tree_(data_structure)). This tree is serialized to markdown files and mdbook then generates html and css for the generated markdown files. 
The script can be found [here](https://gitlab.com/scripture/scripture.gitlab.io/-/blob/generation_branch/generator.py?ref_type=heads).

## Hurdles

There are a total of 4758 pages and we hit limits on various stages. 
1. `mdbook` is not designed to write this many pages. It rerenders the whole book on a single thread with each change. This of course is problematic and so, the generated code and the generation scripts are at separate branches. 
2. `mdbook` running on GitLab CI, due to some unknown reason (probably memory/storage/cpu limitations), won't generate any content on pages since the number of bibles reached 2. So, we moved everything to local build and hosting. 
3. GitLab has a limit on the size of the repo that can be hosted on Gitlab Pages. So, this is hosted on a linux server (which made the app load much faster).
