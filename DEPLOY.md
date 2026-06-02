# Deploy AIS MMT-RFP Codelabs to Cloudflare Pages

## 📦 Folder Contents

```
cf-deploy/
├── index.html                          ← Landing page
├── OCI_NonProd_Codelab.html
├── OCI_Prod_Codelab.html
├── _headers                            ← Cache + security headers
├── _redirects                          ← Friendly URLs (/nonprod, /prod)
├── wrangler.toml                       ← Cloudflare config
└── resource/
    ├── architecture_diagram_oci.svg
    ├── architecture_diagram_oci.png
    ├── architecture_diagram_oci_nonprod.svg
    └── architecture_diagram_oci_nonprod.png
```

---

## 🚀 Deployment Options

### Option A: Wrangler CLI (Recommended · Fastest)

**Prerequisites:**
- Cloudflare account (free tier OK)
- Node.js installed

**Steps:**

```bash
# 1. Install Wrangler CLI
npm install -g wrangler

# 2. Login to Cloudflare
wrangler login
# Browser opens · authorize the CLI

# 3. Deploy from this folder
cd cf-deploy/
wrangler pages deploy . --project-name=ais-mmt-codelabs

# That's it! You'll get a URL like:
# https://ais-mmt-codelabs.pages.dev
```

**First-time setup creates the project automatically.** Each subsequent run updates the existing deployment.

---

### Option B: Cloudflare Dashboard (Drag & Drop)

1. Go to <https://dash.cloudflare.com>
2. Navigate: **Workers & Pages** → **Create application** → **Pages** → **Upload assets**
3. Project name: `ais-mmt-codelabs`
4. Drag the entire `cf-deploy/` folder into the upload area
5. Click **Deploy site**

Done in ~2 minutes. URL: `https://ais-mmt-codelabs.pages.dev`

---

### Option C: Git Integration (Best for CI/CD)

```bash
# 1. Push cf-deploy/ to a GitHub/GitLab repo
cd cf-deploy/
git init
git add .
git commit -m "Initial codelabs deployment"
git remote add origin https://github.com/AIS/mmt-codelabs.git
git push -u origin main

# 2. Connect in Cloudflare Dashboard
# - Workers & Pages → Create → Pages → Connect to Git
# - Select your repo
# - Build settings: leave empty (no build needed)
# - Output directory: /
# - Save & Deploy
```

After this, every `git push` auto-deploys.

---

## 🌐 Custom Domain (Optional)

After deployment, attach a custom domain like `codelabs.ais.co.th`:

1. Cloudflare Dashboard → Workers & Pages → ais-mmt-codelabs → **Custom domains**
2. **Set up a custom domain** → enter `codelabs.ais.co.th`
3. Add the DNS record at AIS's DNS provider (or use Cloudflare DNS)
4. Wait ~5 minutes for SSL cert provisioning

**Result:**
- `https://codelabs.ais.co.th` → Landing page
- `https://codelabs.ais.co.th/nonprod` → Non-Prod codelab
- `https://codelabs.ais.co.th/prod` → Prod codelab

---

## 🔧 Friendly URLs (Configured via `_redirects`)

| Short URL | Destination |
|---|---|
| `/` | Landing page |
| `/nonprod` | OCI_NonProd_Codelab.html |
| `/prod` | OCI_Prod_Codelab.html |
| `/codelab` | OCI_NonProd_Codelab.html (default) |

---

## 🛡 Security Headers (Configured via `_headers`)

- `X-Content-Type-Options: nosniff`
- `X-Frame-Options: SAMEORIGIN`
- `Referrer-Policy: strict-origin-when-cross-origin`
- Cache: 5 min for HTML · 24 hr for diagrams

---

## 📊 Expected Cost

**Cloudflare Pages Free tier:**
- ✅ Unlimited bandwidth
- ✅ 500 builds/month
- ✅ Custom domain + SSL free
- ✅ Global CDN (300+ POPs)
- ✅ DDoS protection

**Cost for this deployment: $0/month** ✓

---

## 🔍 Verify After Deploy

```bash
# Test landing page
curl -I https://ais-mmt-codelabs.pages.dev/

# Test friendly redirects
curl -I https://ais-mmt-codelabs.pages.dev/nonprod
curl -I https://ais-mmt-codelabs.pages.dev/prod

# Test diagrams load
curl -I https://ais-mmt-codelabs.pages.dev/resource/architecture_diagram_oci.svg
```

Expected: all return `200 OK` (or `301` for redirects)

---

## 🔄 Update Workflow

After making changes to codelab HTML files:

```bash
# Re-copy updated files
cp ../OCI_NonProd_Codelab.html ../OCI_Prod_Codelab.html ./
cp ../resource/architecture_diagram_oci*.{svg,png} resource/

# Re-deploy
wrangler pages deploy . --project-name=ais-mmt-codelabs
```

Cloudflare keeps history of all deployments · can roll back if needed.

---

## 📝 Notes

- **No backend needed** — pure static HTML/CSS/JS
- **localStorage** keeps user progress in their browser (not server-side)
- **All assets self-contained** — no external CDN dependencies (except optional Prism.js which has fallback)
- **Mobile-responsive** — works on phones/tablets

---

## ❓ Troubleshooting

| Issue | Solution |
|---|---|
| `wrangler login` fails | Use `wrangler login --browser=false` for headless |
| Build fails on Cloudflare | Check `_headers` and `_redirects` syntax (no leading spaces) |
| Custom domain not resolving | Wait 10 min for DNS propagation · check NS records |
| 404 on `/nonprod` | Verify `_redirects` file deployed (case-sensitive) |
| Old version cached | Hard refresh (Ctrl+Shift+R) or wait 5 min |

---

**Ready to deploy!** Pick Option A (Wrangler) for fastest deployment.
