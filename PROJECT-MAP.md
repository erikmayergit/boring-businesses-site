# PROJECT-MAP — boring-businesses-site

The **Boring Businesses LLC** company website — built to unblock the Apple Developer Program enrollment for Muslim Matching. As of **2026-06-21: LIVE with HTTPS at https://boringbusinesses.info**, served by GitHub Pages **behind Cloudflare** (Cloudflare provides the TLS cert; GitHub's own cert was permanently stuck).

## Architecture (final)
- **Source (local):** `~/Desktop/boring-businesses-site` (this folder). Plain static HTML/CSS, no build. Git remotes: `fresh` → live repo, `origin` → old repo (superseded).
- **Live repo / origin:** `github.com/erikmayergit/boringbusinesses` (public) — GitHub Pages, branch `main`, `/`, `CNAME = boringbusinesses.info`. Serves the content.
- **Old repo:** `github.com/erikmayergit/boring-businesses-site` — Pages **disabled**, superseded (local dir's `origin` still points here).
- **DNS + TLS proxy:** **Cloudflare** (free). Nameservers `joaquin.ns.cloudflare.com` / `mckinley.ns.cloudflare.com`. SSL/TLS mode **Full** + **Always Use HTTPS**. Cloudflare issues the edge cert (Google Trust Services) → green padlock.
- **Why Cloudflare (not pure GitHub like the other sites):** GitHub Pages' Let's Encrypt cert for this domain is **permanently stuck at state "new."** The domain has a heavy prior-hosting history (104 Google-Trust-Services certs for apex/www/api/app/email until 2026-06-12) that wedges GitHub's cert pipeline. GitHub's own support triage confirmed "stuck backend job, manual fix only." Ticket **#4499476** filed; moot now that Cloudflare fronts TLS.

## DNS records (now managed in Cloudflare)
- `A @` → 185.199.108–111.153 (GitHub Pages) — **Proxied (orange)** ← this is what delivers HTTPS
- `CNAME www` → erikmayergit.github.io — **Proxied**
- **Email — PrivateEmail, MUST stay DNS-only (grey):** `MX` mx1/mx2.privateemail.com · `CNAME` mail/autoconfig/autodiscover → privateemail.com · `SRV _autodiscover` · `TXT v=spf1 include:spf.privateemail.com ~all`. → `contact@boringbusinesses.info` is a real mailbox (proxying these would break mail).

## Pages
`/` index · `/about.html` · `/products.html` (Muslim Matching only) · `/contact.html` · `styles.css` · `CNAME`.

## Deploy / operate
```bash
cd ~/Desktop/boring-businesses-site
# edit files, then:
git push fresh main      # deploys to the live repo (erikmayergit/boringbusinesses)
# if an update doesn't show, purge cache in the Cloudflare dashboard
```
- Do NOT re-enable the old repo's Pages or toggle the GitHub custom domain — irrelevant now (Cloudflare owns TLS).
- Do NOT proxy the email CNAMEs in Cloudflare (keep grey) or mail breaks.

## What's done
- 4-page site live with valid HTTPS (Cloudflare / Google Trust Services), http→https redirect, www works.
- Email intact (PrivateEmail records kept DNS-only through the Cloudflare migration).
- Apple enrollment **7L9Q9U4V8N** resubmitted → **pending** (auto-rejection stopped).

## What's NOT done / watch
- **Apple review outcome** — pending. If it bounces again, fallback = make the WHOIS registrant publicly read "Boring Businesses LLC" (the "domain associated with your organization" check).
- **GitHub ticket #4499476** — open but moot; safe to close.

## History
2026-06-18/19 built + deployed (GitHub Pages) · 2026-06-19→21 GitHub cert never issued → exhausted every fix → Cloudflare. See session logs `2026-06-19-boring-businesses-site-apple-enrollment-unblock` and `2026-06-21-boringbusinesses-https-cloudflare-apple`, and `GITHUB-SUPPORT-TICKET.md`.
