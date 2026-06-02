# OCI Console Screenshot Capture Guide

This is the punch list for capturing the **78 screenshots** that the codelabs reference. The codelabs already have placeholders — once you drop the matching PNG into the right folder at the right filename, the striped "pending" card disappears and the screenshot renders.

- **Non-Prod codelab:** 44 shots → `cf-deploy/resource/screenshots/nonprod/`
- **Prod codelab:** 34 shots → `cf-deploy/resource/screenshots/prod/`

The CLI track in each codelab is unaffected — the screenshots are only shown when the user toggles to the **🖱 Console GUI** tab.

---

## Capture conventions

| Setting | Value |
|---|---|
| **Resolution** | At least 1440 × 900 (Retina preferred). Browser at 100% zoom. |
| **Format** | `.png` (lossless). Keep each file under ~400 KB; use `pngquant` or `sharp` if needed. |
| **Browser chrome** | Crop **out** the URL bar, bookmarks, tabs. Only the OCI Console UI should be visible. |
| **Console theme** | Use the default light theme (the codelab styling assumes light). |
| **Region** | All shots in `ap-singapore-1` unless noted. |
| **Annotation** | Red 2–3 px outline boxes around the active control. Optional numbered red circles for multi-step actions. Free tool: **CleanShot X**, **Skitch**, or macOS Preview's markup. |

### PII / data redaction — non-negotiable

Before saving the PNG, blur/redact every visible occurrence of:

- Real **tenancy OCID**, **user OCID**, **API keys**, **fingerprints**
- The **suffix** of your real test compartment if your real tenancy name is sensitive — use a fixed sample like `aisXXXX` in the placeholder hints; rename your test resources to match before screenshotting
- **Passwords**, **DSN strings**, **secret contents** (blur the entire field)
- **Real SSL certificates** / private keys
- **Real IP addresses** of internal AIS infrastructure
- Anything inside the user-profile menu (top-right avatar dropdown)

If unsure → blur it.

---

## File naming

Filenames are already wired into the HTML. **Do not rename them.** The pattern is:

```
{env}-{step}.{sub}{letter}-{slug}.png
```

Examples:
- `nonprod-2.1a-identity-compartments-nav.png`
- `prod-6.1a-pg-ha-instance-count-2.png`

---

## How to validate after capture

1. Save the PNG to the right folder (`resource/screenshots/nonprod/` or `…/prod/`).
2. Open the codelab HTML in a browser:
   ```
   open cf-deploy/OCI_NonProd_Codelab.html
   ```
3. Click the matching step in the sidebar → toggle the **🖱 Console GUI** tab.
4. The striped "pending" card for that ID should now show your screenshot.

If the placeholder is still striped, the filename or path is wrong — check spelling and folder.

---

## Non-Prod codelab (44 shots)

> Region: ap-singapore-1 · Compartment: `compartment-nonprod-aisXXXX`

### Step 2 · Compartment + VCN (13 shots)

| ID | Filename | What to capture |
|---|---|---|
| 2.1a | `nonprod-2.1a-identity-compartments-nav.png` | Hamburger menu expanded → Identity & Security → **Compartments** highlighted. Crop to left nav only. |
| 2.1b | `nonprod-2.1b-compartments-list-create-button.png` | Compartments list page · **Create Compartment** button visible. |
| 2.1c | `nonprod-2.1c-compartment-create-form-filled.png` | Create Compartment side-panel with Name + Description + Parent fields filled. Redact tenancy OCID. |
| 2.1d | `nonprod-2.1d-compartment-active.png` | New compartment row · State = **Active** · OCID visible to copy. |
| 2.2a | `nonprod-2.2a-compartment-switcher.png` | List/resource page · left-panel "Compartment" dropdown expanded with new compartment selected. |
| 2.2b | `nonprod-2.2b-vcn-wizard-start.png` | VCN list · "Start VCN Wizard" dialog open with **Create VCN with Internet Connectivity** selected. |
| 2.2c | `nonprod-2.2c-vcn-wizard-form-top.png` | Wizard top half · VCN Name + Compartment + CIDR Block fields filled (10.30.0.0/16). |
| 2.2d | `nonprod-2.2d-vcn-wizard-form-subnets.png` | Wizard mid · Public subnet 10.30.0.0/24 + Private 10.30.1.0/24 + DNS Label. |
| 2.2e | `nonprod-2.2e-vcn-wizard-review.png` | Wizard Review page listing all resources to be created (VCN/subnets/IGW/NAT/SG/route tables). |
| 2.2f | `nonprod-2.2f-vcn-creation-progress.png` | Progress page · resources ticking green as they get created. |
| 2.2g | `nonprod-2.2g-vcn-detail-subnets-list.png` | VCN detail · left Resources menu · **Subnets** tab showing 2 wizard-created subnets. |
| 2.2h | `nonprod-2.2h-create-subnet-form.png` | Create Subnet panel for `oke-pods` · Regional · CIDR 10.30.4.0/22 · Private · Route Table = private. |
| 2.2i | `nonprod-2.2i-vcn-final-4-subnets.png` | ✓ Subnets list with all 4 (public-lb, oke-nodes, oke-pods, private-data) Available. |

