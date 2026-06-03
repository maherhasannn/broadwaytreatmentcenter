---
name: url.md
description: read on demand. URL inventory and site architecture for broadwaytreatmentcenter.com — which pages exist, what voice to use, and which internal links are safe. Look up a slug here before writing. Costs zero tokens until needed.
last_verified: 2026-06-03
---

# broadwaytreatmentcenter.com URL Map

## Site model (read first)

broadwaytreatmentcenter.com is a **treatment placement and referral service** in Orange County, CA. It was formerly a direct treatment provider and now connects people to a network of verified, licensed providers. It coordinates placement and benefit verification but does **not** own, operate, or staff a treatment facility.

- **Location:** 18582 Beach Blvd, Suite 214, Huntington Beach, CA 92648
- **Phone (the only conversion goal — drive calls here):** (714) 400-2048
- **Secondary CTA:** insurance/benefits verification -> `/insurance-verification/`
- **Footprint:** Orange County / California only. Not multi-state, not national.

## Voice rule (most important — never break this)

Always write as the **referral service**, never as the treatment provider. The "we" is the placement team, not a clinic.

- **Say:** "we connect you with," "our placement team," "our network of verified providers," "our treatment partners," "we coordinate admission," "we verify your benefits," "we help you find."
- **Never say:** "our facility," "our clinic," "we admit," "we treat," "our doctors/nurses treat you," "our detox program," "in our facility."

Recasts:
- "Our facility offers medically supervised detox." -> "We connect you with medically supervised detox programs in our network."
- "Our clinicians treat both partners together." -> "We place couples with programs that keep partners together when clinically appropriate."
- "We accept Anthem Blue Cross." -> "Our treatment partners work with most Anthem PPO plans; we verify your benefits before any commitment."

## Hard rules for every page

- Keep the "placement/referral service, not a treatment facility" disclosure in the opening and the editorial disclaimer.
- **Never guarantee** coverage, in-network status, out-of-pocket cost, or a specific joint-placement setup. Coverage = "verified before any commitment." Joint placement = "regularly possible, never guaranteed ahead of time."
- CTA language: "Call (714) 400-2048," "call a care navigator," "verify your benefits," "begin the placement process." Keep the urgency.
- Any page touching overdose or severe withdrawal: 911 for danger, call/text 988 for crisis. Put a crisis blockquote near the top AND at the close. (Inline blockquote, not a link.)
- Match the model page (`/treatment/couples-addiction-treatment-program/`) for clinical depth and page furniture — byline, crisis blockquotes, mid-page CTA banners, trusted-sources list, editorial disclaimer. See `rehab-content-skill.md`.

---

## Page types (each = a different template)

| Type | Intent | Length | CTA weight | Notes |
|---|---|---|---|---|
| **education** | informational, top-of-funnel | 1,500-3,000 | light, mid + end | symptom/timeline/explainer; build trust, link down-funnel |
| **emergency-intent** | crisis, "now/near me/same-day" | 800-1,500 | heavy, top + repeated | short, reassuring, call-first; 911/988 prominent |
| **insurance** | coverage/verification | 1,200-2,500 | medium | carrier-specific; route to free benefits check via call |
| **geo** | local landing page | 1,200-2,500 | medium-heavy | city specifics; "providers serving [area]," never "our [city] facility" |
| **couples** | relationship angle on any topic | 1,500-3,000 | medium | layer codependency/joint-recovery/boundaries onto base topic |
| **comparison/process** | "X vs Y," "what happens in" | 1,200-2,500 | light-medium | explainer; strong internal linking |

## CTA modes
- **call-primary:** phone CTA above the fold + repeated; verification secondary. (emergency-intent, geo, insurance)
- **verification-primary:** benefits-verification CTA leads, call secondary. (education, comparison, top-of-funnel couples)
- Both always include (714) 400-2048.

---

## Pages that EXIST — safe to link to

These are confirmed live. Link only to these.

**Top-level / utility**
- `/` · `/about/` (-> `/mission-statement/`, `/about/accreditations/`, `/about/treatment-philosophy/`)
- `/faqs/` · `/blog/` · `/contact-us/` · `/privacy-policy/`
- `/insurance-verification/` <- **verification CTA target**
- `/medication-assisted-treatment/` · `/incidental-medical-services-ims/`

