# Kadena-themed Pandoc Presentation Template

Create Kadena-themed presentations from markdown using pandoc

1) Install requirements
1) run `./gen-watch.sh`
1) Write your slides in `source.md`
1) Load `index.html` in a browser

Optionally: deploy to github pages.

This README is available in presentation form [here](https://takadenoshi.github.io/pandoc-presentation-template).

## Requirements

Pandoc & nodemon.

- `./gen.sh` requires pandoc.
    - You can find instructions on installing pandoc on your machine [here](https://pandoc.org/installing.html).
- `./gen-watch.sh` requires nodemon.
    - You can install that globally with `npm i -g nodemon` or `yarn global add nodemon`.
        - Don't have `npm`? You can install [node js](https://nodejs.org/en/download) to get it.

## Running

Running `./gen.sh` will rebuild the target `index.html`.

Running `./gen-watch.sh` will watch the current directory for changes to `.md` or `.slidy` files and run `gen.sh` when any change is detected.

Running `./gen-standalone.sh` will create a standalone index.html with all resources inlined, which can be shared as-is.

## Configuring

This template includes some reasonable defaults and styling for kadena-themed presentations.

### Markdown metadata

The header of the source markdown file includes the following variables that can be set. Refer to `source.md` contents for an example.

|name|description|
|----|-----------|
|title|Presentation title. Ends up in title slide, page title|
|title-prefix|Presentation prefix for html page title|
|author|Ends up in title slide, page meta author|
|date|Ends up in title slide, page meta date|
|icons|List of image sources to show as icons over the title on the title slide. Can be omitted.|
|video|List of `{.src, .type}` for video sources for the background of the title slide (or the entire presentation). Can be omitted.|
|video_playback_rate|Custom playback rate for the video.|
|slide_bg_is_video|`true` to use the video as presentation background, `false` to use image instead. Can be omitted.|
|background|Image background for presentation if `video` is missing or `slide_bg_is_video` is `false`. Can be omitted.|

### Slidy template

The js slideshow library used is `slidy`.

The template file which generates the html is `assets/kadena.slidy`.

### Stylesheets

CSS stylesheets can be tweaked under `assets/styles/`.

If you want to pick different colors or tones, please consult the [Color System](https://www.figma.com/file/cNQkFOjrqO3PAYv7TSIhpB/Foundation?type=design&node-id=188-869&mode=design&t=5J7YpU6yxy8El0DC-0).

# Pre-commit hook

If you need to make sure your `index.html` is up to date with your source, you can use a pre-commit hook like this:

```{.bash .numberLines}
#!/usr/bin/env sh

./gen.sh
git add index.html
```

A sample is provided under `/pre-commit.sample` which you can copy to `.git/hooks/pre-commit`

# Deploying to Github pages

Deploying this to Github pages is straightforward.

1) (Fork repo, rename, enter your content, etc)
1) Go to GitHub -> Settings -> Pages
1) Under "Build and Deployment -> Branch", select `main` and click `Save`.

Your presentation will be deployed to the URL:

`https://<GitHub Username>.github.io/<Repo Name>`

---

If you have moved `index.html` to a subfolder:

1) Edit `/.github/workflows/static.yml`
1) Locate the `jobs.deploy.steps.Upload artifact` step (should have a comment "Upload entire repository".)
1) Replace `path` with the path to your document root.

## Writing pandoc slides

The full pandoc markdown reference can be found [here](https://pandoc.org/MANUAL.html#pandocs-markdown).

### Slides and headings

Slides are separated by H1 headings `# My next Slide` or three dashes `---`.

### Code blocks

Code blocks can have syntax highlighting, e.g.:

    ```javascript
    console.log("very nice");
    ```

If you need line numbers in code blocks, use this invocation:

    ```{.javascript .numberLines}
    console.log("very nice");
    ```

### Lists

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

### Columns

To split a slide in two or more columns, you can use this markdown:

    :::::::::::::: {.columns}
    ::: {.column width="80%"}

    large content to the left

    :::
    ::: {.column width="20%"}

    small content to the right

    :::
    ::::::::::::::

### HRs

You can insert a horizontal ruler / HR by using the html tag: `<hr />`