### Step 3 · WAF + Load Balancer (8 shots)

| ID | Filename | What to capture |
|---|---|---|
| 3.1a | `nonprod-3.1a-lb-list-create-button.png` | Load Balancers list page · Create Load Balancer button visible. |
| 3.1b | `nonprod-3.1b-lb-create-form-details.png` | Add Details · Name + Public + Shape Small 10 Mbps fixed + VCN + public-lb subnet. |
| 3.1c | `nonprod-3.1c-lb-listener.png` | Listener step · HTTP/port 80. |
| 3.1d | `nonprod-3.1d-lb-active-with-ip.png` | ✓ LB detail · State Active · public IP shown. |
| 3.2a | `nonprod-3.2a-waf-policies-list.png` | Identity & Security → WAF → Policies list · Create button visible. |
| 3.2b | `nonprod-3.2b-waf-actions-log-only.png` | WAF Actions tab · "Log Only" action defined (Return 200). |
| 3.2c | `nonprod-3.2c-waf-owasp-rules.png` | WAF Request Protection · OWASP CRS rules 920170/942100/941100 added · Log Only action. |
| 3.2d | `nonprod-3.2d-waf-attach-firewall.png` | WAF Firewalls tab · LB attached as enforcement point. |

### Step 4 · OKE Cluster (6 shots)

| ID | Filename | What to capture |
|---|---|---|
| 4.1a | `nonprod-4.1a-oke-list-create.png` | Developer Services → OKE list · Create Cluster button. |
| 4.1b | `nonprod-4.1b-oke-create-mode-custom.png` | Cluster type picker · **Custom Create** selected. |
| 4.1c | `nonprod-4.1c-oke-cluster-details.png` | Cluster details · k8s v1.29.1 · public API endpoint enabled. |
| 4.1d | `nonprod-4.1d-oke-nodepool-form.png` | Node Pool · AD-1 only · E4.Flex 1 OCPU/4 GB · 1 node · oke-nodes subnet. |
| 4.1e | `nonprod-4.1e-oke-active.png` | ✓ Cluster Active · 1 worker Ready in Nodes tab. |
| 4.3a | `nonprod-4.3a-access-cluster-dialog.png` | "Access Your Cluster" dialog · Local Access tab · create-kubeconfig command visible. **Redact tenancy OCID in command.** |

### Step 6 · PostgreSQL DB (5 shots)

| ID | Filename | What to capture |
|---|---|---|
| 6.2a | `nonprod-6.2a-pg-list-create.png` | Databases → PostgreSQL DB Systems list · Create button. |
| 6.2b | `nonprod-6.2b-pg-basic-info.png` | Create PG · Basic Info · name + version 16. |
| 6.2c | `nonprod-6.2c-pg-shape-storage.png` | Shape E4.Flex 2 OCPU/8 GB · instance count 1 · 100 GB storage. |
| 6.2d | `nonprod-6.2d-pg-network-creds.png` | Network (private-data) + Admin credentials. **Blur password field.** |
| 6.2e | `nonprod-6.2e-pg-active-endpoint.png` | ✓ DB Active · primary endpoint (private IP) visible. |

### Step 7 · Cache (3 shots)

| ID | Filename | What to capture |
|---|---|---|
| 7.1a | `nonprod-7.1a-cache-list-create.png` | Databases → Caches → OCI Cache list · Create button. |
| 7.1b | `nonprod-7.1b-cache-config-form.png` | Create Cache · Valkey 8.1 · non-clustered · 1 shard / 1 node / 4 GB. |
| 7.1c | `nonprod-7.1c-cache-active-fqdn.png` | ✓ Cache Active · Primary FQDN visible. |

