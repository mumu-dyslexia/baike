# Hugo Template Guide

## Template Folder Location

**Templates are located in:** `layouts/` folder (at the root of your Hugo site)

```
layouts/
├── _partials/          # Reusable template fragments
├── _shortcodes/        # Custom shortcodes
├── _markup/            # Markdown rendering templates
├── baseof.html         # Base template (wraps all pages)
├── home.html           # Homepage template
├── single.html         # Default single page template
├── list.html           # Default list/section template
├── docs/               # Templates for "docs" type content
│   ├── single.html     # Single doc page
│   └── list.html       # Doc section listing
├── blog/               # Templates for "blog" type content
│   ├── single.html     # Single blog post
│   └── list.html       # Blog listing page
└── ...                 # Other templates
```

## How Hugo Determines Which Template to Use

Hugo uses a **template lookup order** to find the right template. It checks templates in this order (most specific first):

### For Single Pages (articles):

1. `layouts/{section}/{type}/single.html` - Most specific
2. `layouts/{section}/single.html` - Section-specific
3. `layouts/{type}/single.html` - Type-specific
4. `layouts/single.html` - Default fallback

### For List Pages (sections):

1. `layouts/{section}/{type}/list.html`
2. `layouts/{section}/list.html`
3. `layouts/{type}/list.html`
4. `layouts/list.html`

## Content Types

Content type is determined by:

- **Section name** (folder name in `content/`)
- **Type parameter** (set in front matter with `cascade.type` or `type`)

### Built-in Types:

- `docs` - Documentation pages (with sidebar)
- `blog` - Blog posts (with date, authors, tags)
- `default` - Regular pages (no sidebar by default)

## Template Mapping

### 📚 **Docs Type** (`type: docs`)

**Content Location:** `content/docs/` or any section with `cascade.type: docs`

**Templates Used:**

- **Single pages:** `layouts/docs/single.html`
- **List pages:** `layouts/docs/list.html`

**Features:**

- ✅ Sidebar navigation enabled
- ✅ Breadcrumb navigation
- ✅ Table of contents
- ✅ Previous/Next page navigation
- ✅ Last updated date

**Example:**

```yaml
# content/docs/guide/configuration.md
---
title: Configuration
---
```

### 📝 **Blog Type** (`type: blog`)

**Content Location:** `content/blog/` or any section with `cascade.type: blog`

**Templates Used:**

- **Single posts:** `layouts/blog/single.html`
- **List pages:** `layouts/blog/list.html`

**Features:**

- ❌ Sidebar disabled (placeholder shown)
- ✅ Publication date displayed
- ✅ Author information
- ✅ Tags support
- ✅ Blog-style pagination
- ✅ "Read more" links in listing

**Example:**

```yaml
# content/blog/my-post.md
---
title: My Blog Post
date: 2024-01-01
authors:
  - name: John Doe
    image: /images/author.jpg
tags: [hugo, blog]
---
```

### 📄 **Default Type** (no type specified)

**Content Location:** Any section without a specific type

**Templates Used:**

- **Single pages:** `layouts/single.html`
- **List pages:** `layouts/list.html`

**Features:**

- ❌ Sidebar disabled
- ❌ No breadcrumb (or disabled)
- ✅ Simple centered title
- ✅ Basic content rendering

**Example:**

```yaml
# content/about.md
---
title: About Us
---
```

### 🏠 **Homepage**

**Template:** `layouts/home.html`

**Features:**

- ❌ Sidebar disabled
- ✅ Centered title
- ✅ Homepage content

## Setting Content Type

### Method 1: Section Name

- `content/docs/` → automatically uses `docs` type
- `content/blog/` → automatically uses `blog` type

### Method 2: Cascade in `_index.md`

```yaml
# content/chinese/_index.md
---
title: Chinese Section
cascade:
  type: docs # All pages in this section become "docs" type
---
```

### Method 3: Front Matter

```yaml
# content/my-page.md
---
title: My Page
type: docs # This specific page uses docs type
---
```

## Base Template

**File:** `layouts/baseof.html`

This is the **wrapper template** that all other templates extend. It provides:

- HTML structure (`<html>`, `<head>`, `<body>`)
- Navbar
- Footer
- Scripts
- The `{{ block "main" . }}` where page content is inserted

All other templates define the `main` block, which gets inserted into `baseof.html`.

## Key Differences Summary

| Feature      | Docs            | Blog                | Default        |
| ------------ | --------------- | ------------------- | -------------- |
| Sidebar      | ✅ Enabled      | ❌ Disabled         | ❌ Disabled    |
| Breadcrumb   | ✅ Enabled      | ✅ Enabled          | ❌ Disabled    |
| Date Display | ✅ Last updated | ✅ Publication date | ❌ None        |
| Authors      | ❌ No           | ✅ Yes              | ❌ No          |
| Tags         | ✅ Yes          | ✅ Yes              | ❌ No          |
| Pagination   | ✅ Prev/Next    | ✅ Blog style       | ❌ No          |
| Title Style  | Simple          | Large centered      | Large centered |

## Customizing Templates

You can override any template by creating a file with the same name in your `layouts/` folder. Hugo will use your custom template instead of the theme's default.

Example: To customize docs pages, create `layouts/docs/single.html` in your site (not in the theme).
