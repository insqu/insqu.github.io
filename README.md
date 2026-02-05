# INSQU Website (GitHub Pages)

Simple static website for INSQU using only:
- HTML
- CSS
- JavaScript

No secrets, no backend required.

## Build Plan Checklist

### Phase 1: Messaging and Structure
- [x] Define core positioning and value proposition.
- [x] Create sections: Hero, Services, Expertise, Process, Contact.
- [x] Write copy focused on software consulting and bespoke delivery.

### Phase 2: Front-end Build
- [x] Keep files separated (`index.html`, `styles.css`, `script.js`).
- [x] Build responsive layout with clear calls-to-action.
- [x] Add mobile navigation and smooth scrolling behavior.

### Phase 3: Quality and Launch
- [x] Validate basic static rendering locally.
- [x] Deploy on GitHub Pages from the repository root.
- [x] Configure custom domain on GitHub + Namecheap DNS.

---

## Custom Domain Setup (Namecheap → GitHub Pages)

> Replace `yourdomain.com` with your real domain.

### 1) Configure GitHub Pages
1. In your repo, open **Settings → Pages**.
2. Under **Build and deployment**, set source to:
   - **Deploy from a branch**
   - Branch: `main` (or your default branch), folder: `/ (root)`
3. In **Custom domain**, enter `yourdomain.com` and save.
4. Check **Enforce HTTPS** once DNS is correctly propagated.

### 2) Configure Namecheap DNS
In Namecheap **Domain List → Manage → Advanced DNS**, add records:

For apex/root domain (`yourdomain.com`):
- `A` record → `@` → `185.199.108.153`
- `A` record → `@` → `185.199.109.153`
- `A` record → `@` → `185.199.110.153`
- `A` record → `@` → `185.199.111.153`

For `www` subdomain:
- `CNAME` record → `www` → `insqu.github.io`

Remove conflicting records for `@` or `www` if they exist.

### 3) Verify
- DNS can take a few minutes to 24–48 hours to fully propagate.
- After propagation, open:
  - `https://yourdomain.com`
  - `https://www.yourdomain.com`
- Confirm GitHub Pages shows the domain as active and HTTPS enabled.

## Local Preview
Run a local static server from the repo root:

```bash
python3 -m http.server 8000
```

Then open `http://localhost:8000`.


## Troubleshooting: "Not Found" on GitHub Pages

If you see a GitHub 404 page, run through this checklist:

1. **Repository name check**
   - For a user/org site, the repo must be exactly `insqu.github.io`.
2. **Pages source check**
   - In **Settings → Pages**, source must be your live branch and `/ (root)`.
3. **Custom domain check**
   - In **Settings → Pages**, ensure your exact domain is entered.
   - Wait for the green DNS check status.
4. **DNS check in Namecheap**
   - Keep only the 4 GitHub A records for `@` and one CNAME for `www`.
   - Remove conflicting `URL Redirect`, `A`, `AAAA`, or duplicate `CNAME` records.
5. **Propagation wait**
   - DNS can take up to 24–48 hours globally.
6. **Quick verify commands**

```bash
# Replace with your real domain
nslookup yourdomain.com
nslookup www.yourdomain.com
```

Expected result:
- `yourdomain.com` resolves to GitHub Pages IPs (`185.199.108.153` ... `.111.153`)
- `www.yourdomain.com` resolves to `insqu.github.io`

After DNS is correct, re-open **Settings → Pages** and enable HTTPS.