### Step 8 · Streaming (3 shots)

| ID | Filename | What to capture |
|---|---|---|
| 8.1a | `nonprod-8.1a-stream-pool-create.png` | Create Stream Pool dialog. |
| 8.2a | `nonprod-8.2a-stream-create-form.png` | Create Stream · Name=queue.events · Partitions=2 · Retention=72h. |
| 8.2b | `nonprod-8.2b-streams-list-3.png` | Stream Pool detail · 3 streams Active. |
| 8.2c | `nonprod-8.2c-kafka-conn-settings.png` | Stream Pool → Kafka Connection Settings (bootstrap + SASL pattern). Redact tenancy name. |

### Step 9 · Object Storage + Vault (5 shots)

| ID | Filename | What to capture |
|---|---|---|
| 9.1a | `nonprod-9.1a-buckets-create-form.png` | Create Bucket dialog · Standard · Private. |
| 9.1b | `nonprod-9.1b-buckets-list-3.png` | Bucket list · 3 buckets present. |
| 9.2a | `nonprod-9.2a-vault-create-form.png` | Create Vault · type Default · name filled. |
| 9.2b | `nonprod-9.2b-master-key-create.png` | Create Master Key · AES-256 · Software protection. |
| 9.3a | `nonprod-9.3a-secret-create.png` | Create Secret form. **BLUR/REDACT the contents field.** |

---

## Prod codelab (34 shots)

> Region: ap-singapore-1 · Compartment: `compartment-prod-aisXXXX`
> **Capture in a dedicated test prod-like environment, NOT in real production.**

### Step 2 · Compartment + VCN (Multi-AD) (8 shots)

| ID | Filename | What to capture |
|---|---|---|
| 2.1a | `prod-2.1a-compartment-create.png` | Create Compartment dialog filled for production. |
| 2.2a | `prod-2.2a-vcn-create-basic.png` | Create VCN (non-wizard) · CIDR 10.20.0.0/16 · DNS label. |
| 2.2b | `prod-2.2b-gateways-3-created.png` | VCN detail · IGW + NAT + SG all Available. |
| 2.2c | `prod-2.2c-route-tables.png` | Route Tables list with rt-public and rt-private + one expanded. |
| 2.2d | `prod-2.2d-create-subnet-regional.png` | Create Subnet panel · Subnet Type = **Regional** clearly selected. |
| 2.2e | `prod-2.2e-subnets-4-final.png` | ✓ 4 regional subnets Available. |
| 2.3a | `prod-2.3a-nsg-ingress-rule.png` | Add Ingress Rule on nsg-db · Source Type = **NSG** · Source NSG = nsg-oke-workers. |
| 2.3b | `prod-2.3b-nsgs-3-list.png` | ✓ 3 NSGs created (workers, db, cache). |

### Step 3 · WAF Prevention + Flexible LB (5 shots)

| ID | Filename | What to capture |
|---|---|---|
| 3.1a | `prod-3.1a-lb-flexible-shape.png` | Create LB · **Flexible** shape · 10 / 8000 Mbps. |
| 3.1b | `prod-3.1b-lb-listener-https.png` | HTTPS Listener · port 443 · cert upload fields (do not show cert content). |
| 3.2a | `prod-3.2a-waf-actions-block.png` | WAF Actions · Block (403) + Challenge defined. |
| 3.2b | `prod-3.2b-waf-rate-limit.png` | WAF Request Rate Limiting · 1000 req / 60 s · block 600 s. |
| 3.2c | `prod-3.2c-waf-attached-prevention.png` | ✓ WAF policy · Mode = Prevention · attached to Prod LB. |

### Step 4 · OKE Multi-AD (4 shots)

| ID | Filename | What to capture |
|---|---|---|
| 4.1a | `prod-4.1a-oke-vcn-native-cni.png` | Cluster details · Network Type = **VCN-Native Pod Networking**. |
| 4.1b | `prod-4.1b-nodepool-multi-ad.png` | Node Pool placement · **both AD-1 and AD-2** checked. |
| 4.1c | `prod-4.1c-nodepool-shape-16gb.png` | E4.Flex 2 OCPU / 16 GB / 4 nodes. |
| 4.1d | `prod-4.1d-oke-nodes-2-ads.png` | ✓ Nodes tab · 4 Ready · "Availability Domain" column showing 2 ADs (2 in AD-1, 2 in AD-2). |

