# arithmo-app.github.io

The Arithmo website: one landing page, the privacy policy, and `app-ads.txt`.
Static files only — GitHub Pages runs no build step here, and there is nothing
to install, compile or deploy. Push to `main` and it is live.

**This repo is separate from the app on purpose.** Nothing here imports from
the Flutter project, and nothing in the Flutter project reads from here. The
images in `img/` were generated once from the app's own assets and committed;
regenerating them is a manual copy, not a pipeline.

## What it does, in priority order

1. **Hosts the privacy policy** at `https://arithmo-app.github.io/privacy/`.
   Google Play and the App Store each need a live URL, and it has to still
   resolve years from now.
2. **Serves `app-ads.txt`**, so AdMob can verify that ads bought against
   Arithmo are legitimately ours.
3. **Is a shopfront** — what the game is, and where to get it.

## The URL matters

The policy URL goes into three store forms and should stay short and stable:

```
https://arithmo-app.github.io/privacy/
```

That URL only exists if this repo is named **`arithmo-app.github.io`** under
the GitHub account **`arithmo-app`**. A repo named anything else is served
from `https://arithmo-app.github.io/<repo-name>/`, which would change the
policy URL and every store form that already has it. If the account name
differs, fix the repo name first and tell me — the canonical tags, the
`og:url` and this README all name it.

A real owned domain (arithmo.com is named in the app's `SPEC.md` §0b) is the
more robust long-term home: add a `CNAME` file with the bare domain, point
the DNS at GitHub Pages, and update the URLs in the two HTML files. Do it
*before* the first store submission if you can — changing a live privacy URL
afterwards means editing forms at both stores.

## Before the first Play submission

- [ ] **Name the data controller.** `privacy/index.html` says
      `[TO BE COMPLETED]` where a real person or registered entity must go.
      A privacy policy naming nobody as controller fails its purpose under
      the GDPR — "Arithmo" or "Anidote" alone is not a controller; a legal
      name is ("Jean Dupont, trading as Anidote", or a registered company
      with its number). It is the one thing on the page that cannot ship
      blank.
- [ ] **Paste the real `app-ads.txt` line** from AdMob → Apps → Arithmo →
      app-ads.txt, and set `https://arithmo-app.github.io` as the developer
      website on the Play listing. The crawler finds this file *through* that
      field; without it, the file is never read.
- [ ] **Drop the two fonts into `fonts/`** (see `fonts/README.md`).
- [ ] **Replace the Play badge placeholder** in `index.html` with Google's
      own badge artwork and the real listing URL. The placeholder is
      deliberately not an imitation of it — Google requires its own image.

## The rule about the policy

**The policy and the Play Data Safety form must change together, in the same
sitting.** They are two descriptions of the same facts, and a store reads
them against each other. If an SDK is added or removed from the app, this
page and that form are both wrong until both are updated — an inaccurate
policy is worse than a thin one.

Right now the policy describes three third parties: AdMob, RevenueCat,
Firebase Crashlytics and Firebase Remote Config. **One of those is not in the
app yet** — RevenueCat, blocked on the Play product (`AUDIT.md` B1 in the app
repo). Over-declaring is the safer direction, but the two documents must
agree on the day of submission, so check the shipped build against this list
before you fill the Data Safety form.

**Declare from the binary, not from the prose.** Firebase Analytics was
described here and on the page while it was never a dependency; it has been
removed from both, and the page now says plainly that no analytics service is
used. If one is ever added, this file, the page and `docs/DATA_SAFETY.md` in
the app repo change in the same commit as the line in `pubspec.yaml`.

To edit the policy: it is plain HTML in `privacy/index.html`, one `<h2>` per
section, with the text matching the source `privacy.md` line for line. Change
the *"Last updated"* date in the same edit — that date is the only evidence a
reader has that the page is current.

## Constraints this site keeps

- **No tracking of any kind.** No analytics, no cookies, no embeds, no fonts
  from a third party. The site that hosts the privacy policy must not itself
  be a privacy problem — and it is what lets the policy say, honestly, that
  this site collects nothing.
- **No request leaves the origin.** Everything is inline or in `/fonts/`,
  `/img/`. The only external URLs anywhere are `<a href>` links to the third
  parties' own policies, which are links a reader chooses to follow, not
  requests the page makes.
- **Every page under 100 KB** excluding fonts. Both are well under: the CSS
  is inline, there is no JavaScript at all, and the animated demo on the
  landing page is CSS keyframes.
- **No cognitive or health claim, anywhere.** Nothing about memory, focus,
  concentration, intelligence, IQ, school or work performance, cognitive
  decline, dementia, ADHD, "training your brain", "scientifically proven", or
  neuroplasticity. The FTC fined Lumosity $2M over exactly these claims and
  the evidence does not support them: cognitive training reliably improves
  the trained task and does not generalise. What the site may say is narrower
  and true — the player gets faster at mental arithmetic, and Progress shows
  them their own measured times. Claims about a user's own data need no
  substantiation beyond that data.

## Structure

```
index.html            the landing page, CSS inline
privacy/index.html    the policy — the URL is /privacy/, do not nest it deeper
app-ads.txt           AdMob authorised sellers (placeholder)
fonts/                woff2, same origin, see fonts/README.md
img/                  icon, favicons, screenshots, og preview
README.md             this file
```

`CNAME` is deliberately absent until a real domain exists.
