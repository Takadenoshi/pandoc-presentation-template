---
title-prefix: Example
title:  Kadena-themed Pandoc Presentation Template
author: tasos@kadena.io isa@kadena.io
date: September 13, 2023
background: assets/images/bg.png # image background; used if video is not present or slide_bg_is_video is not true
icons: # icon sources for title slide
  - assets/icons/k-internal-icon.jpg
video: # video for background. multiple formats are supported
  - src: assets/videos/kd-back.mp4
    type: video/mp4
video_playback_rate: 0.5 # slow down the video
slide_bg_is_video: true # use a darkened version of the video as slide background
---

# Kadena-themed Pandoc Presentation Template

Create Kadena-themed presentations from markdown using pandoc

1) Install requirements
1) run `./gen-watch.sh`
1) Write your slides in `source.md`
1) Load `index.html` in a browser

Optionally: deploy to github pages.

# Requirements

- `./gen.sh` requires pandoc.
    - You can find instructions on installing pandoc on your machine [here](https://pandoc.org/installing.html).
- `./gen-watch.sh` requires nodemon.
    - You can install that globally with `npm i -g nodemon` or `yarn global add nodemon`.

# Running

Running `./gen.sh` will rebuild the target `index.html`.

Running `./gen-watch.sh` will watch the current directory for changes to `.md` or `.slidy` files and run `gen.sh` when any change is detected.

Running `./gen-standalone.sh` will create a standalone index.html with all resources inlined, which can be shared as-is.

# Presenting

Pandoc supports some keyboard shortcuts while presenting, like `s` for smaller font size, `b` for larger, `k` to disable click-to-forward, `c` for a table of contents, etc.

Press `h` while on the presentation to show a detailed help screen.

Aside from those you can also press `v` to hide the video background.

# Configuring

## Markdown metadata

The header of the source markdown file includes the following variables that can be set. Refer to `source.md` contents for an example.

|name|description|
|----|-----------|
|title|Presentation title. Ends up in title slide, page title|
|title-prefix|Presentation prefix for html page title|
|author|Ends up in title slide, page meta author|
|date|Ends up in title slide, page meta date|
|icons|List of image sources to show as icons over the title on the title slide. can be omitted|
|video|List of `{.src, .type}` for video sources for the background of the title slide (or the entire presentation)|
|video_playback_rate|custom playback rate for the video|
|slide_bg_is_video|`true` to use the video as presentation background, `false` to use image instead|
|background|image background for presentation if `video` is missing or `slide_bg_is_video` is `false`|

# Configuring

In case you need to tweak the generated html or stylesheets:

## Slidy template

The js slideshow library used is `slidy`.

The template file which generates the html is `assets/kadena.slidy`.

## Stylesheets

CSS stylesheets can be tweaked under `assets/styles/`.

If you want to pick different colors or tones, please consult the [Color System](https://www.figma.com/file/cNQkFOjrqO3PAYv7TSIhpB/Foundation?type=design&node-id=188-869&mode=design&t=5J7YpU6yxy8El0DC-0).

# Writing pandoc slides

The full pandoc markdown reference can be found [here](https://pandoc.org/MANUAL.html#pandocs-markdown).

## Slides and headings

Slides are separated by H1 headings `# My next Slide` or three dashes `---`.

# Writing pandoc slides

## Code blocks, no line numbers

Code blocks can have syntax highlighting, e.g.:

    ` ` ` javascript
    console.log("very nice");
    ` ` `

_Note: the backticks above had to be spaced for font rendering purposes. Do not include spaces between backticks in your code._

Produces:

```javascript
console.log("very nice");
```
# Writing pandoc slides

## Code blocks, with line numbers

If you need line numbers in code blocks, use this invocation:

    ` ` ` {.javascript .numberLines}
    console.log("very");
    console.log("nice");
    ` ` `

_Note: the backticks above had to be spaced for font rendering purposes. Do not include spaces between backticks in your code._

Produces:

```{.javascript .numberLines}
console.log("very");
console.log("nice");
```

# Writing pandoc slides

## Lists

Lists must be separated with a newline from the previous paragraph **but** without newlines between them:

Correct:

```
This is the full list:

- one
- two
- three
```

Incorrect:

```
This is the full list:

- one

- two

- three
```

# Writing pandoc slides

## Columns

To split a slide in two or more columns, you can use this markdown:

    :::::::::::::: {.columns}
    ::: {.column width="80%"}
    ## large content to the left
    :::
    ::: {.column width="20%"}
    small content to the right
    :::
    ::::::::::::::

Produces:

:::::::::::::: {.columns}
::: {.column width="70%"}
## large content to the left
:::
::: {.column width="30%"}
small content to the right
:::
::::::::::::::

# Writing pandoc slides

## HRs

You can insert a horizontal ruler / HR by using the html tag: `<hr />`

<hr />

# Pre-commit hook

If you need to make sure your `index.html` is up to date with your source, you can use a pre-commit hook like this:

```{.bash .numberLines}
#!/usr/bin/env sh

./gen.sh
git add index.html
```

A sample is provided under `/pre-commit.sample`

# Deploying to Github pages

Deploying this to Github pages is straightforward.

1) (Fork repo, rename, enter your content, etc)
1) Go to GitHub -> Settings -> Pages
1) Under "Build and Deployment -> Source", select "GitHub Actions"
1) Configure the "Static HTML" workflow
1) Accept the defaults
    1) If you have customized the location of `index.html`: Locate `path` under `jobs.deploy.steps.Upload artifact` (should have a comment "Upload entire repository".) Replace `.` with the path to your document root.


_Note: This is only available for public repositories._
