# Mellea Landing Page

Static landing page for [Mellea](https://github.com/generative-computing/mellea), served via GitHub Pages from the `docs/` directory.

## Structure

```
docs/
├── index.html          # Single-page landing site (HTML + inline CSS/JS)
├── llms.txt            # Plain-text project summary for AI crawlers
├── mellea-logo.svg     # Logo asset
├── with-mellea.png     # Comparison slider "after" image
├── without-mellea.png  # Comparison slider "before" image
├── robots.txt          # Crawler directives
└── sitemap.xml         # Sitemap for search engines
```

## Deployment

The site is deployed automatically via GitHub Pages from the `docs/` folder on the `main` branch. The custom domain `mellea.ai` should be configured in the repository's Pages settings (and a `CNAME` file added if needed).

## Dynamic Elements

The landing page fetches live data from external APIs on every page load:

| Source | Data | API calls |
|--------|------|-----------|
| GitHub API | Star count, latest release, last commit time, contributor count + avatars, 12-week commit sparkline | 5 |
| PyPI API | Latest package version | 1 |

### Known Limitations

- **GitHub API rate limit**: Unauthenticated requests are limited to **60 requests per hour per IP**. With 5 GitHub API calls per page load, a single visitor can load the page ~12 times/hour before hitting the limit. Under normal traffic this is fine, but a traffic spike (e.g. launch announcement, Hacker News post) could cause the dynamic elements to stop loading temporarily.
- **Graceful degradation**: All dynamic elements hide cleanly when API calls fail — the page remains fully functional with static content only. No errors are shown to visitors.
- **Future improvement**: If rate limiting becomes a problem, the API data could be fetched at build time via a GitHub Action and baked into the HTML, eliminating runtime API calls entirely.

### OG Image

The Open Graph / Twitter Card image is served from the `generative-computing/docs` repo (`https://raw.githubusercontent.com/generative-computing/docs/main/images/hero-dark.png`). If that image is moved or removed, the social sharing preview will break. Consider hosting a dedicated OG image in this repo if the external dependency becomes unreliable.
