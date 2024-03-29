# Darkshredder

Darkshredder is minimalist Jekyll theme for running a personal site and blog running on Jekyll.<br>
For demo <a href="https://blogs.darkshredder.com" target="_blank" rel="noopener">blogs.darkshredder.com</a>

## Features

- [x] Light & Dark Mode support :waxing_crescent_moon:
- [x] Customizable (using `.scss`)
- [x] Responsive (desktop, tab and mobile)
- [x] Mobile First Design
- [x] SEO Optimized
- [x] Images of post Organized ([`jekyll-postfiles`](https://github.com/nhoizey/jekyll-postfiles))
- [x] Generate Sitemap ([`jekyll-sitemap`](https://github.com/jekyll/jekyll-sitemap))
- [x] RSS Feed ([`jekyll-feed`](https://github.com/jekyll/jekyll-feed))
- [x] Syntax Highlighter ([`rouge`](https://github.com/rouge-ruby/rouge))
- [x] Next & Previous Post
- [x] Comment layout, enable in frontmatter if you wish
- [x] Google analytics
- [x] HTML Minify ([`jekyll-compress-html`](https://github.com/penibelst/jekyll-compress-html))
- [x] W3C **Validated**
- [x] Lighthouse and PageSpeed **Passed**


## Backlogs

- [ ] Intergrated with PhotoSwipe.
- [ ] Add schema.org meta information.
- [ ] Transform class selector to BEM metodology.

## Installation

Run local server:

```bash
$ git clone https://github.com/darkshredder/my-blogs.git
$ cd my-blogs
$ bundle install
$ bundle exec jekyll serve
```

Navigate to `localhost:4000`. You're Welcome, Fork and be Stargazer.

## Limitation

- Since [`jekyll-postfiles`](https://github.com/nhoizey/jekyll-postfiles#compatibility) plugin isn't supported by github pages, this cause will make your site problems, path broken or post images won't show up, you can host alternatively using likes [netlify.com](https://netlify.com), [vercel.com](https://vercel.com), [azure.com](https://docs.microsoft.com/azure/static-web-apps/publish-jekyll) or [surge.sh](https://surge.sh) services, which support 3rd party.

