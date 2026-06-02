# bidiom.com Landing Page Setup - TODO

**Date:** 2026-06 (approximate, based on session)  
**Project:** https://github.com/jspeaks/bidiom  
**Vercel:** https://vercel.com/jspeaks-projects (project: bidiom)  
**Dreamhost:** Domain bidiom.com, currently at DNS page for records.

## Current Status

- Static landing page (nice, simple, Tailwind CDN) is created and deployed.
- GitHub repo set up and connected to Vercel.
- Project successfully deployed on Vercel.
- Custom domains `bidiom.com` and `www.bidiom.com` added in Vercel (currently "Invalid Configuration" pending DNS).
- Live preview available on Vercel subdomain (e.g. `bidiom-*.vercel.app` — check Vercel dashboard for exact URL).
- Dreamhost tab open to DNS records editor: `https://panel.dreamhost.com/?tree=domain.dashboard#/site/bidiom.com/dns`
- **Blocker:** Cannot remove Unique IP on Dreamhost (support ticket opened with Dreamhost support).
- Preference: Keep Dreamhost fully managing email/MX records. Only route website traffic (apex + www) to Vercel. Do **not** switch nameservers.

## Completed

- [x] Created polished single-file `index.html` landing page for "Marketplace User Interface Solutions" (hero, solutions, expertise, approach, CTA, footer).
- [x] Added `vercel.json` for static hosting best practices.
- [x] Initialized git, created public GitHub repo `jspeaks/bidiom`, pushed code.
- [x] Imported repo to Vercel, deployed (framework: Other/static, no build).
- [x] Used dev-browser automation to add domains in Vercel and retrieve exact DNS requirements.
- [x] Navigated Dreamhost to the DNS records page for bidiom.com via automation.
- [x] Identified need for "DNS Only" + Unique IP removal before adding root A record.

## Pending / Next Steps

- [ ] Resolve Unique IP removal (support ticket open with Dreamhost).
- [ ] Set domain to "DNS Only" (Deactivate Website) in Dreamhost (required for custom root A record; explicitly does **not** affect email/MX).
- [ ] Add the required DNS records at Dreamhost (while keeping Dreamhost nameservers).
- [ ] (Optional) Clean up old Dreamhost web A records pointing to 205.196.223.101.
- [ ] Wait for DNS propagation.
- [ ] Refresh/validate domains in Vercel (they should go green, SSL auto-provisions).
- [ ] Test custom domain.
- [ ] Revisit and clean up TODO once live.

## Vercel DNS Requirements (exact from current Vercel Domains page)

**For `bidiom.com` (apex/root):**
- Type: **A**
- Name/Host: `@` (leave blank in Dreamhost — it adds @ automatically)
- Value: `216.198.79.1`  
  *(Recommended new IP due to expansion. The classic `76.76.21.21` will also continue to work.)*

**For `www.bidiom.com`:**
- Type: **CNAME**
- Name/Host: `www`
- Value: `31e51af5976fcd80.vercel-dns-017.com.`

**Important notes from Vercel:**
- Add these at your current DNS provider (Dreamhost).
- Do **not** switch to Vercel nameservers (we want Dreamhost to keep handling email).
- Propagation can take time — use https://www.whatsmydns.net/ to monitor.
- Old records (`cname.vercel-dns.com` / `76.76.21.21`) remain compatible.

Current Vercel Domains page (for reference): https://vercel.com/jspeaks-projects/bidiom/settings/domains

## Dreamhost DNS Configuration Steps (Manual, post-support-ticket)

You are already on the right page: `https://panel.dreamhost.com/?tree=domain.dashboard#/site/bidiom.com/dns`

From previous inspection, you will see:
- Custom Records (some existing subdomains)
- DreamHost Records (including `@ A 205.196.223.101`, `www A 205.196.223.101`, mail/ftp/etc.)
- Nameservers: Using DreamHost Nameservers (keep these!)

