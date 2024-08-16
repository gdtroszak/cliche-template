---
title: usage
meta_description: cliche usage
---

# usage

```bash
Usage: cliche [OPTIONS] <CONTENT>

Arguments:
  <CONTENT>  Directory containing the site's content

Options:
      --header <HEADER>  Path to the site's header [default: header.md]
      --footer <FOOTER>  Path to the site's footer [default: footer.md]
      --style <STYLE>    Path to the site's stylesheet [default: style.css]
  -o, --output <OUTPUT>  Site output directory. Will be created if it doesn't already exist [default: _site]
      --domain <DOMAIN>  The domain of the site, used for generating full URLs in the sitemap. If not provided, a sitemap will not be generated
  -h, --help             Print help
  -V, --version          Print version
```

## Details

### Add a header file (optional)

```markdown
<!-- header.md -->

# my awesome website

<nav>

[home](contents/index.md)
[about](contents/about.md)
[whatever](contents/a/secret/path/whatever.md)

</nav>
```

### Add a footer file (optional)

```markdown
<!-- footer.md -->

[Contact](fake@gmail.com) | [Github](https://github.com/gdtroszak/cliche)
```

### Add some content

Create a directory for your content and add some files to it. Here's an example
that shows the URL paths to each page.

```bash
.
└── content/
    ├── index.md              /
    ├── static/
    │   └── image.jpg         /static/image.jpg
    ├── food/
    │   ├── index.md          /food
    │   ├── coffee.md         /food/coffee.html
    │   └── bread/
    │       ├── sourdough.md  /food/bread/sourdough.html
    │       └── wheat.md      /food/bread/wheat.html
    └── bikes/
        └── gravel.md         /bikes/gravel.html
```

Maybe I'd want my homepage to link to a few other pages.

```markdown
<!-- content/index.md -->

---
title: my amazing website
meta_description: a website about me and all the things I like.
---

- [food](./food/index.md)
- [gravel biking](content/bikes/gravel.md)
```

A few things to note here:

1. You can optionally add a title and meta_description in front-matter. This
   will be used in the `meta` tags for the page.
2. Links to other content can either be relative to the file itself or
   the root of your project. Use a text editor with a Markdown LSP. It'll make this
   really easy.

### Add some style (optional)

```css
/*style.css */

html {
    ...
}

body {
    ...
}
```

I'd recommend that you just copy one of the many [classless](https://github.com/dbohdan/classless-css)
options available.

You can add classes by throwing a bunch of HTML all over your Markdown, but that
probably won't end well.

### Run it

```bash
cliche ./content
```

Your site should get spit out to a `_site` directory. If you took advantage
of using `index.md`'s to generate more canonical URL paths, you'll need to serve
the site. Something like [simple-http-server](https://github.com/TheWaWaR/simple-http-server)
is perfect for that.

```bash
simple-http-server -i --nocache ./_site
```
