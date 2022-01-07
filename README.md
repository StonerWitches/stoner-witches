# stonerwitches.com

This repository houses the codebase for https://www.stonerwitches.com aka the actual greatest website made in the course of modern civilization.

This website is powered by the [Hugo](https://gohugo.io/) framework, which is written in [Go](https://golang.org/) and makes use of the [Tailwind](https://tailwindcss.com/) CSS framework along with the Tailwind CSS [typography plugin](https://tailwindcss.com/docs/typography-plugin) and [form plugin](https://github.com/tailwindlabs/tailwindcss-forms). The build setup uses [PostCSS](https://postcss.org/) and [PurgeCSS](https://purgecss.com/) (when running the production build) for post-processing of CSS. Most of the code is written in HTML, JavaScript, and CSS. AlpineJS is used for easier handling of CSS interactions, transitions, and animations. JavaScript is compiled using Hugo's built-in ESBuild pipelines.

# Setup

## Coding Environment

It is strongly recommended to download [Microsoft Visual Studio Code](https://code.visualstudio.com/docs/setup/setup-overview) or a similar code editor such as Atom to allow for easier reading and modification of code.

Whatever code editor you use, please download the [EditorConfig](https://editorconfig.org/#download) plugin relevant for your editor and ensure to apply the repository `.editorconfig` to ensure consistency across development environments in whitespace, newlines, etc.

## Versions

This project is currently being developed in an environment with the following utilities and versions:

```console
$ node -v
v14.17.5

$ npm -v
8.1.4

$ hugo version
Hugo Static Site Generator v0.79.0-1415EFDC linux/amd64 BuildDate: 2020-11-27T09:09:02Z
```

## Installation

Hugo can be installed by following these directions:

https://gohugo.io/getting-started/installing/

Node JS can be configured using `nvm`. Ensure to `nvm use 14` (or use any version above 12) if you have more than one version of Node installed.

After both Hugo and `npm` are set up correctly, please install `npm` packages for this repository using:

```console
npm install
```

## Development

Runs a server on localhost port 1313 by default. If port 1313 is occupied, Hugo will randomly pick a port to run the application on. To run the development server, from the root directory run:

```console
npm start
```

This command runs `hugo server --disableFastRender` by default. See the [hugo server](https://gohugo.io/commands/hugo_server/) documentation for more options available when running a local Hugo server.

When the Hugo server is running, any updates from watched directories will automatically be rebuilt and made available.

### Branches

There are two primary branches in use:
- `main`
- `testing`

Additional branches can be created for development of specific features. All side branches must be merged into `testing`, then a PR made from `testing` -> `main` to get changes reviewed and approved prior to moving the commits to the production server.

## Production

TODO

# Project Structure

Hugo puts files into a specific [directory structure](https://gohugo.io/getting-started/directory-structure/) with a few key things to note:

- All content goes in the `/content` directory
- All base structure, templates, partials, and shortcodes go in the `/layouts` directory
- All miscellaneous data (used for shortcodes & variables) goes into the `/data` directory
- All CSS goes into `/assets/css` and are referenced from `/css`
- All JS goes into the `/assets/js` directory and are referenced from `/js`
- All images go into the `/static/img` directory and are referenced from `/img`

## Creating a New Page

### Content and Images

When creating a new page, new files should be added under the following directory structure:

```html
/content/$PARENT_FOLDER/$CHILD_FOLDER
- _index.html (Contains all Markdown & HTML content formatted using shortcodes)

/img/$PARENT_FOLDER/$CHILD_FOLDER
```

If creating a new parent/child folder and URL pattern, make sure there is also an `_index.html` file created at the parent level directory structure (`/content/$PARENT_FOLDER`) that excludes the page from the sitemap, if there is no content defined for the parent page:

```markdown
---
sitemap_exclude: true
---
```

### URLs and Menu Items

Existing files that may need to be modified include:

```html
# Checklist: Is the newly created page given a nickname in this file?
/data
- urls.toml (Contains all nicknames for URLs for created pages)

# Checklist: Is the page meant to appear in the navigation?
/config.toml
- [menu] (Both top and footer menus are defined here; adjust menu item according to weight and ensure the item is placed under the correct menu group for accurate positioning)
```

_Note: In config.toml, lower weight gets higher precedence. So content with lower weight will come first._

### Shortcodes

TODO: Update this section with relevant shortcode examples.

Panels that are available for use as templates for content sections can be found under `/layouts/shortcodes`. Each are commented with usage instructions. All shortcodes must be referenced using `{{< shortcode-name >}}{{< /shortcode-name >}}` as syntax for the tags.

As an example, a shortcode being referenced under `/content/` that has inner content and variables:

```markdown
{{< panel-simple
  header="Lorem Ipsum"
  btnText="my button text"
  btnLink="{{ $.Site.Data.urls.urlNickname }}"
  textAlignment="center" >}}

  Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.

{{< /panel-simple >}}
```

If a shortcode is fully defined or has no inner content, it should not use a closing tag.

```markdown
{{< panel-fully-defined >}}

{{< panel-with-variables
  header="Lorem ipsum"
  btnText="my button text"
  btnLink={{ $.Site.Data.urls.urlNickname
  textAlignment="center >}}
```

### Expectations

TODO: Document expectations for coding standards within this block. Emphasize editorconfig & code editor usage, as well as standards such as:

- Whitespaces around code blocks. There is always whitespace around wrapping shortcodes, but never any whitespace inside the innermost
shortcodes. For example, in the following code block, `content-wrapper` & `content` both have whitespace surrounding the inner content.
However, `heading1` and `display1` have no further children shortcodes, so whitespace is left out.
- Tags are always alphabetized. There are as many ways to organize tags as there are developers; to keep consistency without requiring
those adding on to the codebase to be aware of semantics, alphabetization is the way to go.

```html
<!-- HOW INTERESTING -->
{{< content-wrapper
  backgroundImage="bkg_img_example" >}}

  {{< content
    contentPlacement="left"
    textAlignment="left"
    width="partial" >}}

    {{< heading1
      color="light" >}}
      How Interesting
    {{< /heading1 >}}

    {{< display1
      color="light" >}}
      Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
      Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.
    {{< /display1 >}}

  {{< /content >}}

{{< /content-wrapper >}}
```

# Licenses

## External Dependencies

- [npm](https://docs.npmjs.com/policies/npm-license/) - Artistic License 2.0
- [Hugo](https://github.com/gohugoio/hugo/blob/master/LICENSE) - Apache 2
- [PostCSS](https://github.com/postcss/postcss/blob/master/LICENSE) - MIT
- [Tailwind CSS](https://github.com/tailwindlabs/tailwindcss/blob/master/LICENSE) - MIT

# Copyright

&copy; 2022 Stoner Witches. All Rights Reserved.
