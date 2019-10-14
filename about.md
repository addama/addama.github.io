---
layout: default
title: "Xtract Solutions Documentation | About"
permalink: /about/
---

# Welcome to Documentation Land

## Installation

**For normal interactions with the site, you don't need to install anything** - but if you need to change the layout or want to test your checklist locally, you'll need to set up your environment.

The site runs on github-pages, which interprets pages using Jekyll and Liquid. So, so run this locally, we need to set that up.

1. [Install Ruby](https://www.ruby-lang.org/en/downloads/)
1. Clone the repo
1. Navigate to your repo directory
1. Open a console and run the following commands:
  - Install Bundler and Jekyll gems: `gem install bundler jekyll`
  - Run the Jekyll server: `bundler exec jekyll serve`
1. Navigate to `localhost:4000`

You can now make changes to your local version and watch the changes live(-ish) in your browser.

## Adding New Documents

This site is [post](https://jekyllrb.com/docs/posts/)-based, which means that we are leveraging Jekyll's internal handling of `_posts` to organize and display the documents.

You can either add documents inside your cloned repo, or directly from the Github interface. The only difference is that if you have cloned the repo, you will need to commit and push/create pull request, whereas the Github UI handles that stuff for you on a transactional basis.

To add a new document:
1. Navigate to `/_posts`
1. Create a new file with the filename `{YYYY}-{MM}-{DD}-{Title}.md`, where:
  - `{YYYY}` is the 4 digit year
  - `{MM}` is the 1-2 digit month (can have leading 0 or not)
  - `{DD}` is the 1-2 digit day (can have leading 0 or not)
  - `{Title}` is the title. The title can have spaces, as Jekyll slugifies the titles, but for operating system safety, it's best to use underscores or dashes between words.
1. Open your file
1. Add the following [front matter](https://jekyllrb.com/docs/front-matter/) to the top of the file:
```md
---
title: 
author: 
categories: []
excerpt: 
---
```
1. Edit the front matter to include a `title`, `author`, `categories`, and `excerpt`. These properties are mandatory for order and sanity to prevail - don't be the loser that doesn't fill them out!
  - You may wish to look at the main listing to see what categories already exist
1. Commit your document
  - Github Pages only allows up to 10 new builds per hour, and it generally takes between 10 and 60 seconds to build a new version. If your changes don't appear immediately, this may be why.

## Site-wide Config Changes

You can change overarching info about the site in the `/_config.yml` file.

You can change the syntax highlighting color scheme by editing the `/css/default.css` file, and changing the `@import` line to point to a different CSS file in `/css/syntax`. By default, I have included *fruity*, *github*, *monokai*, *native*, *zenburn*, and our own branded style, *xtract*.

You can change the font by adding the font to `/css/fonts`, and adding it to `/css/default.css` as a new font face (or edit the existing entry, just remember to change the name). The default font used is *Raleway*.

The header and footer on all of the pages can be found in `/_includes`. Be aware that changing these will change the look and feel of ALL pages, as all pages are currently using the `default` layout, which loads the header and footer. You can use Liquid to make decisions based on what page you're on to do page-specific things. But, like, don't do that, please. Simple is better.

You can add images to `/images`. Feel free to create subdirectories under that if that makes organization/naming easier.

## Resources
* [Ruby](https://www.ruby-lang.org/en/)
* [Bundler](https://bundler.io/)
* [Jekyll](https://jekyllrb.com/)
* [Liquid](https://shopify.github.io/liquid/)
* [Github Pages](https://pages.github.com/)
* [Markdown (for Github)](https://guides.github.com/features/mastering-markdown/)
* [Ruby Gems available by default on Github Pages](https://pages.github.com/versions/)