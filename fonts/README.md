# Fonts

Two files go here, both woff2, both subset to latin:

```
bricolage-grotesque-800.woff2   headings and numerals
inter-tight-400.woff2           body text
inter-tight-600.woff2           bold body text
```

The `@font-face` rules in `index.html` and `privacy/index.html` already
point at exactly these names, so dropping the files in is the whole job.

Until they are here the pages fall through to the platform's own sans
(`ui-sans-serif, system-ui, …`). That is deliberate: the site must never
fetch a font from a third party, so a missing file degrades rather than
reaching for fonts.googleapis.com. **Do not replace the `@font-face` rules
with a Google Fonts link** — it would put a request to Google on the page
that hosts the privacy policy, and the policy says this site collects
nothing.

Subsetting, if you have the full families as .ttf or .otf:

```bash
pip install fonttools brotli
pyftsubset BricolageGrotesque-ExtraBold.ttf \
  --unicodes="U+0000-00FF,U+2018,U+2019,U+201C,U+201D,U+2013,U+2014,U+2192,U+00D7,U+00F7,U+2212" \
  --layout-features="kern,liga,tnum" --flavor=woff2 \
  --output-file=bricolage-grotesque-800.woff2
```

Keep `U+00D7` (×), `U+00F7` (÷), `U+2212` (the true minus) and `U+2192` (→):
the landing page draws a round of the game with them.
