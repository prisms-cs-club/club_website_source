---
title: Club Website Contribution Guidelines
date: 
updated:
tags:
- Hexo
- Website
categories:
- Documentation
keywords: 
description:
top_img: 'linear-gradient(to right, #2c3e50, #4ca1af)'
comments:
cover: /img/PRCS_Logo.png
toc: true 
toc_number: true
toc_style_simple:
copyright:
copyright_author: Tony Zhao
copyright_author_href: https://ttzytt.com
copyright_url:  
copyright_info:
mathjax: false
katex: true
aplayer:
highlight_shrink:
aside:
---

## Configuration of Development Environment

This website is built based on the frame work of [Hexo](https://hexo.io/), a static website generator. The theme we used is [Butterfly](https://butterfly.js.org/en/).

### Install Node.js

Hexo is based on Node.js, so we need to install Node.js first. You can download the installer from [Node.js official website](https://nodejs.org/en/). Either the LTS version or the latest version will be fine.

To check if you installed Node.js successfully, you can run the following command in your terminal:

```bash
node -v
```

If runned this command successfully with something printed out in the terminal, this means you have installed Node.js.


### Cloning the Source Code Repository 

The website have two repositories, the first one is the source code repository, which is the one you are reading now. We use this repository to sync modifications from different club members. The second one is the deployment repository, which contained all html/css/js files for github pages to deploy.

Since the source code repository contains submodules (the theme we used), it need tobe cloned in a resursive way like this:

```bash
git clone --recursive -j8 https://github.com/prisms-cs-club/club_website_source.git
```

### Install Hexo and Other Dependencies

After cloned the source code repository, use `cd` command to enter the directory of the repository, and run the following commands to install Hexo and other dependencies:

```bash
npm install --force
```
 
Running this commend will let npm install all the dependencies listed in `package.json` file. The `--force` option is used to force npm to reinstall all the dependencies, which is useful when you want to update the dependencies to the latest version.

If this did not work you might want to clear the cache by running:

```bash
npm cache clean --force
```

Then run the previous command again.

### Run the Website Locally

To verify if your environment is configured properly and the website can be built successfully, you can run the following command to start a local server (on the directory of the source code repository):

```bash
hexo clean    # clean the cache
hexo generate # render markdown files into html files
hexo server   # start the server in local machine
```

This series of command can also be simplified as:

```bash
hexo cl
hexo g 
hexo s
```

The default port for locally generated hexo website is `4000`, so you can visit the website by entering `localhost:4000` in your browser.


## Writing a New Post

### Creating a New File

Every hexo pages are rendered from markdown files, and for the same reason, we need to create a new markdown file for each new post.

To create a new post, you should add a markdown file in `/source/_posts` folder, all markdown file should be ended with the suffix of `.md`.

The name of the markdown file will be used as the url of the post, so you should name the file properly. That is to say the filename should act as a good indication of the content while keeping a short length. For example, the title of this post is "Club Website Contribution Guidelines", so the filename is `website_guidelines.md` to ensure it tells the reader what the post is about while keeping a shorter length.

Notice to separate words in the filename, we use `_` instead of `-` or other method, this is just a convention we use in this website.

Another important point is not to start the filename with `_`, hexo will ignore any files starting with this (including video, images, etc.).

### Front Matter 

The front matter is a section of the markdown file that contains some meta information of the post. It is surrounded by `---` at the beginning and the end of the section. We'll learn how to write the front matter using the example of this post.

```yml
---
title: Club Website Contribution Guidelines
date: 2023-10-16 # the date when this post is first published
updated:         # the latest date when this post is updated, you do not need to fill this field, it will be 
                 # automatically filled by hexo if you run the command `hexo g`
tags:            # tags of this post, these are more specific topics that this post is about.
- Hexo           
- Website
categories:      # categories of this post, this is the "form" of the post. For example, manim notes are 
- Documentation  # categorized in "lecture notes"
keywords:        # don't need to care about this
description:     # Brief description of this post, if left empty, will use the first ~20 words
top_img: 'linear-gradient(to right, #2c3e50, #4ca1af)' # top banner image, if you don't have something in your 
                                                       # mind, just use this one
comments:        # whether to enable comments for this post (default true)
cover: /img/PRCS_Logo.png # the cover image of this post, if you don't have one, leave it false
toc: true        # whether to show the table of content (default true)
toc_number: true # whether to show the number of each section in the table of content (default false)
toc_style_simple:
copyright: true  # whether to display the copyright information section at the end of the post (default true)
copyright_author: Tony Zhao 
copyright_author_href: https://ttzytt.com # The link when clicking the author's name at the end of the post
                                          # This could be author's personal website, github account, etc.
copyright_url:   # If this post is transfered from another website, you can put the original URL here
copyright_info:  # The default copyright license we're using is CC BY-NC-SA 4.0, if you have some extra things
                 # put it here
mathjax: false   # do not change this
katex: true      # do not change this
aplayer:         # don't need to care about this
highlight_shrink: # if codeblocks are too long, you can set this to true to shrink it when exceeding to max height.
aside:           # don't need to care about this
---
```

### Formats 

#### Markdown 

Hexo posts should be written in Markdown format, and the in detailed documentation could be found at <https://www.markdownguide.org/cheat-sheet/> (most of the extended features are supported, but make sure the rendered post is as expected before publishing it).

#### Math Equations

If you want to insert block math equations, you should insert latex code between `$$` and `$$` like this:

```latex
$$
x^2 + y^2 = r^2
$$
```

And it renders as follows:

$$
x^2 + y^2 = r^2
$$

For inserting inline math equations, you should insert latex code between `$` and `$` like this:

```latex
The equation $x^2 + y^2 = r^2$ is the equation of a circle.
```

And it renders as follows: The equation $x^2 + y^2 = r^2$ is the equation of a circle.

All supported latex syntax could be found at <https://katex.org/docs/support_table>

#### Extended Features

Notice that hexo and the bufferfly theme support many extra features that are useful but are not included in the markdown standard, you can find the documentation of these features at <https://butterfly.js.org/en/posts/butterfly-docs-en-theme-config-one/#Tag-Plugins>, and <https://whatsid.me/2019/08/21/hexo-markdown-syntax/>.


### Images and Videos

Specifically for images and videos, the way to insert them might be a little different from usual. In markdown files, images are inserted in the following way: 

#### Images 

```markdown
![image description](image url)
```

And here the image url is not the absolute path in your own computer but the relative path in the website. For all images, you should put them in the `/source/img` folder. And then when you use the url, you should delete the `/source` part. For example, logo of the website is stored as `/source/img/PRCS_logo.png`, and the url for this image is `/img/PRCS_logo.png`. If I write `![](/img/PRCS_logo.png)`, I will have the image successfully inserted:

![](/img/PRCS_logo.png)

#### Videos

For videos, use the following format: 

```
{% raw %}
<video src=path_to_the_video type='video/mp4' controls='controls' width='100%' height='100%'/></video>
{% endraw%}
```

Here the `{% raw %}` and `{% endraw%}` are used to indicate that these lines are not markdown code, but raw html code. The `path_to_the_video` works as the same way as the image url (relative path that does not contain `/source`). And you should put all videos also in `/source/src` folder.


### Contributing to the Website

After you have finished writing the post and contacted with the two club leaders (tony.zhao@prismsus.org, tom.geng@prismsus.org), you can commit the changes to the source code repository.

```bash 
git add . # let git start to track the new files you have added
git commit -am what_you_have_done # commit the changes
git push
```

Notice that for commit information, which is the `what_you_have_done` part, you should write something meaningful, like `added a new post "Note for Manim Lecture 3" ` or `fixed a typo in the post about manim`. This is important because it will be shown in the commit history of the repository, and it will be helpful for other club members to understand what you have done.


After pushing the changes to the source code repository, you will now need to deploy the website into our github pages repository by the following commands:

```bash
hexo clean
hexo generate
hexo deploy
```

Which is equivalent to 

```bash
hexo cl
hexo g
hexo d
```