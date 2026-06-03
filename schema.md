---
name: schema.md
description: Generate a complete, valid enterprise JSON-LD @graph for a broadwaytreatmentcenter.com page (detox/rehab, couples, withdrawal, insurance, Orange County geo, emergency pages). Use whenever the user provides a page URL/topic/title/meta/H1 and asks for schema, JSON-LD, or structured data. Output is one ready-to-paste <script> tag, Google-valid, with stable @IDs. Pairs with wordpress.md and url.md.
---

# Rehab Schema Skill (broadwaytreatmentcenter.com)

## Output rule
Output **one valid JSON-LD `<script type="application/ld+json">` block only**, no prose before or after. Single `@graph` array.

## Inputs needed (collect or infer)
Full page URL, page topic, SEO title, meta description, H1, primary + secondary keyword, page type (from url.md), datePublished/dateModified, approx word count, breadcrumb pillar.

## Business typing, the E-E-A-T decision (locked)
Use the **hybrid**: `Organization` + `MedicalOrganization`, joined by shared @IDs.

**Do NOT type the entity as `LocalBusiness`, `MedicalBusiness`, `MedicalClinic`, or `Hospital`.** Broadway presents as a referral/placement service, not a treatment facility; typing it as a care-delivering medical business would (a) contradict the site's own "not a treatment facility" disclosure and (b) be an accuracy problem on a YMYL page. `MedicalOrganization` is the correct, valid type for a health-topic organization that does not itself have to be a clinic.

**Address handling (the difference from a no-address network):** Broadway HAS a real, verifiable address (18582 Beach Blvd, Suite 214, Huntington Beach, CA 92648). So, unlike a pure national network, we DO attach a real `PostalAddress` and `Place` with the true street, city, state, postal code, and country. Real address data is truthful and supports local relevance. We just never wrap it in a `LocalBusiness`/`MedicalClinic` type. Every value stays accurate; nothing is fabricated.

`MedicalOrganization` carries topical authority via `knowsAbout`, positioned as a referral/information network, **not** a treatment provider. Never imply the site delivers care directly. (`Article.author`/`publisher` = Organization.)

> Ranking note to surface to the user when relevant: a named credentialed medical reviewer (Person -> `reviewedBy` on the WebPage/Article) is a strong YMYL trust signal. If the page displays a real reviewer with a real credential, add it; never invent a reviewer name or license number, as a fake credential is both a policy risk and an accuracy problem. If unknown, omit and flag it as an easy lever to add later.

