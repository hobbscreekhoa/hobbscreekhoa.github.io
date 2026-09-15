# The Homestead on Hobbs Creek — HOA Website

Static one-page site. No build step, no framework, no dependencies.
`index.html` is the whole site; `docs/` holds the governing documents.

---

## For board members: how to update the site

**Posting new meeting minutes**

1. Open the HOA's **"PUBLIC — Posted on Website"** folder in Google Drive.
2. Drag the PDF in.
3. Open the **Meeting Minutes** Google Sheet and add one row: `Date`, `Title`, `Link`.

That's it. The website picks it up automatically. You never edit the website itself.

> ⚠️ Anything placed in that Drive folder becomes **publicly visible on the internet
> immediately**. Never put member rosters, delinquency lists, violation letters, or
> anything with residents' personal information in it. Rule of thumb: if you wouldn't
> staple it to the mailbox kiosk, it doesn't go in the folder.

**Changing the meeting day/time** — that text lives in `index.html`; ask whoever
maintains the site. It changes rarely enough not to be worth wiring up.

---

## For whoever maintains the site

### Wiring up the minutes

Edit the `CONFIG` block at the top of the `<script>` in `index.html`:

```js
var CONFIG = {
  minutesSheetCsv:  '',   // Sheet → File → Share → Publish to web → CSV
  minutesFolderUrl: ''    // the public Drive folder, used as fallback
};
```

**"Publish to web" is a different switch from "Share".** A sheet that is only
link-shared returns **401** on the publish URL. You need File → Share →
*Publish to web*, not just the Share dialog.

Sheet columns must be, in order: **Date | Title | Link**

Behaviour is deliberately fail-safe:

| State | What visitors see |
|---|---|
| Sheet configured and reachable | The list of minutes, styled like the rest of the page |
| Sheet unreachable or malformed | Plain "Browse all meeting minutes →" link to the Drive folder |
| Nothing configured | "Minutes are available on request — email the board" |

It never renders an error and never renders an empty list. If Google changes
something, the page quietly degrades instead of breaking.

### Deploying to GitHub Pages

1. Push to a repository.
2. Settings → Pages → deploy from branch, root.
3. For the custom domain, add a `CNAME` file containing `hobbscreekhoa.org`,
   then Settings → Pages → Custom domain, and tick **Enforce HTTPS**.
4. In GoDaddy DNS, point the apex `A` records at GitHub's Pages IPs and the
   `www` CNAME at `<org>.github.io`.

> ⚠️ **Do not touch the `MX` or `TXT` records.** They carry the HOA's Google
> Workspace email. Changing them breaks mail for the whole association.
> Only `A` and `CNAME` records need to change.

`.nojekyll` is present so GitHub Pages serves files as-is.

### Notes

- Governing documents live in `docs/` on purpose — they are small, effectively
  permanent, and too important to depend on an outside host.
- The site was rebuilt from a GoDaddy Website Builder v7 site that could not be
  made mobile-friendly and had no SSL certificate.

---

## Icon credits

Icons are inlined as SVG (no external requests, nothing to load at runtime).

- Document and envelope icons: [Lucide](https://lucide.dev) — ISC License
- Facebook and Google Forms marks: [Simple Icons](https://simpleicons.org) — CC0 1.0

The Facebook and Google Forms marks are trademarks of their respective owners
and are used here only to label links pointing to the association's own
Facebook group and Google Form, which is their intended use.
