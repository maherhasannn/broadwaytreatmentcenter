# Broadway Treatment Center — Claude Code Instructions

## Project overview

This repo powers content operations for [broadwaytreatmentcenter.com](https://broadwaytreatmentcenter.com) — a treatment placement and referral service in Orange County, CA, specializing in detox, residential and outpatient rehab, couples treatment, medical detox, withdrawal care, dual diagnosis, MAT, and insurance-supported placement. The site runs on WordPress.

Broadway was formerly a direct treatment provider in Huntington Beach and now connects people to a network of verified, licensed providers. All content targets people in crisis: panicking spouses/parents, couples deciding to get help together, someone in active withdrawal, and high-intent searchers who need help today. Every article is written for one conversion goal — phone calls to **(714) 400-2048** — with insurance/benefits verification as the secondary CTA.

**Positioning guardrail (non-negotiable):** Broadway is a placement/referral service, **not a treatment facility**. The active voice ("we verify benefits," "we coordinate admission," "available 24/7") is defensible only when paired with that disclosure and with no guarantees on coverage or joint placement. The "we" is the placement team, never a clinic. This framing must hold across every article and the schema.

**Site thesis (the one idea every page serves):** Broadway is a recognized former-provider brand repurposed into a 24/7 placement service that monetizes high-intent, crisis-state searchers by routing them to vetted partner facilities via a phone call. Clinically authoritative enough to earn trust, honest about the referral role, built to convert a panicked searcher into a call.

Canonical model page for structure, depth, and voice: `https://broadwaytreatmentcenter.com/treatment/couples-addiction-treatment-program/`. (There is no Rhode Island model page; Broadway's footprint is Orange County / California only.)

---

## Environment

WordPress credentials are loaded automatically from `.env` at session start via the SessionStart hook. They are available as environment variables:

- `WP_USERNAME` — WordPress admin username
- `WP_APP_PASSWORD` — WordPress application password
- `WP_API_ENDPOINT` — `https://broadwaytreatmentcenter.com/wp-json/wp/v2/pages`

If credentials are missing, run the session-start hook manually:
```bash
CLAUDE_CODE_REMOTE=true CLAUDE_PROJECT_DIR=$(pwd) CLAUDE_ENV_FILE=/tmp/claude-env bash .claude/hooks/session-start.sh
```

### Hosting environment constraints

The site runs on SiteGround. All GCP datacenter IPs (34.x.x.x, 35.x.x.x) hit a SiteGround JavaScript proof-of-work CAPTCHA (HTTP 202 response) before any request reaches WordPress. The CAPTCHA cookie (`_I_`) is cryptographically bound to the external IP that solved it. GCP Cloud NAT rotates external IPs per TCP connection, so you cannot solve on one connection and post on another — the cookie will be rejected and the POST returns 403.

**What works:** single persistent `http.client.HTTPSConnection` (all steps on one socket, described in Step 5).
**What does not work:** curl subprocesses, multiple Python urllib calls, the `requests` library, wp-login.php session auth — all either rotate IPs or trigger WAF escalation.
**What is also blocked:** `/xmlrpc.php` (returns 502 from SiteGround's application firewall regardless of CAPTCHA state).

---

## Available skills

Three custom skills are installed automatically at session start:

| Skill | Purpose |
|---|---|
| `/url` | Canonical URL map — which pages EXIST (safe to link to) vs DON'T exist yet (use substitutes), site model, voice rule, page types, CTA modes. Always pull slugs, page type, parent pillar, geo, keyword, and CTA mode from here. Mark a line with the completed marker after building it; check for the marker before starting so pages aren't built twice. |
| `/wordpress` | Full article engine — deep-clinical 4,000–6,000+ words, 3 embedded CTA boxes (top/middle/end), 15–25 FAQs, comparison table, crisis blockquotes, medically-reviewed byline, trusted-sources list, editorial disclaimer. |
| `/schema` | Generates the JSON-LD `<script>` block. Requires the article content as input. |

---

## Full content + posting routine

Follow these steps in order every time a new draft is created.

### Step 1 — Pick a slug with `/url`

Invoke `/url` to review the canonical page map. Either:
- Pick a page from the EXIST list that hasn't been built yet (no completed marker), or
- Identify the right cluster and mint a new slug following that cluster's naming convention (geo pages follow the live `/telehealth-therapy-{city}-ca/` pattern)

The map gives the slug its **page type** (education / emergency-intent / insurance / geo / couples / comparison), **cluster + parent pillar** (drives internal linking), **geo**, **target keyword**, and **CTA mode** (call-primary or verification-primary). Never invent a slug or a link target without checking here first. **Only link to pages in the EXIST list.**

### Step 2 — Write the article with `/wordpress`

Invoke `/wordpress` with the chosen slug/topic. The skill will produce:

- Deep-clinical 4,000–6,000+ word article in WordPress Gutenberg block HTML (emergency-intent pages run shorter — see map)
- Clinical depth: named assessment scales (CIWA-Ar, COWS), hour/day withdrawal timelines, specific medication classes, substance-by-substance danger gradients
- 3 embedded CTA boxes, contextually rewritten per page (Box 1 dark navy hero + phone; Box 2 white clinical-assessment card + pillar/insurance links; Box 3 light continuum card + next-stage link)
- Medically-reviewed byline + top and closing crisis blockquotes (911 / 988 / local crisis line + the (714) 400-2048 number)
- 15–25 FAQ entries formatted for AI Overview extraction
- At least one comparison table (inpatient vs outpatient, or detox vs rehab)
- Internal links using only confirmed EXIST pages from `/url` (up to parent pillar, sideways to cluster siblings + neighboring OC geo, plus `/insurance-verification/` and/or `/contact-us/`)
- External links to authoritative sources only: SAMHSA, NIDA, CDC, NIH, NIAAA, California DHCS, 988 Lifeline
- Editorial disclaimer ("placement/referral service, not a treatment facility") + full deliverables block at the end (SEO title, meta, slug, H1, internal link map, etc.)

**Before moving to Step 3:** Verify every link in the article — internal and external — returns a valid response. Confirm no `[BRACKETED PLACEHOLDER]` text survives in the CTA boxes (topic, geo, headlines, hrefs all customized to this page). Confirm no direct-provider voice slipped in ("our facility," "we treat," "our clinical staff"). Do not skip this check.

### Step 3 — Generate schema with `/schema`

Invoke `/schema` and pass:
1. The full page URL (`https://broadwaytreatmentcenter.com/<slug>/`)
2. The complete article content from Step 2

The skill outputs a single `<script type="application/ld+json">` block — ready to paste into WordPress as a Custom HTML block at the bottom of the post content.

The schema includes: `Organization`, `MedicalOrganization` (referral/info network, **not** treatment provider; `knowsAbout` topics, `medicalSpecialty: ["Psychiatric"]` only — no invalid enum values), `ContactPoint`, `Place` (real Huntington Beach address), `WebSite`, `WebPage`, `Article`, `FAQPage`, `Service` (no priced Offer), `BreadcrumbList`, `DefinedTermSet`, and relevant `DefinedTerm` / `Thing` entities for the page's cluster.

**Do NOT type the entity as `LocalBusiness` / `MedicalBusiness` / `MedicalClinic` / `Hospital`** — Broadway is a referral service, not a care-delivering clinic; that typing would contradict the site's own disclosure on a YMYL page. (Broadway DOES have a real address, so a truthful `PostalAddress`/`Place` is included — just never wrapped in a clinic/business type.) No `aggregateRating` or review nodes; the provider-era Joint Commission seal stays in prose only, never as schema rating data.

**The schema skill will refuse to generate if:**
- No FAQ section exists in the article
- Any link hasn't been verified against the EXIST list / valid-links reference

### Step 4 — Final link check

Before posting, confirm:
- [ ] All internal links resolve to real broadwaytreatmentcenter.com pages in the EXIST list (no `/couples-assessment/`, `/crisis-support/`, or out-of-state geo — use substitutes: `/insurance-verification/` or `/contact-us/`, and inline 911/988 for crisis)
- [ ] All external links return HTTP 200
- [ ] No bracketed placeholder text survives in the CTAs (`[EMOTIONAL HOOK HEADLINE]`, `[CLUSTER PILLAR URL]`, `[NEXT-STAGE URL]`, etc.)
- [ ] Phone links point to `tel:7144002048` (displayed "(714) 400-2048") — never split the displayed number from the tel: target
- [ ] No direct-provider voice ("our facility," "we treat," "our detox program") survives anywhere
- [ ] Schema JSON is valid (no trailing commas, all brackets matched, single @graph, single script tag)

### Step 5 — Post to WordPress

**Do not use curl subprocesses, the `requests` library, or multiple separate Python HTTP calls.** SiteGround's WAF issues a proof-of-work CAPTCHA to all GCP IPs, and the resulting `_I_` cookie is bound to the external IP that solved it. GCP Cloud NAT rotates IPs per TCP connection, so solving and posting on separate connections means the cookie arrives on the wrong IP and the POST returns 403.

**The only working approach: write a Python script inline that performs all steps on a single persistent `http.client.HTTPSConnection` object.**

The script must do the following in order, on one `conn` object without closing it between steps:

#### 1. Build the JSON payload

Construct the WordPress payload dict and serialize it to bytes:

```python
import json, base64, hashlib, time, os, re, sys, ssl, http.client, urllib.parse

WP_USERNAME = os.environ['WP_USERNAME']
WP_APP_PASSWORD = os.environ['WP_APP_PASSWORD']
ENCODED_CREDS = base64.b64encode(f"{WP_USERNAME}:{WP_APP_PASSWORD}".encode()).decode()
HOST = 'broadwaytreatmentcenter.com'
TARGET = '/wp-json/wp/v2/pages'

PAYLOAD = json.dumps({
    "title": "<SEO title>",
    "slug": "<slug>",
    "status": "publish",          # always publish, never draft
    "content": FULL_CONTENT,      # Gutenberg HTML + schema <!-- wp:html --> block appended
    "excerpt": "<meta description>",
    "parent": 0,
    "menu_order": 0,
    "meta": {
        "_yoast_wpseo_title": "...",
        "_yoast_wpseo_metadesc": "...",
        "_yoast_wpseo_focuskw": "...",
        "_yoast_wpseo_canonical": "https://broadwaytreatmentcenter.com/<slug>/",
        "_yoast_wpseo_opengraph-title": "...",
        "_yoast_wpseo_opengraph-description": "...",
        "_yoast_wpseo_twitter-title": "...",
        "_yoast_wpseo_twitter-description": "...",
    }
}).encode('utf-8')
```

The `content` field must include the full Gutenberg block HTML from Step 2 with the `<script type="application/ld+json">` block from Step 3 appended as a `<!-- wp:html -->` block at the very end.

#### 2. Open one SSL connection

```python
ssl_ctx = ssl.create_default_context()
ssl_ctx.check_hostname = False
ssl_ctx.verify_mode = ssl.CERT_NONE   # required in this environment

UA = 'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.0.0 Safari/537.36'
conn = http.client.HTTPSConnection(HOST, 443, context=ssl_ctx, timeout=90)
cookies = {}

def parse_cookies(resp):
    for h, v in resp.getheaders():
        if h.lower() == 'set-cookie':
            kv = v.split(';')[0].strip()
            if '=' in kv:
                k2, v2 = kv.split('=', 1)
                cookies[k2.strip()] = v2.strip()

def cookie_hdr():
    return '; '.join(f'{k}={v}' for k, v in cookies.items())
```

#### 3. Fetch the CAPTCHA challenge (on `conn`)

```python
encoded_target = urllib.parse.quote(TARGET, safe='')
captcha_url = f'/.well-known/sgcaptcha/?r={encoded_target}'

conn.request('GET', captcha_url, headers={
    'Host': HOST, 'User-Agent': UA, 'Connection': 'keep-alive'
})
r1 = conn.getresponse()
body1 = r1.read().decode('utf-8', errors='replace')
parse_cookies(r1)

m = re.search(r'const sgchallenge="([^"]+)"', body1)
challenge = m.group(1)  # format: "difficulty:timestamp:nonce:target_hash:"
```

#### 4. Solve the PoW (CPU only — no network)

```python
def mbe(n):
    """Minimal big-endian bytes — must match the JS implementation exactly."""
    if n > 16777215: nb = 4
    elif n > 65535:  nb = 3
    elif n > 255:    nb = 2
    else:            nb = 1
    r = bytearray(nb)
    for i in range(nb - 1, -1, -1):
        r[i] = n & 0xFF; n >>= 8
    return bytes(r)

def solve_pow(challenge_str):
    difficulty = int(challenge_str.split(':')[0])
    cb = challenge_str.encode('utf-8')
    t0 = time.time()
    for counter in range(10_000_000):
        inp = cb + mbe(counter)
        if int.from_bytes(hashlib.sha1(inp).digest()[:4], 'big') >> (32 - difficulty) == 0:
            ms = int((time.time() - t0) * 1000)
            return base64.b64encode(inp).decode('ascii'), ms, counter + 1
            # solution = b64(challenge_bytes + counter_bytes), NOT b64(hash)
    return None, 0, 0

sol, ms, total = solve_pow(challenge)
```

Difficulty is typically 21 bits, solving in 1–10 seconds.

#### 5. Submit the solution (on the same `conn`)

```python
params = urllib.parse.urlencode({'r': TARGET, 'sol': sol, 's': f"{ms}:{total}"})
conn.request('GET', f'/.well-known/sgcaptcha/?{params}', headers={
    'Host': HOST, 'User-Agent': UA,
    'Referer': f'https://{HOST}{captcha_url}',
    'Connection': 'keep-alive',
    'Cookie': cookie_hdr(),
})
r2 = conn.getresponse()
body2 = r2.read().decode('utf-8', errors='replace')
parse_cookies(r2)

# _I_ may arrive via Set-Cookie header or via JS document.cookie in the body
m2 = re.search(r'document\.cookie="(_I_=[^;"]+)', body2)
if m2 and '_I_' not in cookies:
    k, v = m2.group(1).split('=', 1)
    cookies[k] = v.rstrip('"')
```

#### 6. POST the article (on the same `conn`)

```python
conn.request('POST', TARGET, body=PAYLOAD, headers={
    'Host': HOST, 'User-Agent': UA,
    'Content-Type': 'application/json; charset=utf-8',
    'Content-Length': str(len(PAYLOAD)),
    'Authorization': f'Basic {ENCODED_CREDS}',
    'Accept': 'application/json',
    'Origin': f'https://{HOST}',
    'Referer': f'https://{HOST}/wp-admin/',
    'Connection': 'keep-alive',
    'Cookie': cookie_hdr(),
})
r3 = conn.getresponse()
body3 = r3.read().decode('utf-8', errors='replace')
conn.close()

result = json.loads(body3)
print(f"Post ID: {result['id']}")
print(f"Link:    {result['link']}")
print(f"Status:  {result['status']}")
```

A successful response is HTTP 201. Parse `result['id']` and `result['link']` to confirm.

#### On success

1. Log the post ID, link, slug, and edit URL.
2. Mark the slug's line in `url.md` with ✅.
3. `git add url.md && git commit -m "Mark /<slug>/ as published (WP page ID <id>)" && git push -u origin <branch>`.
4. Delete every temporary script and working file created during the run. **NEVER commit or push any file other than `url.md`.**

---

## Content standards

- Voice: senior addiction-medicine-literate placement specialist speaking to a panicking partner — specific, calm, clinically credible, never sensational
- Active placement-service voice ("we connect you with," "we verify benefits," "we coordinate admission," "24/7") — always paired with the "not a treatment facility" disclosure. Never direct-provider voice ("our facility," "we treat," "our clinicians treat you")
- Every section opens with a 2–3 sentence direct answer (AI Overview ready)
- Deep clinical register required — named scales, timelines, medications, substance-specific danger gradients (see `/wordpress`)
- No unsupported guarantees, no "best" or "top rated" as ranked claims, no recovery/outcome promises
- Medical framing: "can," "may," "in many cases," "depending on the facility/plan" — never "will" or "guaranteed"
- Coverage + joint placement always framed as verified/assessed, never guaranteed ahead of time
- 911 / 988 callouts wherever overdose or severe withdrawal is discussed
- Word count: 4,000–6,000+ words per geo/pillar article (emergency-intent pages shorter)
- CTAs: 3 per article, all contextually rewritten — no generic copy, no surviving placeholders
- NO EM DASHES

---

## NAP / brand constants (verified — never change without re-verifying live)

- **Name:** Broadway Treatment Center
- **Phone:** (714) 400-2048 / `+1-714-400-2048` / `tel:7144002048`  *(note: an older number, (714) 443-8218, appears in some legacy meta — replace on sight)*
- **Address:** 18582 Beach Blvd, Suite 214, Huntington Beach, CA 92648, US  *(real and verified — used in schema Place/PostalAddress, but the entity is never typed as LocalBusiness/MedicalClinic)*
- **Footprint:** Orange County / California only — not national, not multi-state
- **Contact URL:** `https://broadwaytreatmentcenter.com/contact-us/`
- **Insurance/verification URL:** `https://broadwaytreatmentcenter.com/insurance-verification/`  *(use this as the secondary CTA target; replaces the non-existent assessment URL)*
- **Crisis:** inline 911 / 988 blockquote — there is no `/crisis-support/` page; do not link one
- **API endpoint:** `https://broadwaytreatmentcenter.com/wp-json/wp/v2/pages`
