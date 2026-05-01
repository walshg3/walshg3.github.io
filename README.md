# gregwalsh.tech

Source for my personal blog and portfolio at **[www.gregwalsh.tech](https://www.gregwalsh.tech)** — security engineering, PKI, and homelab notes.

## Stack

- **[Hugo](https://gohugo.io/)** — static site generator
- **[PaperMod](https://github.com/adityatelange/hugo-PaperMod)** — theme (git submodule)
- **[hugo-embed-pdf-shortcode](https://github.com/anvithks/hugo-embed-pdf-shortcode)** — PDF embedding (git submodule)
- **GitHub Pages + GitHub Actions** — built and deployed from `main` via `.github/workflows/gh-pages.yml`

## Local development

```bash
git clone --recurse-submodules https://github.com/walshg3/walshg3.github.io.git
cd walshg3.github.io
hugo server -D
```

The `--recurse-submodules` flag is required — the theme lives in `themes/PaperMod` as a submodule.

## Writing a post

```bash
hugo new content posts/my-post.md
```

Edit the front matter, drop `draft: true` to `false`, and push to `main`. The Actions workflow handles the rest.

## Custom domain

`CNAME` points the GitHub Pages site at `www.gregwalsh.tech`. DNS is managed in Cloudflare.
