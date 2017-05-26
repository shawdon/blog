+++
date = "2017-05-20T19:39:03+08:00"
draft = false
title = "Get Started with Hugo"

+++

[TOC]

# Create a new site

```shell
hugo new site <your-site-name>
```

The new directory `<your-site-name>` has the following layout:

```shell
blog
├── archetypes
├── config.toml
├── content
├── data
├── layouts
├── static
└── themes
```

# Choose a theme

```shell
git submodule add -b master https://github.com/zyro/hyde-x.git themes/hyde-x
```

# Configuration

```toml
baseURL = "https://shawdon.github.io/"
languageCode = "en-us"
title = "My New Hugo Site"
disqusShortname = "your_disqus_shortname" # Optional, enable Disqus integration
MetaDataFormat = "toml"
theme = "hyde-x"
paginate = 10

[author]
    name = "Shawdon"

[permalinks]
    # Optional. Change the permalink format for the 'post' content type.
    # The format shown here is the same one Jekyll/Octopress uses by default.
    post = "/blog/:year/:month/:day/:title/"

[taxonomies]
    # Optional. Use if you want tags and lists.
    category = "categories"

#
# All parameters below here are optional and can be mixed and matched.
#
[params]
    # If false display full article contents in blog index.
    # Otherwise show description and 'read on' link to individual blog post page.
    # Default (if omitted) is true.
    truncate = true

    # Used when a given page doesn't set its own.
    defaultDescription = "Your default page description"
    defaultKeywords = "your,default,page,keywords"

    # Hide estimated reading time for posts.
    # Default (if omitted) is false.
    hideReadingTime = false

    # Changes sidebar background and link/accent colours.
    # See below for more colour options.
    # This also works: "theme-base-08 layout-reverse", or just "layout-reverse".
    theme = ""

    # Select a syntax highight.
    # Check the static/css/highlight directory for options.
    highlight = "sunburst"

    # Optional additional custom CSS file URL, will override other styles.
    customCSS = ""

    # Displays under the author name in the sidebar, keep it short.
    # You can use markdown here.
    tagline = "Shut up and fuck the world."

    # Text for the top menu link, which goes the root URL for the site.
    # Default (if omitted) is "Blog".
    home = "Home"

    # Metadata used to drive integrations.
    googleAnalytics = "Your Google Analytics tracking code"
    gravatarHash = "MD5 hash of your Gravatar email address"

    # Sidebar social links, these must be full URLs.
    github = ""
    bitbucket = ""
    stackOverflow = ""
    linkedin = ""
    googleplus = ""
    facebook = ""
    twitter = ""
    youtube = ""

    # Other social-like sidebar links
    rss = false  # switch to true to enable RSS icon link
    flattr = ""  # populate with your flattr uid
```
# Add a post

```shell
hugo new post/<post-name>.<file-format>
```

The new post is here:

```shell
content
└── post
    └── get-started-with-hugo.md
```

# Server the site

```shell
hugo server -D -t=hyde-x
```

-D, --buildDrafts:                include content marked as draft

-t, --theme string:               theme to use (located in /themes/THEMENAME/)

Now the site is available at http://localhost:1313/ .

# Make posts public

```shell
hugo undraft content/post/<post-file>
```

# Generate website

```shell
hugo
```

After that, `public` directory will be created containing the generated website source.

# Deploy on GitHub Pages

```shell
rm -rf public
git submodule add -b master https://github.com/shawdon/shawdon.github.io.git public
hugo
cd public
git add .
git commit -m "deploy blog for the 1st time"
git push origin master
```

There is also a script to automate it:

```sh
#!/bin/bash

echo -e "\033[0;32mDeploying updates to GitHub...\033[0m"

echo "Build the site"
hugo # if using a theme, replace with `hugo -t <YOURTHEME>`

# Go To Public folder
cd public
# Add changes to git.
git add .

echo "Commit changes"
msg="rebuilding site `date`"
if [ $# -eq 1 ]
  then msg="$1"
fi
git commit -m "$msg"


echo "Push source and build repos"
git push origin master

# Come Back up to the Project Root
cd ..

echo "Deploy success"
```