### Step-by-step:

1. **Resolve Unique IP**
   - Support ticket opened because "couldn't remove the unique IP".
   - Once support (or you) removes the Unique IP attached to bidiom.com, return to this DNS page.

2. **Set to DNS Only (Deactivate Website)**
   - In the A record form (or domain settings), you will see: "The website for this domain must be deactivated before root-level custom DNS records of this type may be added."
   - Click **Deactivate Website** / **Yes, Deactivate Website**.
   - Dreamhost note (from UI): "This will not deactivate or cancel the hosting plan itself. It does not delete hosted files nor does it remove any existing custom DNS records on the domain. **Other services, such as email and MX records, are also left intact.**"
   - The domain can be set back to Fully Hosted later from Manage Websites if needed.

3. **Add the A record (apex)**
   - Click **Add Record** → choose **A**.
   - Host: leave **blank** (Dreamhost adds `@` for root).
   - Points to: `216.198.79.1` (or `76.76.21.21`).
   - TTL: default is fine.
   - Click **Add Record**.

4. **Add the CNAME record (www)**
   - Click **Add Record** → choose **CNAME**.
   - Host: `www`
   - Points to: `31e51af5976fcd80.vercel-dns-017.com.`
   - Click **Add Record**.

5. **Clean up (recommended)**
   - Locate the old DreamHost web records:
     - `@ A 205.196.223.101`
     - `www A 205.196.223.101`
   - Delete them (or edit to the new Vercel values).
   - **Do not touch** mail.*, webmail, ftp, mysql, ssh, or any other non-web records.

6. Click **Refresh DNS** if available.

7. Monitor propagation (whatsmydns.net for both `bidiom.com` and `www.bidiom.com`).

8. Return to Vercel Domains page and click **Refresh** on the invalid entries. They should validate.

## Existing Dreamhost Records Snapshot (from automation)

(Leave most of these alone — only web apex/www need changing.)

- Various Custom Records (e.g. auctionos NS records, cullony CNAME)
- DreamHost Records included:
  - @ A 205.196.223.101
  - ftp A 205.196.223.101
  - mail A ...
  - mailboxes A ...
  - mysql A ...
  - ssh A ...
  - webmail A ...
  - www A 205.196.223.101
  - etc.
- Nameservers: DreamHost (ns1.dreamhost.com, ns2..., ns3...)

## Quick Links

- GitHub: https://github.com/jspeaks/bidiom
- Vercel Project: https://vercel.com/jspeaks-projects/bidiom
- Vercel Domains: https://vercel.com/jspeaks-projects/bidiom/settings/domains
- Dreamhost DNS (current): https://panel.dreamhost.com/?tree=domain.dashboard#/site/bidiom.com/dns
- Dreamhost help (custom DNS): https://help.dreamhost.com/hc/en-us/articles/360035516812-Adding-custom-DNS-records
- Propagation checker: https://www.whatsmydns.net/

## Notes / Gotchas

- Email safety is the top priority — nameservers stay at Dreamhost.
- "Deactivate Website" / DNS Only is required for root A records pointing away from Dreamhost hosting.
- Unique IP removal was the immediate blocker (hence the support ticket).
- Once DNS is correct, Vercel will handle SSL automatically.
- The landing page is very lightweight (single HTML + CDNs) — easy to iterate later.
- If you want to resume browser automation: re-run dev-browser on the open tabs (Vercel + Dreamhost) and I can help fill forms, etc.

## After This Is Live

- Update the landing page content with real copy, case studies, contact form, etc.
- Add analytics, Open Graph images, etc.
- Consider adding a contact form (e.g. via Vercel or Formspree).
- Revisit README.md (it has some deployment notes).

---

**Revisit this file when the Dreamhost support ticket is resolved.**  
Run `cat TODO.md` or open it in your editor to pick up exactly where we left off.

If you update the DNS manually and want me to verify via the attached browser tabs later, just say so!