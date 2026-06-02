# bidiom.com

A clean, modern landing page for **Bidiom** — Marketplace User Interface Solutions.

## The Site

- Single-file static HTML landing page (`index.html`)
- Uses Tailwind via CDN + Font Awesome for a polished, professional look with zero build step
- Fully responsive, accessible, and fast
- Sections: Hero, Solutions, Trust stats, Expertise, Approach, CTA, Footer

## Local Development

Just open `index.html` directly in a browser.

For a local server (recommended):

```bash
# Python
python -m http.server 8000

# Or Node
npx serve .
```

## Deployment (GitHub + Vercel + Dreamhost)

This project is designed to be deployed via **Vercel** while living in **GitHub**, with the custom domain `bidiom.com` managed through **Dreamhost**.

The GitHub repository has already been created and the initial landing page pushed:

**https://github.com/jspeaks/bidiom**

### Recommended Flow

1. **Import into Vercel** (your next step)
   - Go to [https://vercel.com/jspeaks-projects](https://vercel.com/jspeaks-projects)
   - Click **Add New Project** → **Import Git Repository**
   - Select the `bidiom` repo (jspeaks/bidiom)
   - Framework Preset: **Other** (or leave as "Not configured")
   - Root Directory: leave as `/`
   - Build Command: (leave blank)
   - Output Directory: (leave blank)
   - Click Deploy

2. **(Already done)** The code is on GitHub main branch.
   - Go to [https://vercel.com/jspeaks-projects](https://vercel.com/jspeaks-projects)
   - Click **Add New Project** → **Import Git Repository**
   - Select your `bidiom` repo
   - Framework Preset: **Other** (or leave as "Not configured")
   - Root Directory: leave as `/`
   - Build Command: (leave empty)
   - Output Directory: (leave empty — Vercel will serve root `index.html`)
   - Deploy

   You will immediately get a `*.vercel.app` preview URL.

3. **Add your custom domain in Vercel**
   - In your Vercel project, go to **Settings → Domains**
   - Add `bidiom.com`
   - Vercel will show you the exact DNS instructions for your domain.

   Two main options will be presented:

   **Option A — Vercel Nameservers (cleanest for most people)**
   - Vercel gives you `ns1.vercel-dns.com` and `ns2.vercel-dns.com`
   - At Dreamhost (you're already on the nameservers panel), change the nameservers for bidiom.com to Vercel's.
   - **Important**: If you currently have email (MX records), subdomains, or other services at Dreamhost, you must first recreate equivalent DNS records inside Vercel's DNS dashboard *before* switching nameservers.
   - After switching, Vercel will automatically issue SSL and handle everything.

   **Option B — Keep Dreamhost nameservers + add records**
   - Keep using Dreamhost's nameservers.
   - Set the domain to **DNS Only** (required for apex A records pointing elsewhere — see Dreamhost help).
   - Add these records (Vercel will show the precise values):
     - **A record** for apex (`@` or blank host) → `76.76.21.21`
     - **CNAME** for `www` → the value Vercel provides (e.g. `cname.vercel-dns.com` or a project-specific hash)

4. **Configure at Dreamhost**
   - You're currently looking at: https://panel.dreamhost.com/?tree=domain.names#/domains/bidiom.com/nameservers
   - Decide between the two options above.
   - For record-based setup, you will also need the DNS settings page (Manage Websites → three dots → DNS Settings).

5. **Verify**
   - Use https://www.whatsmydns.net/ to check propagation for both `bidiom.com` and `www.bidiom.com`
   - Vercel will show the domain as "Valid Configuration" once DNS and SSL are ready.
   - Add a redirect from `www` → apex (or vice versa) in Vercel Domains settings if desired.

### Useful Vercel Docs (follow these when adding the domain)

- https://vercel.com/docs/domains/working-with-domains/add-a-domain
- https://vercel.com/docs/domains/working-with-nameservers

### Optional: vercel.json

For future-proofing you can add a `vercel.json` (example included below if you want clean rewrites or headers later).

## Next Steps / Ideas

- Replace the placeholder stats and testimonials with real ones.
- Add actual case studies or a simple portfolio section.
- Connect a real contact form (Vercel Forms, Formspree, or Resend + API route — though for pure static you can stay with `mailto:` for now).
- Add a `/blog` or other static pages later (Vercel will still work great).
- Add Open Graph / social meta tags (easy win).

## License

Private / proprietary for Bidiom.

---

Questions? Start by deploying the static site to Vercel first (you'll have a live URL in < 2 minutes), then tackle the domain config while the preview is live. This order makes DNS changes much less stressful.
