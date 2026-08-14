# Asilomar Bioelectronics Symposium — website

Static site for [asilomarbioelectronics.com](https://www.asilomarbioelectronics.com/), hosted on GitHub Pages. No build step, no frameworks — plain HTML + one CSS file.

## Editing

- Each page is one `.html` file in the repo root. Edit the text right in the file and push; GitHub Pages redeploys automatically in about a minute.
- Shared styles live in `css/style.css`. The header/nav and footer are repeated in each page — if you change the nav, change it in every `*.html` file (search for `site-nav`).
- Images live in `assets/img/`. Add a new speaker headshot there and reference it as `assets/img/name.jpg`.
- Yearly updates: `speakers.html`, `schedule.html`, `submission.html` (abstract deadlines + poster instructions), `registration.html` (rates + registration link), and add the finished year to `past.html`.

## Preview locally

Open `index.html` in a browser, or run a tiny server from this folder:

```
python3 -m http.server 8420
```

## Custom domain

To serve this at www.asilomarbioelectronics.com: in the repo's Settings → Pages, set the custom domain, then point the domain's DNS (currently at Squarespace) with a CNAME record for `www` to `<username>.github.io`. GitHub's docs: https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site
