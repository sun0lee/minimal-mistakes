---
title: "Layouts"
permalink: /docs/layouts/
excerpt: "Descriptions and samples of all layouts included with the theme and how to best use them."
single_layout_gallery:
  - image_path: /assets/images/mm-layout-single-header.png
    alt: "single layout with header example"
  - image_path: /assets/images/mm-layout-single-meta.png
    alt: "single layout with comments and related posts"
last_modified_at: 2020-08-30T21:27:40-04:00
toc: true
toc_sticky: true
toc_label: "Included Layouts"
toc_icon: "columns"
---

레이아웃은 모든 테마에 기본이 됨. 아래에서는 기본으로 제공되는 레이아웃, 모양 및 제작된 콘텐츠를 확인함.  

## Default 레이아웃

다른 모든 레이아웃이 상속하는 기본 레이아웃. `_includes`:

* `<head>` elements
* masthead navigation links
* {% raw %}`{{ content }}`{% endraw %}
* page footer
* scripts

**Note:** You won't ever assign this layout directly to a post or page. Instead all other layouts will build off of it by setting `layout: default` in their YAML Front Matter.
{: .notice--warning}

### 레이아웃 기반 사용자 정의 클래스

 - 각 레이아웃에 해당하는 클래스 이름이 `<body>` element에 자동으로 추가됨.  
 - 예를 들면 `<body class="layout--single">`

| layout           | class name                  |
| ---------------- | --------------------------- |
| archive          | `.layout--archive`          |
| archive-taxonomy | `.layout--archive-taxonomy` |
| search           | `.layout--search`           |
| single           | `.layout--single`           |
| splash           | `.layout--splash`           |
| home             | `.layout--home`             |
| posts            | `.layout--posts`            |
| categories       | `.layout--categories`       |
| category         | `.layout--category`         |
| tags             | `.layout--tags`             |
| tag              | `.layout--tag`              |

YAML Front Matter를 사용하여 CSS나 JavaScript로 대상에 사용자 지정 클래스를 할당할 수 있음. 예를 들어 "art directed" posts처럼 특정 페이지에 사용자 지정 스타일을 추가하는데 적합함.

Example:

```yaml
---
layout: splash
classes:
  - landing
  - dark-theme
---
```

Outputs:

```html
<body class="layout--splash landing dark-theme">
```

### Canonical URL

YAML Front Matter에서  `canonical_url` 옵션을 지정하여 사용자 지정 표준 url을 설정할 수 있음.

```yaml
layout: single
title: Title of Your Post
canonical_url: "https://yoursite.com/custom-canonical-url"
```

이렇게 하면 페이지의 `<head>`에서 다음이 생성됨:

```html
<link rel="canonical" href="https://yoursite.com/custom-canonical-url" />
```

## Compress 레이아웃

HTML을 Liquid로 압축하는 Jekyll layout으로 추가하기.
`layout: compress` to `_layouts/default.html`.

**Note:** `// comments` 인라인이 있는 경우 마크업을 엉망으로 만들고 JavaScript를 손상시키는 것으로 알려져 있습니다. 이러한 이유로 기본적으로 비활성화되어 있습니다
{: .notice--danger}

