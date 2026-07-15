# GitHub Support ticket — Pages HTTPS cert stuck at "new"

**Status:** ✅ SUBMITTED 2026-06-20 — **ticket #4499476** (open, account `erikmayergit`, category Repositories → Repository features, type "Errors, problems"). GitHub's own AI triage confirmed the diagnosis verbatim ("stuck backend cert job; only resolution is manual GitHub intervention"). Awaiting Pages/Certificates team.
**Where it was submitted:** https://support.github.com/contact
**Drafted:** 2026-06-20. Ticket body below (kept for the record).

---

**Subject:** GitHub Pages custom-domain HTTPS certificate stuck at "new" — never provisions (boringbusinesses.info)

Hi GitHub Support,

A GitHub Pages custom-domain HTTPS certificate has been stuck in the **"new"** state ("This domain was recently added. The certificate request process will begin shortly.") for **2+ days** and never provisions. I've exhausted standard troubleshooting and believe it needs manual intervention on your side.

**Details**
- Account: `erikmayergit`
- Repository: `erikmayergit/boringbusinesses` (public) — branch `main`, path `/`. Pages is enabled and the site builds and serves over HTTP correctly.
- Custom domain: `boringbusinesses.info` — **verified** at the account level (shows "Verified" under Settings → Pages).
- Pages API shows `https_certificate.state = "new"` and `https_enforced = false`; the state never advances to `issued`.

**DNS (registrar Namecheap, BasicDNS) — confirmed correct:**
- `A @` → 185.199.108.153 / .109.153 / .110.153 / .111.153
- `CNAME www` → `erikmayergit.github.io`
- No `CAA` records; DNSSEC disabled; `http://boringbusinesses.info` serves the site (HTTP 200).

**Troubleshooting already performed (cert stayed at "new" through all of it):**
1. Removed and re-added the custom domain several times.
2. Fully disabled and re-enabled GitHub Pages.
3. Re-deployed to a brand-new repository.
4. Verified the domain at the account level via DNS TXT challenge (succeeded).
5. Waited 24h+ with no attempts, to rule out Let's Encrypt rate limits.

**Likely relevant:** this domain was previously hosted on another platform — certificate-transparency logs show certs from Google Trust Services for the apex + `www`/`api`/`app` subdomains rotating until ~2026-06-12. It may carry a stale certificate/domain association on GitHub's side. For comparison, another custom domain on this same account (`xn--lampengrn-x9a.de`) provisions HTTPS with no issue — so the problem is specific to this one domain.

**Request:** Please investigate why the Let's Encrypt certificate order for `boringbusinesses.info` won't progress past "new," clear any stale association, and re-provision the certificate.

Thank you,
Erik