**Treatment cluster** (`/treatment/`)
- `/treatment/` (pillar)
- `/treatment/orange-county-detox/` (pillar) -> `/drug-detox/`, `/alcohol-detox/`, `/opioid-detox/`, `/heroin-detox/`, `/fentanyl-detox/`, `/prescription-pills-detox/` (all nested under it)
- `/treatment/residential-treatment-orange-county/`
- `/treatment/alcohol-treatment/` -> `/program/`, `/inpatient/`, `/outpatient/`, `/center/`, `/drug-and-alcohol-abuse/`
- `/treatment/substance-abuse/` -> `/program/`, `/outpatient-treatment/`, `/inpatient-treatment/`, `/treatment-center/`
- `/treatment/outpatient-rehab-orange-county/` (IOP pillar)
- `/treatment/intervention/` · `/treatment/aftercare/`

**Unique Services cluster** (`/unique-services/`)
- `/unique-services/` (pillar)
- `/treatment/couples-addiction-treatment-program/` (-> `/center/`) <- **couples link target + model page**
- `/treatment/pet-friendly/` · `/treatment/dual-diagnosis/` · `/treatment/jail-diversion/`
- `/unique-services/relapse-prevention/` · `/unique-services/life-skills-training/`

**Geo pattern (live, expanding)**
- `/telehealth-therapy-{city}-ca/` — live for Midway City, Buena Park. Follow this nested-NAP, referral-voice pattern for new geo pages.

## Pages that DON'T exist yet — do NOT link to these

If you need one of these as a link target, use the substitute instead. Don't invent the link.

| Wanted page | Status | Use instead |
|---|---|---|
| `/couples-assessment/` | not live | `/insurance-verification/` or `/contact-us/` |
| `/crisis-support/` | not live | inline 911/988 blockquote (no link) |
| `/couples-detox-rhode-island/` | not live, out of CA footprint | model on `/treatment/couples-addiction-treatment-program/` |
| any state/national geo (RI, etc.) | not live | stick to California / Orange County |
| the 90 new topic pages | being built | link **up** to a pillar above, not sideways to other new pages |

---

## How to use this map (instruction for the writing skill)

1. **Every internal link must point to a page in the "EXIST" list.** If the link you want is in the "DON'T exist" list, use its substitute. Never emit a link to a page you haven't confirmed exists.
2. Pick the **page type** -> use its template.
3. Build internal links: **up** to the parent pillar, **sideways** to 2-3 sibling pages in the same cluster, plus a CTA link to `/insurance-verification/` and/or `/contact-us/`.
4. Apply the **referral voice rule** everywhere. Never direct-provider voice.
5. Set the **CTA mode**; always include (714) 400-2048.
6. Use the **target keyword** as primary; add natural variations.
7. New geo pages follow the `/telehealth-therapy-{city}-ca/` pattern. New topic pages link up to a pillar, not to each other, until they're published.
8. **After building a page, mark its line in this file with a ✅ so it isn't written twice.** Before starting any page, check that its line is not already marked ✅ — if it is, the page is done; pick a different URL. A line with no ✅ is still open.
---

# Couples Rehab — Content Build Todo (90 pages)

Status: `[ ]` not started · `[✅]` posted to WP draft
⚠️ = YMYL/accuracy watch item (see notes at bottom)

# URL Content Checklist

