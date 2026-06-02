# AIS MMT-RFP Codelabs

Interactive learning codelabs สำหรับ deploy ระบบ Queue Management บน Oracle Cloud Infrastructure (OCI)

🔗 **Live site:** https://betask-mmt-codelabs.pages.dev (auto-deployed via Cloudflare Pages)

## 📚 Codelabs

| Codelab | Audience | Duration |
|---|---|---|
| [OCI Non-Prod Setup](OCI_NonProd_Codelab.html) | Dev/QA/UAT environments | ~2 hours |
| [OCI Prod Setup](OCI_Prod_Codelab.html) | Production deployment | ~3-4 hours |

## ✨ Features

- 🎨 **Architecture Progress Diagram** — เห็นภาพรวมระบบ · ส่วนที่ build แล้วมีสี · ส่วนที่ยังไม่ build เป็นสีเทา
- 📘 **NOTE** boxes — ข้อมูลที่ควรรู้
- ⚠️ **NOTICE** boxes — เตือนสำคัญ
- 💡 **TECHNIQUE** boxes — เทคนิคที่ควรเรียนรู้
- 🛑 **PROD WARNING** boxes — เตือนเฉพาะ production deployment
- 📋 **Step tracking** — บันทึก progress ผ่าน localStorage
- 🔗 **URL deep-linking** — `?step=N` resume ที่ step ใดก็ได้

## 🚀 Quick Access

| URL | Destination |
|---|---|
| `/` | Landing page |
| `/nonprod` | Non-Prod codelab |
| `/prod` | Prod codelab |

## 🛠 Tech Stack

- Pure static HTML/CSS/JavaScript (no build step)
- Inline SVG architecture diagrams
- localStorage for progress persistence
- Mobile-responsive

## 📂 Repository Structure

```
.
├── index.html                          ← Landing page
├── OCI_NonProd_Codelab.html
├── OCI_Prod_Codelab.html
├── _headers                            ← Cloudflare cache + security
├── _redirects                          ← URL aliases (/nonprod, /prod)
├── wrangler.toml                       ← Cloudflare config
├── DEPLOY.md                           ← Deployment guide
└── resource/                           ← Architecture diagrams
    ├── architecture_diagram_oci.svg
    ├── architecture_diagram_oci.png
    ├── architecture_diagram_oci_nonprod.svg
    └── architecture_diagram_oci_nonprod.png
```

## 🚀 Auto-Deploy via Cloudflare Pages

Connected to Cloudflare Pages. Every push to `main` triggers automatic deployment.

- **Production:** `main` branch → `https://betask-mmt-codelabs.pages.dev`
- **Preview:** Pull requests get unique preview URLs

## 📝 License

Internal use — AIS MMT-RFP project · BeTASK Solutions