* [Documentation](http://jch.penibelst.de/)

## Single layout

sidebar와 main content의 조합으로 이루어진 제일 많이 사용하는 레이아웃

**Includes:**

* 캡션이 있는 헤더 이미지 (Optional)
* header overlay (solid color/image) (Optional) + text and optional "call to action" button
* Optional social sharing links module
* Optional comments module
* Optional related posts module
* Wide page variant

**설정방법**
1. Front Matter : `layout: single`
2. `_config.yml` : [Front Matter default]({{ "/docs/configuration/#front-matter-defaults" | relative_url }}) -> 추천!

### Wide page

본 콘텐츠를 오른쪽으로 확장하여 일반적으로 목차가 차지하는 공간을 채웁니다. 게시물 또는 YAML Front Matter에 다음을 추가합니다. :

```yaml
classes: wide
```

**Note:** If the page contains a table of contents, it will no longer appear to the right. Instead it will be forced into the main content container directly following the page's title.
{: .notice--info}

### toc (Table of contents)

YAML Front Matter에  `toc: true` 를 추가하면 자동 생성 목차 목록이 활성화 됨.


| Parameter   | Required | Description | Default |
| ---------   | -------- | ----------- | ------- |
| **toc**     | Optional | Show table of contents. (boolean) | `false` |
| **toc_label** | Optional | Table of contents title. (string) | `toc_label` in UI Text data file. |
| **toc_icon**  | Optional | Table of contents icon, displays before the title. (string) | [Font Awesome](https://fontawesome.com/v5/search?s=solid&m=free) <i class="fas fa-file-alt"></i> **file-alt** icon. Other FA icons can be used instead. |
| **toc_sticky** | Optional | Stick table of contents to top of screen.                   | `false` |

**TOC example with custom title and icon**

```yaml
---
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---
```

{% capture notice-text %}
**Note:** You need to use contiguous levels of headings for the TOC to generate properly. For example:

```markdown
Good headings:

# Heading
## Heading
### Heading
### Heading
# Heading
## Heading

Bad headings:

# Heading
### Heading (skipped H2)
##### Heading (skipped H4)
```
{% endcapture %}

<div class="notice--warning">
  {{ notice-text | markdownify }}
</div>

## Archive 레이아웃

기본적으로 `single` 레이아웃과 동일하며, 마크업 조정 및 일부 모듈 제거에 차이가 있음.

**Includes:**

* 캡션이 있는 선택적 헤더 이미지 (Optional)
* 헤더 오버레이 (단색/ 이미지; Optional) + text + 버튼 (optional "call to action")
* 목록 및 그리드 보기

Below are sample archive pages you can easily drop into your project, taking care to rename `permalink`, `title`, or the filename to fit your site. Each is 100% compatible with GitHub Pages.

* [All Posts Grouped by Category -- List View][posts-categories]
* [All Posts Grouped by Tag -- List View][posts-tags]
* [All Posts Grouped by Year -- List View][posts-year]
* [All Posts Grouped by Collection -- List View][posts-collection]
* [Portfolio Collection -- Grid View][portfolio-collection]

[posts-categories]: https://github.com/{{ site.repository }}/blob/master/docs/_pages/category-archive.md
[posts-tags]: https://github.com/{{ site.repository }}/blob/master/docs/_pages/tag-archive.md
[posts-year]: https://github.com/{{ site.repository }}/blob/master/docs/_pages/year-archive.md
[posts-collection]: https://github.com/{{ site.repository }}/blob/master/docs/_pages/collection-archive.html
[portfolio-collection]: https://github.com/{{ site.repository }}/blob/master/docs/_pages/portfolio-archive.md

post와 page 발췌문(excerpt)은 텍스트의 첫 단락을 가져오는 Jekyll에 의해 자동 생성됨.
excerpt을 직접 작성하려면 YAML Front Matter에서 아래처럼 직접 기술할 수 있음.

```yaml
excerpt: "A unique line of text to describe this post that will display in an archive listing and meta description with SEO benefits."
```

### Wide page

```yaml
classes: wide
```

### Grid 보기

Adding `type=grid` to the `archive-single` archive post가 4열 그리드로 표시됨.

포트폴리오 컬렉션의 모든 문서를 표시하는 아카이브를 생성하기
- portfolio archive page (eg. `_pages/portfolio-archive.md`)
- YAML Front Matter:

```yaml
---
title: Portfolio
layout: collection
permalink: /portfolio/
collection: portfolio
entries_layout: grid
---
```

- 티져 이미지는 YAML Front Matter을 사용하여 헤더 이미지와 유사하게 할당됨.

```yaml
header:
  teaser: path-to-teaser-image.jpg
```

**Note:**  자세한 내용은 `_include`의 링크 참조  [**Helpers**]({{ "/docs/helpers/" | relative_url }}).
{: .notice--info}

## Taxonomy(분류) 아카이브

If you have the luxury of using Jekyll plugins, the creation of category and tag archives is greatly simplified. Simply enable support for the [`jekyll-archives`](https://github.com/jekyll/jekyll-archives) plugin with a few `_config.yml` settings as noted in the [**Configuration**]({{ "/docs/configuration/#archive-settings" | relative_url }}) section and you're good to go.

직접 `jekyll-archives` 아카이브 페이지를 생성할 수 있으며, 아래는 샘플 분류 아카이브 목록임.  

| Name                 | Layout | Example |
| -------------------- | ------ | ------ |
| [Posts Archive](https://mmistakes.github.io/minimal-mistakes/year-archive/) | `layout: posts` | [year-archive.md](https://github.com/mmistakes/minimal-mistakes/blob/master/docs/_pages/year-archive.md) |
| [Categories Archive](https://mmistakes.github.io/minimal-mistakes/categories/) | `layout: categories` | [category-archive.md](https://github.com/mmistakes/minimal-mistakes/blob/master/docs/_pages/category-archive.md) |
| [Category Archive](https://mmistakes.github.io/minimal-mistakes/categories/edge-case/) | `layout: category` | [edge-case.md](https://github.com/mmistakes/minimal-mistakes/blob/master/docs/_pages/edge-case.md) |
| [Tags Archive](https://mmistakes.github.io/minimal-mistakes/tags/) | `layout: tags` | [tag-archive.md](https://github.com/mmistakes/minimal-mistakes/blob/master/docs/_pages/tag-archive.md) |
| [Tag Archive](https://mmistakes.github.io/minimal-mistakes/tags/markup/) | `layout: tag` | [markup.md](https://github.com/mmistakes/minimal-mistakes/blob/master/docs/_pages/markup.md) |
| [Collection Archive](https://mmistakes.github.io/minimal-mistakes/recipes/) | `layout: collection` | [recipes-archive.md](https://github.com/mmistakes/minimal-mistakes/blob/master/docs/_pages/recipes-archive.md) |

**Note:** 기본적으로 문서는 목록 보기로 표시되며 yaml front matter에서 다음을 설정하면 됨. `entries_layout: grid`
{: .notice--info}

### `layout: posts`

This layout displays all posts grouped by the year they were published. It accommodates the same front matter as `layout: archive`.

### `layout: categories`

This layout displays all posts grouped category. It accommodates the same front matter as `layout: archive`.

### `layout: tags`

This layout displays all posts grouped by tag. It accommodates the same front matter as `layout: archive`.

### `layout: collection`

This layout displays all documents grouped by a specific collection. It accommodates the same front matter as `layout: archive` with the addition of the following:

```yaml
collection: # collection name
entries_layout: # list (default), grid
show_excerpts: # true (default), false
sort_by: # date (default), title or any metadata key added to the collection's documents
sort_order: # forward (default), reverse
```

To create a page showing all documents in the `recipes` collection you'd create `recipes.md` in the root of your project and add this front matter:

```yaml
title: Recipes
layout: collection
permalink: /recipes/
collection: recipes
```

If you want to sort the collection by title add `sort_by: title`. If you want reverse sorting, add `sort_order: reverse`.
You can also use any metadata key that is present in the documents. For example, you can add `number: <any number>` to your documents and use `number` as the sort key:

```yaml
sort_by: number
```

### `layout: category`

This layout displays all posts grouped by a specific category. It accommodates the same front matter as `layout: archive` with the addition of the following:

```yaml
taxonomy: # category name
entries_layout: # list (default), grid
```

To create a page showing all posts assigned to the category `foo` you'd create `foo.md` and add this front matter:

```yaml
title: Foo
layout: category
permalink: /categories/foo/
taxonomy: foo
```

### `layout: tag`

This layout displays all posts grouped by a specific tag. It accommodates the same front matter as `layout: archive` with the addition of the following:

```yaml
taxonomy: # tag name
entries_layout: # list (default), grid
```

To create a page showing all posts assigned to the tag `foo bar` you'd create `foo-bar.md` and add this front matter:

```yaml
title: Foo Bar
layout: tag
permalink: /tags/foo-bar/
taxonomy: foo bar
```

## Home page layout

A derivative archive page layout to be used as a simple home page. It is built to show a paginated list of recent posts based off of the [pagination settings]({{ "/docs/configuration/#paginate" | relative_url }}) in `_config.yml`.

<figure>
  <img src="{{ '/assets/images/mm-home-post-pagination-example.jpg' | relative_url }}" alt="paginated home page example">
  <figcaption>Example of a paginated home page showing 5 recent posts.</figcaption>
</figure>

To use create `index.html` at the root of your project and add the following YAML Front Matter:

```yaml
---
layout: home
---
```

Then configure pagination in `_config.yml`.

```yaml
paginate: 5 # amount of posts to show
paginate_path: /page:num/
```

If you'd rather have a paginated page of posts reside in a subfolder instead of acting as your homepage make the following adjustments.

Create `index.html` in the location you'd like. For example if I wanted it to live at **/blog** I'd create `/blog/index.html` with `layout: home` in its YAML Front Matter.

Then adjust the `paginate_path` in **_config.yml** to match.

```yaml
paginate_path: /blog/page:num
```

**Note:** Jekyll can only paginate a single `index.html` file. If you'd like to paginate more pages (e.g. category indexes) you'll need the help of a custom plugin. For more pagination related settings check the [**Configuration**]({{ "/docs/configuration/#paginate" | relative_url }}) section.
{: .notice--info}

**Note:** By default, documents are shown in a list view. To change to a grid view add `entries_layout: grid` to the page's front matter. To increase the width of the main container, giving more space to the grid items also add `classes: wide` to the home page's YAML Front Matter.
{: .notice--info}

## Splash page layout

For full-width landing pages that need a little something extra add `layout: splash` to the YAML Front Matter.

**Includes:**

* Optional header image with caption
* Optional header overlay (solid color/image) + text and optional "call to action" button
* Feature blocks (`left`, `center`, and `right` alignment options)

![splash page layout example]({{ "/assets/images/mm-layout-splash.png" | relative_url }})

Feature blocks can be assigned and aligned to the `left`, `right`, or `center` with a sprinkling of YAML. For full details on how to use the `feature_row` helper check the [**Content**]({{ "/docs/helpers/" | relative_url }}) section or review a [sample splash page](https://github.com/{{ site.repository }}/blob/master/docs/_pages/splash-page.md).

## Search page layout

A page with a search form. Add `layout: search` to the YAML Front Matter similar to [this example](https://github.com/mmistakes/minimal-mistakes/blob/master/test/_pages/search.md) on the test site.

![search page layout example]({{ "/assets/images/search-layout-example.png" | relative_url }})

**Note:** A page using the `layout: search` isn't compatible with the new [site search feature]({{ "/docs/configuration/#site-search" | relative_url }}) incorporated in the masthead.
{: .notice--warning}

### Exclusions

If you would like to exclude specific pages/posts from the search index set the search flag to `false` in the YAML Front Matter for the page/post.

```yaml
search: false
```

**ProTip:** Add a link to this page in the masthead navigation.
{: .notice--info}

---

## Headers

To add some visual punch to a post or page, a large full-width header image can be included.

Be sure to resize your header images. `~1280px` is a good width if you aren't [responsively serving up images](http://alistapart.com/article/responsive-images-in-practice). Through the magic of CSS they will scale up or down to fill the container. If you go with something too small it will look like garbage when upscaled, and something too large will hurt performance.

**Please Note:** Paths for image headers, overlays, teasers, [galleries]({{ "/docs/helpers/#gallery" | relative_url }}), and [feature rows]({{ "/docs/helpers/#feature-row" | relative_url }}) have changed and require a full path. Instead of just `image: filename.jpg` you'll need to use the full path eg: `image: /assets/images/filename.jpg`. The preferred location is now `/assets/images/`, but can be placed elsewhere or external hosted. This all applies for image references in `_config.yml` and `author.yml` as well.
{: .notice--danger}

![single layout header image example]({{ "/assets/images/mm-single-header-example.jpg" | relative_url }})

Place your images in the `/assets/images/` folder and add the following YAML Front Matter:

```yaml
header:
  image: /assets/images/image-filename.jpg
```

For externally hosted images include the full image path instead of just the filename:

```yaml
header:
  image: http://some-site.com/assets/images/image.jpg
```

To provide a custom alt tag for screen readers:

```yaml
header:
  image: /assets/images/unsplash-image-1.jpg
  image_description: "A description of the image"
```

To include a caption or attribution for the image:

```yaml
header:
  image: /assets/images/unsplash-image-1.jpg
  caption: "Photo credit: [**Unsplash**](https://unsplash.com)"
```

**ProTip:** Captions written in Markdown are supported, so feel free to add links, or style text. Just be sure to wrap it in quotes.
{: .notice--info}

### Header overlay

To overlay text on top of a header image you have a few more options:

| Name                     | Description | Default |
| ----                     | ----------- | ------- |
| **overlay_image**        | Header image you'd like to overlay. Same rules as `header.image` from above. | |
| **overlay_filter**       | Color/opacity to overlay on top of the header image. Example: `0.5`, `rgba(255, 0, 0, 0.5)` or [`linear-gradient`][mdn-linear-gradient]. |
| **show_overlay_excerpt** | Display excerpt in the overlay text | true |
| **excerpt**              | Auto-generated page excerpt is added to the overlay text or can be overridden. | |
| **tagline**              | Overrides page excerpt. Useful when header text needs to be different from excerpt in archive views. | |
| **actions**              | Call to action button links (`actions` array: `label` and `url`). More than one button link can be assigned. | |
| **cta_label**            | Deprecated, use `actions` instead. Call to action button text label. | `more_label` in UI Text data file |
| **cta_url**              | Deprecated, use `actions` instead. Call to action button URL. | |

  [mdn-linear-gradient]: https://developer.mozilla.org/en-US/docs/Web/CSS/linear-gradient()

With this YAML Front Matter:

```yaml
excerpt: "This post should display a **header with an overlay image**, if the theme supports it."
header:
  overlay_image: /assets/images/unsplash-image-1.jpg
  caption: "Photo credit: [**Unsplash**](https://unsplash.com)"
  actions:
    - label: "More Info"
      url: "https://unsplash.com"
```

You'd get a header image overlaid with text and a call to action button like this:

![single layout header overlay example]({{ "/assets/images/mm-single-header-overlay-example.jpg" | relative_url }})

You also have the option of specifying a solid background-color to use instead of an image.

![single layout header overlay with background fill]({{ "/assets/images/mm-single-header-overlay-fill-example.jpg" | relative_url }})

```yaml
excerpt: "This post should display a **header with a solid background color**, if the theme supports it."
header:
  overlay_color: "#333"
```

You can also specifying the opacity (between `0` and `1`) of a black overlay like so:

![transparent black overlay]({{ "/assets/images/mm-header-overlay-black-filter.jpg" | relative_url }})

```yaml
excerpt: "This post should [...]"
header:
  overlay_image: /assets/images/unsplash-image-1.jpg
  overlay_filter: 0.5 # same as adding an opacity of 0.5 to a black background
  caption: "Photo credit: [**Unsplash**](https://unsplash.com)"
  actions:
    - label: "Download"
      url: "https://github.com"
```

Or if you feel colorful, use full rgba:

![transparent red overlay]({{ "/assets/images/mm-header-overlay-red-filter.jpg" | relative_url }})

```yaml
excerpt: "This post should [...]"
header:
  overlay_image: /assets/images/unsplash-image-1.jpg
  overlay_filter: rgba(255, 0, 0, 0.5)
  caption: "Photo credit: [**Unsplash**](https://unsplash.com)"
  actions:
    - label: "Download"
      url: "https://github.com"
```

Or if you want to do more fancy things, go all the way to [linear-gradient][mdn-linear-gradient]:

![transparent custom overlay]({{ "/assets/images/mm-header-overlay-custom-filter.jpg" | relative_url }})

```yaml
excerpt: "This post should [...]"
header:
  overlay_image: /assets/images/unsplash-image-1.jpg
  overlay_filter: linear-gradient(rgba(255, 0, 0, 0.5), rgba(0, 255, 255, 0.5))
  caption: "Photo credit: [**Unsplash**](https://unsplash.com)"
  actions:
    - label: "Download"
      url: "https://github.com"
```

Multiple call to action button links can be assigned like this:

```yaml
excerpt: "This post should display a **header with an overlay image**, if the theme supports it."
header:
  overlay_image: /assets/images/unsplash-image-1.jpg
  caption: "Photo credit: [**Unsplash**](https://unsplash.com)"
  actions:
    - label: "Foo Button"
      url: "#foo"
    - label: "Bar Button"
      url: "#bar"
```

### Open Graph & Twitter Card images

By default the large page header or overlay images are used for sharing previews. If you'd like to set this image to something else use `page.header.og_image` like:

```yaml
header:
  image: /assets/images/your-page-image.jpg
  og_image: /assets/images/your-og-image.jpg
```

**ProTip:** `og_image` is useful for setting OpenGraph images on pages that don't have a header or overlay image.
{: .notice--info}

---

## Sidebars

The space to the left of a page's main content is blank by default, but has the ability to show an author profile (name, short biography, social media links), custom content, or both.

### Author profile

Add `author_profile: true` to a post or page's YAML Front Matter.

![single layout example]({{ "/assets/images/mm-layout-single.png" | relative_url }})

Better yet, enable it with Front Matter Defaults set in `_config.yml`.

```yaml
defaults:
  # _posts
  - scope:
      path: ""
      type: posts
    values:
      author_profile: true
```

**Note:** To disable the author sidebar profile for a specific post or page, add `author_profile: false` to the YAML Front Matter instead.
{: .notice--warning}

To assign more author links, add to the `author.links` array  in [`_config.yml`]({{ "/docs/configuration/" | relative_url }}) link so. Any of [Font Awesome's icons](https://fontawesome.com/v5/search) are available for use.

```yaml
author:
  name: "Your Name"
  avatar: "/assets/images/bio-photo.jpg"
  bio: "I am an **amazing** person." # Note: Markdown is allowed
  location: "Somewhere"
  links:
    - label: "Made Mistakes"
      icon: "fas fa-fw fa-link"
      url: "https://mademistakes.com"
    - label: "Twitter"
      icon: "fab fa-fw fa-twitter-square"
      url: "https://twitter.com/mmistakes"
    - label: "GitHub"
      icon: "fab fa-fw fa-github"
      url: "https://github.com/mmistakes"
    - label: "Instagram"
      icon: "fab fa-fw fa-instagram"
      url: "https://instagram.com/mmistakes"
```

**Note:** Depending on the icon and theme skin used, colors may not be used. Popular social networks like Twitter, Facebook, Instagram, etc. have the appropriate brand color set in CSS. To change or add missing colors edit [`_utilities.scss`](https://github.com/mmistakes/minimal-mistakes/blob/master/_sass/minimal-mistakes/_utilities.scss) in `<site root>/_sass/minimal-mistakes/`.
{: .notice--info}

For example, to color a Reddit icon, simply add a `color` declaration and the corresponding hex code like so:

```scss
.social-icons {
  .fa-reddit {
    color: #ff4500;
  }
}
```

![Reddit link in author profile with color]({{ "/assets/images/mm-author-profile-reddit-color.png" | relative_url }})

### Custom sidebar content

Blocks of content can be added by using the following under `sidebar`:

| Name          | Description                                                |
| ----          | -----------                                                |
| **title**     | Title or heading.                                          |
| **image**     | Image path placed in `/images/` folder or an external URL. |
| **image_alt** | Alternate description for image.                           |
| **text**      | Text. Markdown is allowed.                                 |

Multiple blocks can also be added by following the example below:

```yaml
sidebar:
  - title: "Title"
    image: http://placehold.it/350x250
    image_alt: "image"
    text: "Some text here."
  - title: "Another Title"
    text: "More text here."
```

<figure>
  <img src="{{ '/assets/images/mm-custom-sidebar-example.jpg' | relative_url }}" alt="custom sidebar content example">
  <figcaption>Example of custom sidebar content added as YAML Front Matter.</figcaption>
</figure>

**Note:** Custom sidebar content added to a post or page's YAML Front Matter will appear below the author profile if enabled with `author_profile: true`.
{: .notice--info}

### Custom sidebar navigation menu

To create a sidebar menu[^sidebar-menu] similar to the one found in the theme's documentation pages you'll need to modify a `_data` file and some YAML Front Matter.

[^sidebar-menu]: Sidebar menu supports 1 level of nested links.

<figure>
  <img src="{{ '/assets/images/mm-custom-sidebar-nav.jpg' | relative_url }}" alt="sidebar navigation example">
  <figcaption>Custom sidebar navigation menu example.</figcaption>
</figure>

To start, add a new key to `_data/navigation.yml`. This will be referenced later via YAML Front Matter so keep it short and memorable. In the case of the theme's documentation menu I used `docs`.

**Sample sidebar menu links:**

```yaml
docs:
  - title: Getting Started
    children:
      - title: "Quick-Start Guide"
        url: /docs/quick-start-guide/
      - title: "Structure"
        url: /docs/structure/
      - title: "Installation"
        url: /docs/installation/
      - title: "Upgrading"
        url: /docs/upgrading/

  - title: Customization
    children:
      - title: "Configuration"
        url: /docs/configuration/
      - title: "Navigation"
        url: /docs/navigation/
      - title: "UI Text"
        url: /docs/ui-text/
      - title: "Authors"
        url: /docs/authors/
      - title: "Layouts"
        url: /docs/layouts/

  - title: Content
    children:
      - title: "Working with Posts"
        url: /docs/posts/
      - title: "Working with Pages"
        url: /docs/pages/
      - title: "Working with Collections"
        url: /docs/collections/
      - title: "Helpers"
        url: /docs/helpers/
      - title: "Utility Classes"
        url: /docs/utility-classes/

  - title: Extras
    children:
      - title: "Stylesheets"
        url: /docs/stylesheets/
      - title: "JavaScript"
        url: /docs/javascript/
```

Now you can pull these links into any page by adding the following YAML Front Matter.

```yaml
sidebar:
  nav: "docs"
```

**Note:** `nav: "docs"` references the `docs` key in `_data/navigation.yml` so make sure they match.
{: .notice--info}

If you're adding a sidebar navigation menu to several pages the use of Front Matter Defaults is a better option. You can define them in `_config.yml` to avoid adding it to every page or post.

**Sample sidebar nav default:**

```yaml
defaults:
  # _docs
  - scope:
      path: ""
      type: docs
    values:
      sidebar:
        nav: "docs"
```

---

## Social sharing links

The `single` layout has an option to enable social links at the bottom of posts for sharing on Twitter, Facebook, and LinkedIn. Similar to the links found in the author sidebar, the theme ships with defaults for the most common social networks.

![default social share link buttons]({{ "/assets/images/mm-social-share-links-default.png" | relative_url }})

To enable these links add `share: true` to a post or page's YAML Front Matter or use a [default](https://jekyllrb.com/docs/configuration/#front-matter-defaults) in your `_config.yml` to apply more globally.

If you'd like to add, remove, or change the order of these default links you can do so by editing [`_includes/social-share.html`](https://github.com/mmistakes/minimal-mistakes/blob/master/_includes/social-share.html).

Let's say you wanted to replace the LinkedIn button with a Reddit one. Simply replace the HTML with the following:

```html
{% raw %}<a href="https://www.reddit.com/submit?url={{ page.url | absolute_url | url_encode }}&title={{ page.title }}" class="btn" title="{{ site.data.ui-text[site.locale].share_on_label }} Reddit"><i class="fab fa-fw fa-reddit" aria-hidden="true"></i><span> Reddit</span></a>{% endraw %}
```

The important parts to change are:

1. Share point URL *eg. `https://www.reddit.com/submit?url=`
2. Link `title`
3. [Font Awesome icon](http://fontawesome.io/icons/) (`fa-` class)
4. Link label

![Reddit social share link button]({{ "/assets/images/mm-social-share-links-reddit-gs.png" | relative_url }})

To change the color of the button use one of the built in [utility classes]({{ "/docs/utility-classes/#buttons" | relative_url }}). Or you can create a new button class to match whatever color you want.

Under the `$social` color map in `assets/_scss/_buttons.scss` simply add a name (this will be appened to `btn--`) that matches the new button class. In our case `reddit` ~> `.btn--reddit`.

```scss
$social:
(facebook, $facebook-color),
(twitter, $twitter-color),
(linkedin, $linkedin-color),
(reddit, #ff4500);
```

**ProTip:** For bonus points you can add it as a Sass `$variable` that you set in `_variables.scss` like the other ["brand" colors](http://brandcolors.net/).
{: .notice--info}

Add the new `.btn--reddit` class to the `<a>` element from earlier, [compile `main.css`]({{ "/docs/stylesheets/" | relative_url }}) and away you go.

```html
{% raw %}<a href="https://www.reddit.com/submit?url={{ page.url | relative_url }}&title={{ page.title }}" class="btn btn--reddit" title="{{ site.data.ui-text[site.locale].share_on_label }} Reddit"><i class="fab fa-fw fa-reddit" aria-hidden="true"></i><span> Reddit</span></a>{% endraw %}
```

![Reddit social share link button]({{ "/assets/images/mm-social-share-links-reddit-color.png" | relative_url }})

---

## Custom head and footer

The `default` layout includes a number of custom templates, which provide ways for you to directly add content to all your pages.

### Head

`_includes/head/custom.html` is included at the end of the `<head>` tag. An example use of this include is to add custom CSS per page:

Add some Liquid tags for the new configuration to `_includes/head/custom.html`.
{% raw %}```html
{% if page.page_css %}
  {% for stylesheet in page.page_css %}
    <link rel="stylesheet" href="{{ stylesheet | relative_url }}">
  {% endfor %}
{% endif %}
```{% endraw %}

Next, add `page_css` to any page's YAML Front Matter to have your CSS loaded for that page.
```yaml
page_css:
  - /path/to/your/custom.css
```

### Footer

`_includes/footer/custom.html` is included at the beginning of the `<footer>` tag. An example use of this include is to add custom JavaScript per page:

Add some Liquid tags for the new configuration to `_includes/footer/custom.html`.
{% raw %}```html
{% if page.page_js %}
  {% for script in page.page_js %}
    <script src="{{ script | relative_url }}"></script>
  {% endfor %}
{% endif %}
```{% endraw %}

Next, add `page_js` to any page's YAML Front Matter to have your JavaScript loaded for that page.
```yaml
page_js:
  - /path/to/your/custom.js
```

---