### Step 6 · PG HA Pair (4 shots)

| ID | Filename | What to capture |
|---|---|---|
| 6.1a | `prod-6.1a-pg-ha-instance-count-2.png` | Instance count = **2** (HA pair). |
| 6.1b | `prod-6.1b-pg-regionally-durable.png` | Storage section · **Regionally Durable** toggle ON. |
| 6.1c | `prod-6.1c-pg-backup-policy.png` | Backup Daily · 30-day retention · Sunday 03:00 maintenance. |
| 6.1d | `prod-6.1d-pg-primary-standby.png` | ✓ Instances tab · 1 Primary (AD-1) + 1 Standby (AD-2). |

### Step 7 · Cache HA (2 shots)

| ID | Filename | What to capture |
|---|---|---|
| 7.1a | `prod-7.1a-cache-ha-2-nodes.png` | Create Cache · Node count = 2 · 8 GB each. |
| 7.1b | `prod-7.1b-cache-ha-active.png` | ✓ Nodes tab · 1 Primary + 1 Replica · Primary FQDN visible. |

### Step 8 · Streaming Multi-AD (3 shots)

| ID | Filename | What to capture |
|---|---|---|
| 8.1a | `prod-8.1a-stream-pool-create.png` | Create Stream Pool dialog. |
| 8.2a | `prod-8.2a-stream-integration-30day.png` | Create Stream for `integration.events` · Retention = 720 h. |
| 8.2b | `prod-8.2b-streams-3-active.png` | ✓ 3 streams Active · retention column visible. |

### Step 9 · Object Storage + VP Vault (3 shots)

| ID | Filename | What to capture |
|---|---|---|
| 9.1a | `prod-9.1a-bucket-create.png` | Create Bucket · Standard · Private. |
| 9.1b | `prod-9.1b-bucket-replication-tokyo.png` | Create Replication Policy · destination = ap-tokyo-1 · DR bucket. |
| 9.2a | `prod-9.2a-vault-virtual-private.png` | Create Vault · type = **Virtual Private** (HSM). |

### Step 11 · Failover + Cost + Alarms (5 shots)

| ID | Filename | What to capture |
|---|---|---|
| 11.2a | `prod-11.2a-pg-failover-action.png` | DB system detail · **Actions** dropdown open · Failover option visible. |
| 11.2b | `prod-11.2b-pg-role-swapped.png` | ✓ After failover · roles swapped (AD-2 now Primary). |
| 11.3a | `prod-11.3a-cost-analysis-by-service.png` | Cost Analysis · grouped by Service · last 7 days · prod compartment filter. |
| 11.3b | `prod-11.3b-budget-alert.png` | Create Budget · alerts at 75 / 90 / 100% · email recipients. |
| 11.3c | `prod-11.3c-alarm-5xx.png` | Create Alarm · oci_lbaas / HttpResponses · 5XX dimension · &gt; 10/min for 5 min. |

---

## Bulk-capture workflow

If you're going through this in one sitting:

1. **Set up a clean test tenancy or sandbox compartment.** Don't capture against real prod.
2. **Run the CLI commands from Step 1 first** (Prerequisites) so your shell has the env vars and resource OCIDs.
3. **Window size:** set browser to a fixed window size (e.g. 1600 × 1000) for all shots — keeps the screenshots visually consistent.
4. **Capture in order** within each step — the dialog flow follows the step list above.
5. **Save → annotate → optimize → save final.** Tools:
   - Capture: macOS `Cmd+Shift+4` (region) or CleanShot X
   - Annotate: CleanShot X / Skitch / `pencil` icon in Preview
   - Optimize: `pngquant --quality=65-85 file.png --output file.png --force` (Homebrew: `brew install pngquant`)
6. After dropping in a batch, reload the codelab in browser and confirm the placeholders flipped to real images.

## Optional: convert PNG to WebP for smaller payloads

If you want to keep the deployed Cloudflare Pages bundle small, you can serve WebP and let the `<img>` tag fall back. The current setup uses plain `<img src="...png">`, so just commit PNGs — they're cached at 24 h by `_headers`.

---

**Last updated:** 2026-06-02
