---
title: Contributing to Our Blog
description: Instructions for contributing to our Club's Blog
author: vinayak
date: 2025-08-17 01:03:00 -0700
categories: [Demo, Logistics]
tags: [demo]
toc: true
render_with_liquid: false
pin: true
math: true
comments: true
---
> Note: This document takes most of its content from the official documentation of [Chirpy](https://chirpy.dev/docs/contributing/), which is the theme used for our blog. It has been adapted to fit our specific needs and practices.

## Environment Setup
To contribute to our blog, you need to set up your local environment. Follow these steps:

### 1. Fork the Repository
Fork the repository to your GitHub account. This will create a copy of the repository where you can make changes without affecting the original project. You can then clone your forked repository to your local machine.

### 2. Set up the Environment

Once your repository is created, it's time to set up your development environment. There are two primary methods:

#### Using Dev Containers 

Dev Containers offer an isolated environment using Docker, which prevents conflicts with your system and ensures all dependencies are managed within the container.

**Steps**:

1. Install Docker:
   - On Windows/macOS, install [Docker Desktop][docker-desktop].
   - On Linux, install [Docker Engine][docker-engine].
2. Install [VS Code][vscode] and the [Dev Containers extension][dev-containers].
3. Clone your repository:
   - For Docker Desktop: Start VS Code and [clone your repo in a container volume][dc-clone-in-vol].
   - For Docker Engine: Clone your repo locally, then [open it in a container][dc-open-in-container] via VS Code.
4. Wait for the Dev Containers setup to complete.

#### Setting up Natively (If you're feeling adventurous)

For Unix-like systems, you can set up the environment natively for optimal performance, though you can also use Dev Containers as an alternative.

**Steps**:

1. Follow the [Jekyll installation guide](https://jekyllrb.com/docs/installation/) to install Jekyll and ensure [Git](https://git-scm.com/) is installed.
2. Clone your repository to your local machine.
3. If you forked the theme, install [Node.js][nodejs] and run `bash tools/init.sh` in the root directory to initialize the repository.
4. Run command `bundle` in the root of your repository to install the dependencies.


### 3. Using Getting Started in the Environment

#### Start the Jekyll Server

To run the site locally, use the following command:

```terminal
$ bundle exec jekyll serve
```

> If you are using Dev Containers, you must run that command in the **VS Code** Terminal.
{: .prompt-info }

After a few seconds, the local server will be available at <http://127.0.0.1:4000>.

### 4. Creating a new post
Now that your environment is set up, you can start contributing to the blog. Here are some guidelines to follow:

You will need to create a new post file in the `_posts` directory within the appropriate directory category. The file name should follow the format `YYYY-MM-DD-TITLE.EXTENSION`{: .filepath}, where `YYYY-MM-DD` is the date of the post, `TITLE` is a descriptive title, and `EXTENSION` is either `md` or `markdown`.

#### Front Matter

Basically, you need to fill the [Front Matter](https://jekyllrb.com/docs/front-matter/) as below at the top of the post:

```yaml
---
title: TITLE
date: YYYY-MM-DD HH:MM:SS +/-TTTT
categories: [TOP_CATEGORY, SUB_CATEGORY]
tags: [TAG]     # TAG names should always be lowercase
---
```

**Default Front Matter to Use**

```yaml
---
title: Post Title
description: Brief description of the post.
author: <Name of the authors>
date: 2025-08-17 01:03:00 -0700
categories: [Articles, General Information]
tags: [article, general]
pin: true
math: true
comments: true
```

A detailed explanation of each field is as follows:

#### Timezone of Date

To accurately record the release date of a post, you should not only set up the `timezone` of `_config.yml`{: .filepath} but also provide the post's timezone in variable `date` of its Front Matter block. Format: `+/-TTTT`, e.g. `-0700` for phoenix time.

#### Categories and Tags

The `categories` of each post are designed to contain up to two elements, and the number of elements in `tags` can be zero to infinity. For instance:

```yaml
---
categories: [Animal, Insect]
tags: [bee]
---
```

#### Author Information

The author information of the post usually does not need to be filled in the _Front Matter_ , they will be obtained from variables `social.name` and the first entry of `social.links` of the configuration file by default. But you can also override it as follows:

Adding author information in `_data/authors.yml` (If your website doesn't have this file, don't hesitate to create one).

```yaml
<author_id>:
  name: <full name>
  twitter: <twitter_of_author>
  url: <homepage_of_author>
```
{: file="_data/authors.yml" }

And then use `author` to specify a single entry or `authors` to specify multiple entries:

```yaml
---
author: <author_id>                     # for single entry
# or
authors: [<author1_id>, <author2_id>]   # for multiple entries
---
```

#### Post Description

By default, the first words of the post are used to display on the home page for a list of posts, in the _Further Reading_ section, and in the XML of the RSS feed. If you don't want to display the auto-generated description for the post, you can customize it using the `description` field in the _Front Matter_ as follows:

```yaml
---
description: Short summary of the post.
---
```
Additionally, the `description` text will also be displayed under the post title on the post's page.

#### Table of Contents

By default, the **T**able **o**f **C**ontents (TOC) is displayed on the right panel of the post. If you want to turn it off globally, go to `_config.yml`{: .filepath} and set the value of variable `toc` to `false`. If you want to turn off TOC for a specific post, add the following to the post's [Front Matter](https://jekyllrb.com/docs/front-matter/):

```yaml
---
toc: false
---
```

#### Comments
If you want to close the comment for a specific post, add the following to the **Front Matter** of the post:

```yaml
---
comments: true
---
```

### 5. Writing Posts
Once you have set up the post file and filled in the Front Matter, you can start writing your post using Markdown syntax. The important details are explained in the following section.


## Writing Instructions 
This section is based on chirpy's official documentation, which can be found [here](https://chirpy.dev/docs/posts/). It provides a comprehensive overview of how to write posts for our blog. 

### Media

> Copy and paste the following code snippet to the top of your post to set the path for media resources.
{: .prompt-danger }
```markdown
{% assign parts = page.path | split: '/' %}
{% assign filename = parts[2] | split: '.' | first %}
{% assign image_path = site.post_image_path | append: '/' | append: parts[1] | append: '/' | append: filename %}
```

All media resources (images, audio, video) in the post should be placed in the `PostMedia/` directory under a new folder with the exact same name as your post under the relevant category. The images are referenced in the post using the following syntax:
For example, 
```markdown
![Image description]({{image_path}}/image.png)
```

#### Size

To prevent the page content layout from shifting when the image is loaded, we should set the width and height for each image.

```markdown
![Desktop View]({{site.post_image_path}}/category/your-post-title/image.png){: width="700" height="400" }
```
{: .nolineno}
> The code is **Space Sensitive**. Make sure you don't add any extra spaces between the brackets and the attributes.
{: .prompt-warning }

> For an SVG, you have to at least specify its _width_, otherwise it won't be rendered.
{: .prompt-info }

Starting from _Chirpy v5.0.0_, `height` and `width` support abbreviations (`height` → `h`, `width` → `w`). The following example has the same effect as the above:

```markdown
![Desktop View]({{site.post_image_path}}/category/your-post-title/image.png){: w="700" h="400" }
```

{: .nolineno}

#### Position

By default, the image is centered, but you can specify the position by using one of the classes `normal`, `left`, and `right`.

> Once the position is specified, the image caption should not be added.
{: .prompt-warning }

- **Normal position**

  Image will be left aligned in below sample:

  ```markdown
  ![Desktop View](/assets/img/sample/mockup.png){: .normal }
  ```
  {: .nolineno}

- **Float to the left**

  ```markdown
  ![Desktop View](/assets/img/sample/mockup.png){: .left }
  ```
  {: .nolineno}

- **Float to the right**

  ```markdown
  ![Desktop View](/assets/img/sample/mockup.png){: .right }
  ```
  {: .nolineno}

#### Dark/Light mode

You can make images follow theme preferences in dark/light mode. This requires you to prepare two images, one for dark mode and one for light mode, and then assign them a specific class (`dark` or `light`):

```markdown
![Light mode only](/path/to/light-mode.png){: .light }
![Dark mode only](/path/to/dark-mode.png){: .dark }
```

#### Shadow

The screenshots of the program window can be considered to show the shadow effect:

```markdown
![Desktop View](/assets/img/sample/mockup.png){: .shadow }
```
{: .nolineno}

#### Preview Image

If you want to add an image at the top of the post, please provide an image with a resolution of `1200 x 630`. Please note that if the image aspect ratio does not meet `1.91 : 1`, the image will be scaled and cropped.

Knowing these prerequisites, you can start setting the image's attribute:

```yaml
---
image:
  path: /path/to/image
  alt: image alternative text
---
```

Note that the [`media_subpath`](#url-prefix) can also be passed to the preview image, that is, when it has been set, the attribute `path` only needs the image file name.

For simple use, you can also just use `image` to define the path.

```yml
---
image: /path/to/image
---
```

#### LQIP

For preview images:

```yaml
---
image:
  lqip: /path/to/lqip-file # or base64 URI
---
```

> You can observe LQIP in the preview image of post \"[Text and Typography](../text-and-typography/)\".

For normal images:

```markdown
![Image description](/path/to/image){: lqip="/path/to/lqip-file" }
```
{: .nolineno }

#### Video

##### Social Media Platform

You can embed videos from social media platforms with the following syntax:

```liquid
{% include embed/{Platform}.html id='{ID}' %}
```

Where `Platform` is the lowercase of the platform name, and `ID` is the video ID.

The following table shows how to get the two parameters we need in a given video URL, and you can also know the currently supported video platforms.

| Video URL                                                                                          | Platform   | ID             |
| -------------------------------------------------------------------------------------------------- | ---------- | :------------- |
| [https://www.**youtube**.com/watch?v=**H-B46URT4mg**](https://www.youtube.com/watch?v=H-B46URT4mg) | `youtube`  | `H-B46URT4mg`  |
| [https://www.**twitch**.tv/videos/**1634779211**](https://www.twitch.tv/videos/1634779211)         | `twitch`   | `1634779211`   |
| [https://www.**bilibili**.com/video/**BV1Q44y1B7Wf**](https://www.bilibili.com/video/BV1Q44y1B7Wf) | `bilibili` | `BV1Q44y1B7Wf` |

##### Video Files

If you want to embed a video file directly, use the following syntax:

```liquid
{% include embed/video.html src='{URL}' %}
```

Where `URL` is a URL to a video file e.g. `/path/to/sample/video.mp4`.

You can also specify additional attributes for the embedded video file. Here is a full list of attributes allowed.

- `poster='/path/to/poster.png'` — poster image for a video that is shown while video is downloading
- `title='Text'` — title for a video that appears below the video and looks same as for images
- `autoplay=true` — video automatically begins to play back as soon as it can
- `loop=true` — automatically seek back to the start upon reaching the end of the video
- `muted=true` — audio will be initially silenced
- `types` — specify the extensions of additional video formats separated by `|`. Ensure these files exist in the same directory as your primary video file.

Consider an example using all of the above:

```liquid
{%
  include embed/video.html
  src='/path/to/video.mp4'
  types='ogg|mov'
  poster='poster.png'
  title='Demo video'
  autoplay=true
  loop=true
  muted=true
%}
```

##### Audios

If you want to embed an audio file directly, use the following syntax:

```liquid
{% include embed/audio.html src='{URL}' %}
```

Where `URL` is a URL to an audio file e.g. `/path/to/audio.mp3`.

You can also specify additional attributes for the embedded audio file. Here is a full list of attributes allowed.

- `title='Text'` — title for an audio that appears below the audio and looks same as for images
- `types` — specify the extensions of additional audio formats separated by `|`. Ensure these files exist in the same directory as your primary audio file.

Consider an example using all of the above:

```liquid
{%
  include embed/audio.html
  src='/path/to/audio.mp3'
  types='ogg|wav|aac'
  title='Demo audio'
%}
```

### Pinned Posts

You can pin one or more posts to the top of the home page, and the fixed posts are sorted in reverse order according to their release date. Enable by:

```yaml
---
pin: true
---
```

### Prompts

There are several types of prompts: `tip`, `info`, `warning`, and `danger`. They can be generated by adding the class `prompt-{type}` to the blockquote. For example, define a prompt of type `info` as follows:

```md
> Example line for prompt.
{: .prompt-info }
```
{: .nolineno }

### Syntax

###### Inline Code

```md
`inline code part`
```
{: .nolineno }

###### Filepath Highlight

```md
`/path/to/a/file.extend`{: .filepath}
```
{: .nolineno }

###### Code Block

Markdown symbols ```` ``` ```` can easily create a code block as follows:

````md
```
This is a plaintext code snippet.
```
````

##### Specifying Language

Using ```` ```{language} ```` you will get a code block with syntax highlight:

````markdown
```yaml
key: value
```
````

> The Jekyll tag `{% highlight %}` is not compatible with this theme.
{: .prompt-danger }

##### Line Number

By default, all languages except `plaintext`, `console`, and `terminal` will display line numbers. When you want to hide the line number of a code block, add the class `nolineno` to it:

````markdown
```shell
echo 'No more line numbers!'
```
{: .nolineno }
````

##### Specifying the Filename

You may have noticed that the code language will be displayed at the top of the code block. If you want to replace it with the file name, you can add the attribute `file` to achieve this:

````markdown
```shell
# content
```
{: file="path/to/file" }
````

##### Liquid Codes

If you want to display the **Liquid** snippet, surround the liquid code with `{% raw %}` and `{% endraw %}`:

````markdown
{% raw %}
```liquid
{% if product.title contains 'Pack' %}
  This product's title contains the word Pack.
{% endif %}
```
{% endraw %}
````

Or adding `render_with_liquid: false` (Requires Jekyll 4.0 or higher) to the post's YAML block.

### Mathematics

We use [**MathJax**][mathjax] to generate mathematics. For website performance reasons, the mathematical feature won't be loaded by default. But it can be enabled by:

[mathjax]: https://www.mathjax.org/

```yaml
---
math: true
---
```

After enabling the mathematical feature, you can add math equations with the following syntax:

- **Block math** should be added with `$$ math $$` with **mandatory** blank lines before and after `$$`
  - **Inserting equation numbering** should be added with `$$\begin{equation} math \end{equation}$$`
  - **Referencing equation numbering** should be done with `\label{eq:label_name}` in the equation block and `\eqref{eq:label_name}` inline with text (see example below)
- **Inline math** (in lines) should be added with `$$ math $$` without any blank line before or after `$$`
- **Inline math** (in lists) should be added with `\$$ math $$`

```markdown
<!-- Block math, keep all blank lines -->

$$
LaTeX_math_expression
$$

<!-- Equation numbering, keep all blank lines  -->

$$
\begin{equation}
  LaTeX_math_expression
  \label{eq:label_name}
\end{equation}
$$

Can be referenced as \eqref{eq:label_name}.

<!-- Inline math in lines, NO blank lines -->

"Lorem ipsum dolor sit amet, $$ LaTeX_math_expression $$ consectetur adipiscing elit."

<!-- Inline math in lists, escape the first `$` -->

1. \$$ LaTeX_math_expression $$
2. \$$ LaTeX_math_expression $$
3. \$$ LaTeX_math_expression $$
```

> Starting with `v7.0.0`, configuration options for **MathJax** have been moved to file `assets/js/data/mathjax.js`{: .filepath }, and you can change the options as needed, such as adding [extensions][mathjax-exts].  
> If you are building the site via `chirpy-starter`, copy that file from the gem installation directory (check with command `bundle info --path jekyll-theme-chirpy`) to the same directory in your repository.
{: .prompt-tip }

[mathjax-exts]: https://docs.mathjax.org/en/latest/input/tex/extensions/index.html

### Mermaid

[**Mermaid**](https://github.com/mermaid-js/mermaid) is a great diagram generation tool. To enable it on your post, add the following to the YAML block:

```yaml
---
mermaid: true
---
```

Then you can use it like other markdown languages: surround the graph code with ```` ```mermaid ```` and ```` ``` ````.

### Learn More

For more knowledge about Jekyll posts, visit the [Jekyll Docs: Posts](https://jekyllrb.com/docs/posts/).