## Validity rules (prevent Rich Results errors)
- `medicalSpecialty` must use real schema.org `MedicalSpecialty` enum values. **Valid:** `Psychiatric`. Do NOT use "AddictionMedicine", "MentalHealth", "BehavioralHealth", "Addiction", "Detox", etc., none are in the enum and they throw warnings. Put those concepts in `knowsAbout` (free text) instead.
- No `aggregateRating`, `review`, or `Review` nodes. No verified review data exists; fabricating it is a policy violation. (Broadway's pages cite a Joint Commission Gold Seal from its provider era; do NOT render that as a `Rating`/`Review`. If used at all, it belongs only in prose, attributed to network partners, never as schema rating data.)
- No recovery guarantees, no diagnosis language anywhere in text values.
- Avoid `Offer`/`price` on the Service node (a price:0 on a treatment-adjacent service reads as "free treatment"). Describe the service without a priced Offer.
- FAQ answers: medically cautious, encourage emergency care where relevant, no diagnosis.
- All URLs absolute and real; only link pages that EXIST per url.md. Never emit a URL from url.md's "DON'T exist" list.
- `inLanguage`: "en-US". Phone: "+1-714-400-2048".

## FAQ rich-result caveat (set expectations)
Google restricts FAQ rich results to recognized authoritative health/gov sites (since 2023). Keep FAQPage markup regardless, Bing and AI engines (ChatGPT/Gemini/Perplexity) still parse it, but don't promise FAQ star features in the SERP.

## Stable @IDs (site-level constant, page-level templated)
Site: `#organization`, `#medicalorganization`, `#website`, `#place`, `#contact`
Page: `{URL}#webpage`, `{URL}#article`, `{URL}#faq`, `{URL}#service`, `{URL}#breadcrumb`, `{URL}#terms`
Topic Things: `{URL}#primary-topic`, plus `#medical-detox`, `#addiction-treatment`, `#couples-rehab`, `#withdrawal`, `#behavioral-health` (customize to page).

## Site-level constants (verified, reuse on every page)
- Organization/MedicalOrganization name: "Broadway Treatment Center"
- url: "https://broadwaytreatmentcenter.com/"
- telephone: "+1-714-400-2048"
- address: 18582 Beach Blvd, Suite 214, Huntington Beach, CA 92648, US
- areaServed: Orange County / California (and US as the outer bound). Broadway's footprint is California, not national; prefer "Orange County, California" / a State node over a bare US-only claim on geo pages.
- sameAs: include only real, verified profiles (e.g. the site's actual Facebook/X if confirmed). Omit any profile you cannot verify, never invent one.

## @graph node checklist
1. **Organization** `#organization`, name, url, telephone, logo (ImageObject), address (PostalAddress, real), contactPoint ref, sameAs (real profiles only, omit if unknown).
2. **MedicalOrganization** `#medicalorganization`, referral/info network; `medicalSpecialty: ["Psychiatric"]`; `knowsAbout: [...]` full topic list; `areaServed` Orange County / California; `address` (real PostalAddress, same as Org); do NOT mark as a treatment provider or a LocalBusiness/Clinic.
3. **ContactPoint** `#contact`, telephone, contactType "customer service", areaServed US, availableLanguage English.
4. **Place** `#place`, real PostalAddress (street, city, region CA, postalCode, country US). A `geo` (GeoCoordinates) may be included since the address is real; if you don't have verified lat/long, omit `geo` rather than guessing.
5. **WebSite** `#website`, publisher -> Organization; SearchAction potentialAction.
6. **WebPage** `{URL}#webpage`, isPartOf website; publisher -> Organization; about -> #primary-topic; mainEntity -> article/faq/service; mentions -> topic Things; significantLink -> real internal links from url.md; inLanguage; optional reviewedBy -> Person (only if a real reviewer is displayed).
7. **Article** `{URL}#article`, headline (H1), description (meta), author + publisher -> Organization, mainEntityOfPage -> webpage, datePublished/dateModified, articleSection, keywords, wordCount, inLanguage.
8. **Service** `{URL}#service`, page-specific name (detox->"Medical Detox Placement & Withdrawal Guidance"; couples->"Couples Addiction Treatment Navigation"; withdrawal->"Withdrawal Education & Detox Guidance"; insurance->"Insurance Verification & Treatment Navigation"); provider -> MedicalOrganization; areaServed Orange County / California; audience; serviceOutput list; NO priced Offer.
9. **BreadcrumbList** `{URL}#breadcrumb`, Home > [pillar by page type] > [Page]. Use real pillar URLs from url.md (e.g. /treatment/, /treatment/orange-county-detox/, /treatment/couples-addiction-treatment-program/, /unique-services/, /insurance-verification/). Never use a pillar URL that isn't in the EXIST list.
10. **FAQPage** `{URL}#faq`, 8-12 Question/acceptedAnswer pairs, pulled from the page's actual FAQ; medically cautious.
11. **DefinedTermSet** `{URL}#terms` + **DefinedTerm** children, the page's clinical entities (medical detox, withdrawal, dual diagnosis, MAT, CIWA-Ar, COWS, etc.) as a glossary set.
12. **Thing** entities, `#primary-topic` + the mentioned topic Things, each with name + description, referenced by WebPage about/mentions.

## Cross-checks before output (run all, in order)
1. **Type check:** no `LocalBusiness`, `MedicalBusiness`, `MedicalClinic`, or `Hospital` anywhere. Entity is `Organization` + `MedicalOrganization` only.
2. **Specialty check:** `medicalSpecialty` contains only valid enum values (`Psychiatric`). Everything else is in `knowsAbout` free text.
3. **No-rating check:** no `aggregateRating`, `Rating`, `review`, or `Review` nodes anywhere.
4. **No-priced-offer check:** the Service node has no `Offer` or `price`.
5. **URL check:** every `url`, `significantLink`, `item` (breadcrumb), and `sameAs` is absolute, and every internal URL appears in url.md's EXIST list. No "DON'T exist" URLs (no /couples-assessment/, /crisis-support/, no out-of-state geo).
6. **Truthful-data check:** address is the real Broadway address; no invented reviewer name/license, no invented social profiles, no guessed geo coordinates.
7. **Voice check:** no text value implies Broadway delivers treatment directly ("our facility treats", "we admit"). Service/Org descriptions use referral/placement framing.
8. **Dates/counts check:** datePublished, dateModified, wordCount, keywords are filled with real values, not placeholders.
9. **JSON validity check:** valid JSON, no trailing commas, all braces/brackets closed, single `@graph` array, single `<script>` tag. Mentally parse it before output; if unsure, state the one risky spot rather than emit invalid JSON.
