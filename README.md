# book-kingdom

Google Ads landing page for Kingdom Appliance Repair — `book.kingdomappliancerepairfl.com`.

Static single page, deployed on Vercel. Headline personalizes from URL params set in the ad campaign's final URLs.

## URL parameters

| Param | Values | Effect |
|---|---|---|
| `appliance` | `refrigerator`, `fridge`, `washer`, `dryer`, `oven`, `stove`, `range`, `dishwasher`, `icemaker`, `freezer` | Headline becomes e.g. "Dryer Repair Near You"; matching appliance card highlights; booking form pre-selects it |
| `brand` | `samsung`, `lg`, `whirlpool`, `maytag`, `ge`, `frigidaire`, `kitchenaid`, `bosch`, `kenmore`, `electrolux`, `amana` | Prefixes headline, e.g. "Maytag Dryer Repair Near You"; brand highlights in the brand strip |

Unknown/missing values fall back to "Appliance Repair Near You" — a bad param can never break the page.

Examples:

- `/?appliance=dryer` → Dryer Repair Near You
- `/?appliance=dryer&brand=maytag` → Maytag Dryer Repair Near You

## Tracking

- GTM container `GTM-MKZ8K9C3` (same as main site)
- `dataLayer` events: `call_click` (any tel link) and `lead_form_submit` (form success), both carry `appliance` and `brand` — map these to Google Ads conversions in GTM
- Page is `noindex` (meta + `X-Robots-Tag` header via `vercel.json`)

## Lead form

Posts via FormSubmit.co AJAX to david@graphicworksdesign.com. First real submission triggers a one-time FormSubmit activation email — click the confirm link in it or leads won't deliver. Swap to the FormSubmit random-string endpoint after activation to hide the email from scrapers.

## DNS

GoDaddy: CNAME `book` → `cname.vercel-dns.com`, then add `book.kingdomappliancerepairfl.com` as the domain in the Vercel project.