| # | Page Title | URL | Done |
|---|---|---|---|
| 1 | Signs Someone Needs Drug Detox | /signs-someone-needs-drug-detox/ | ☐ |
| 2 | Alcohol Withdrawal Symptoms Timeline | /alcohol-withdrawal-symptoms-timeline/ | ☐ |
| 3 | Fentanyl Detox Orange County | /fentanyl-detox-orange-county-ca/ | ☐ |
| 4 | Cocaine Addiction Treatment Orange County | /cocaine-addiction-treatment-orange-county/ | ☐ |
| 5 | Meth Rehab Orange County | /meth-rehab-orange-county-ca/ | ☐ |
| 6 | Benzo Detox Orange County | /benzodiazepine-detox-orange-county/ | ☐ |
| 7 | Rehab That Accepts Anthem Blue Cross | /anthem-blue-cross-rehab-orange-county/ | ☐ |
| 8 | Rehab That Accepts Aetna Insurance | /aetna-rehab-orange-county/ | ☐ |
| 9 | Rehab That Accepts Cigna Insurance | /cigna-rehab-orange-county/ | ☐ |
| 10 | Rehab That Accepts United Healthcare | /united-healthcare-rehab-orange-county/ | ☐ |
| 11 | Does Insurance Cover Rehab in California | /does-insurance-cover-rehab-california/ | ☐ |
| 12 | How to Help an Addicted Loved One | /how-to-help-an-addicted-loved-one/ | ☐ |
| 13 | My Husband Is Addicted to Drugs | /my-husband-is-addicted-to-drugs/ | ☐ |
| 14 | My Wife Is Addicted to Alcohol | /my-wife-is-addicted-to-alcohol/ | ☐ |
| 15 | My Son Is Addicted to Fentanyl | /my-son-is-addicted-to-fentanyl/ | ☐ |
| 16 | My Daughter Needs Rehab | /my-daughter-needs-rehab/ | ☐ |
| 17 | Couples Rehab Orange County | /couples-rehab-orange-county-ca/ | ☐ |
| 18 | Rehab for Married Couples California | /rehab-for-married-couples-california/ | ☐ |
| 19 | Pet Friendly Rehab California | /pet-friendly-rehab-california/ | ☐ |
| 20 | Executive Rehab Orange County | /executive-rehab-orange-county/ | ☐ |
| 21 | Rehab for Professionals Orange County | /rehab-for-professionals-orange-county/ | ☐ |
| 22 | Rehab for Nurses and Healthcare Workers | /rehab-for-nurses-orange-county/ | ☐ |
| 23 | Rehab for First Responders California | /rehab-for-first-responders-california/ | ☐ |
| 24 | Trauma Therapy Orange County | /trauma-therapy-orange-county/ | ☐ |
| 25 | PTSD Treatment Orange County | /ptsd-treatment-orange-county/ | ☐ |
| 26 | EMDR Therapy Orange County | /emdr-therapy-orange-county-ca/ | ☐ |
| 27 | OCD Treatment Orange County | /ocd-treatment-orange-county/ | ☐ |
| 28 | Bipolar Disorder Treatment Orange County | /bipolar-treatment-orange-county/ | ☐ |
| 29 | Borderline Personality Disorder Treatment | /borderline-personality-disorder-treatment-orange-county/ | ☐ |
| 30 | Panic Attack Treatment Orange County | /panic-attack-treatment-orange-county/ | ☐ |
| 31 | Mental Breakdown Help Orange County | /mental-breakdown-help-orange-county/ | ☐ |
| 32 | Depression Treatment Without Medication | /depression-treatment-without-medication/ | ☐ |
| 33 | Holistic Rehab Orange County | /holistic-rehab-orange-county/ | ☐ |
| 34 | Christian Rehab Orange County | /christian-rehab-orange-county/ | ☐ |
| 35 | Luxury Rehab Orange County | /luxury-rehab-orange-county/ | ☐ |
| 36 | Private Rehab California | /private-rehab-california/ | ☐ |
| 37 | Same Day Rehab Admissions Orange County | /same-day-rehab-admissions-orange-county/ | ☐ |
| 38 | Emergency Rehab Placement California | /emergency-rehab-placement-california/ | ☐ |
| 39 | 24 Hour Rehab Helpline Orange County | /24-hour-rehab-helpline-orange-county/ | ☐ |
| 40 | What Happens in Rehab | /what-happens-in-rehab/ | ☐ |
| 41 | How Long Is Rehab | /how-long-is-rehab/ | ☐ |
| 42 | How Much Does Rehab Cost | /how-much-does-rehab-cost-california/ | ☐ |
| 43 | Can You Work While in Outpatient Rehab | /can-you-work-while-in-outpatient-rehab/ | ☐ |
| 44 | Virtual Rehab California | /virtual-rehab-california/ | ☐ |
| 45 | Online Therapy Orange County | /online-therapy-orange-county/ | ☐ |
| 46 | Telehealth Addiction Treatment California | /telehealth-addiction-treatment-california/ | ☐ |
| 47 | Mental Health Treatment Near Disneyland | /mental-health-treatment-near-disneyland/ | ☐ |
| 48 | Addiction Treatment Near John Wayne Airport | /addiction-treatment-near-john-wayne-airport/ | ☐ |
| 49 | Rehab Near Newport Beach | /rehab-near-newport-beach-ca/ | ☐ |
| 50 | Rehab Near Irvine California | /rehab-near-irvine-ca/ | ☐ |
| 51 | Addiction Treatment for Veterans | /veteran-addiction-treatment-california/ | ☐ |
| 52 | Veterans Mental Health Treatment | /veterans-mental-health-treatment-orange-county/ | ☐ |
| 53 | Court Ordered Rehab California | /court-ordered-rehab-california/ | ☐ |
| 54 | Drug Diversion Program Orange County | /drug-diversion-program-orange-county/ | ☐ |
| 55 | DUI Rehab Programs California | /dui-rehab-programs-california/ | ☐ |
| 56 | Sober Living Orange County | /sober-living-orange-county/ | ☐ |
| 57 | Transitional Housing After Rehab | /transitional-housing-after-rehab/ | ☐ |
| 58 | Relapse Prevention Planning | /relapse-prevention-planning/ | ☐ |
| 59 | Signs of Relapse | /signs-of-relapse-addiction/ | ☐ |
| 60 | When to Go to Rehab | /when-to-go-to-rehab/ | ☐ |
| 61 | Is Alcohol Detox Dangerous | /is-alcohol-detox-dangerous/ | ☐ |
| 62 | Fentanyl Withdrawal Symptoms | /fentanyl-withdrawal-symptoms/ | ☐ |
| 63 | Cocaine Withdrawal Symptoms | /cocaine-withdrawal-symptoms/ | ☐ |
| 64 | Meth Withdrawal Timeline | /meth-withdrawal-timeline/ | ☐ |
| 65 | Heroin Withdrawal Timeline | /heroin-withdrawal-timeline/ | ☐ |
| 66 | Xanax Withdrawal Symptoms | /xanax-withdrawal-symptoms/ | ☐ |
| 67 | Marijuana Addiction Treatment | /marijuana-addiction-treatment-orange-county/ | ☐ |
| 68 | Ketamine Addiction Treatment | /ketamine-addiction-treatment-california/ | ☐ |
| 69 | Prescription Drug Rehab Orange County | /prescription-drug-rehab-orange-county/ | ☐ |
| 70 | Adderall Addiction Treatment | /adderall-addiction-treatment-orange-county/ | ☐ |
| 71 | Young Adult Rehab Orange County | /young-adult-rehab-orange-county/ | ☐ |
| 72 | Teen Mental Health Treatment Orange County | /teen-mental-health-treatment-orange-county/ | ☐ |
| 73 | Rehab for College Students California | /rehab-for-college-students-california/ | ☐ |
| 74 | Anxiety and Depression Treatment Near Me | /anxiety-and-depression-treatment-near-me/ | ☐ |
| 75 | Best Outpatient Rehab Orange County | /best-outpatient-rehab-orange-county/ | ☐ |
| 76 | Best Mental Health Treatment Orange County | /best-mental-health-treatment-orange-county/ | ☐ |
| 77 | Orange County Addiction Treatment Guide | /orange-county-addiction-treatment-guide/ | ☐ |
| 78 | Orange County Mental Health Resource Guide | /orange-county-mental-health-resource-guide/ | ☐ |
| 79 | Orange County Detox Guide | /orange-county-detox-guide/ | ☐ |
| 80 | Orange County Rehab Admissions Guide | /orange-county-rehab-admissions-guide/ | ☐ |
| 81 | Mental Health Crisis Help Orange County | /mental-health-crisis-help-orange-county/ | ☐ |
| 82 | Suicidal Thoughts Help California | /suicidal-thoughts-help-california/ | ☐ |
| 83 | Burnout Recovery Program Orange County | /burnout-recovery-program-orange-county/ | ☐ |
| 84 | High Functioning Anxiety Treatment | /high-functioning-anxiety-treatment/ | ☐ |
| 85 | Failure to Launch Young Adult Program | /failure-to-launch-program-orange-county/ | ☐ |
| 86 | Social Anxiety Treatment Orange County | /social-anxiety-treatment-orange-county/ | ☐ |
| 87 | Grief Counseling Orange County | /grief-counseling-orange-county/ | ☐ |
| 88 | Therapy for Healthcare Workers | /therapy-for-healthcare-workers-orange-county/ | ☐ |
| 89 | Mental Health Treatment for Entrepreneurs | /mental-health-treatment-for-entrepreneurs/ | ☐ |
| 90 | Orange County Behavioral Health Hub | /orange-county-behavioral-health-hub/ | ☐ |
- **link anchor** (#86–90) — hub pages; build first so siblings have link targets.

## Suggested build order
Hub (#86–90) → Crisis + Emergency (#27–29, 61–66) → Substance (#35–43) → everything else → LA Geo at scale (#1–22).
