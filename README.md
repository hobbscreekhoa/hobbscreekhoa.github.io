# The Homestead on Hobbs Creek — HOA Website

Static one-page site. No build step, no framework, no dependencies.
`index.html` is the whole site; `docs/` holds the governing documents.

---

## For board members: how to update the site

**Posting new meeting minutes**

Upload them to PayHOA under **Documents → Minutes**, the same as always. Nothing on
the website needs to change — it links to the portal rather than listing the files.

Same for financial reports, welcome letters, and anything else homeowners should have.

**When a homeowner says they cannot find the minutes**

They usually cannot get into the portal. The site invites them to email the board
about login or sign-up trouble, so expect those emails — send an invitation from
PayHOA, or help them reset their password.

**Changing the meeting day/time** — that text lives in `index.html`; ask whoever
maintains the site. It changes rarely enough not to be worth wiring up.

---

## For whoever maintains the site

Colors, type and component rules are in [DESIGN.md](DESIGN.md).

### Minutes and other homeowner documents

They live in PayHOA, behind a homeowner login, so the site cannot list them. Two
plain links point there instead — one row in **For Residents**, one line under
**Meetings** — both to `https://app.payhoa.com/auth/login`.

That URL is PayHOA's shared login page; there is no per-association address and no
usable deep link to the Documents tab (it redirects to the login and loses where you
were headed). If PayHOA ever gives the HOA its own subdomain, or the board turns on
PayHOA's public owner page, swap the two links and consider listing documents again.

Both places also tell homeowners without a login to email the board. Do not remove
that — new buyers and renters hit it constantly, and a bare login link is a dead end
for them.

An earlier version of this site pulled minutes from a public Google Drive folder via
a published Sheet. That code is gone. If minutes ever leave PayHOA, it is in the git
history (commit `64386dd` and earlier), but a single link to wherever they live is
almost certainly the better answer.

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
