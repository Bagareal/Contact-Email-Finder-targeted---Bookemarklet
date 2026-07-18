# Contact Email Finder — Bookmarklet

A lightweight browser bookmarklet that helps you find a website's public contact
email when it's buried, missing from the navigation, or hidden behind an
unhelpful contact form.

## Why I made this

I kept running into the same frustrating situation: I needed to reach a
company — for a complaint, a question, a support request — and their website
simply didn't make it easy. No visible email, a contact form that goes
nowhere useful, and the "Contact" link (if it even exists) buried three
clicks deep. Opening dozens of pages by hand just to find one email address
felt like a waste of time for something that should be simple.

So I built this: instead of blindly crawling an entire site page by page, it
checks a small, targeted set of places where a contact email is most likely
to be — the homepage, common contact/about/legal paths (in the site's own
language, detected automatically, plus English as a fallback), the page
footer, and structured data (JSON-LD) that many sites embed. It stops there.
It's meant to save a few minutes of manual clicking, not to replace it
entirely.

## What it does

- Scans the current page and a small set (~40) of likely pages on the same
  domain: `/contact`, `/about`, `/privacy`, `/legal`, `/support`, and their
  equivalents in French, German, Italian, Spanish, Portuguese, and Dutch —
  prioritized based on the site's detected language.
- Tries common file extension variants too (`.php`, `.html`, `.aspx`), to
  cover older or enterprise sites that don't use extensionless URLs.
- Reads the site's `sitemap.xml` (or `sitemap_index.xml`) first and
  prioritizes any real, verified contact/about/legal pages it finds there
  over guessed paths.
- Follows footer links automatically, since contact info is conventionally
  placed there regardless of language.
- Reads structured data (`application/ld+json`) that some sites use to
  publish contact info in a machine-readable format.
- Filters out obvious false positives: tracking IDs (e.g. Sentry keys),
  image filenames like `logo@2x.png`, and placeholder addresses like
  `someone@example.com`.
- **Checks `robots.txt` first** and skips any page the site has explicitly
  marked as off-limits to automated access.
- Shows everything in a small on-page panel — no data leaves your browser,
  nothing is stored or sent anywhere.

## What it does *not* do

- It does not crawl an entire website. It checks a fixed, small list of
  likely pages — never more than ~40 requests per run.
- It does not follow links recursively beyond that initial list.
- It does not bypass logins, paywalls, CAPTCHAs, or any access restriction.
- It does not store, transmit, or share anything it finds — everything stays
  local to your browser tab.

## Installation

1. Open the file [`contact-finder-bookmarklet.txt`](./contact-finder-bookmarklet.txt)
   and copy its entire contents (it starts with `javascript:`).
2. In your browser, create a new bookmark (any page, any name).
3. Open your browser's **bookmark manager** (not the address bar — most
   browsers strip `javascript:` URLs pasted directly into the address bar)
   and edit that bookmark's URL field, pasting the copied code there.
4. Save it. Click the bookmark while on the website you want to search.

## ⚠️ Intended use — please read

This tool is meant for **occasional, individual use**: finding a contact
email for a company you personally need to reach, when the normal channels
make it unreasonably hard.

**Please do not use this to:**
- Build mailing lists or contact databases for marketing, cold outreach, or
  bulk/unsolicited email campaigns.
- Scrape emails at scale across many sites.
- Harvest personal data belonging to individuals rather than
  organizations/businesses.

Collecting a published email address is not automatically the same as
having the right to email it — in the EU, sending unsolicited commercial
email without a legal basis violates GDPR and the ePrivacy Directive, and
similar rules exist elsewhere (e.g. CAN-SPAM in the US). Using this tool to
build spam lists is both against its intended purpose and, depending on
what you do with the data, potentially illegal. Use it responsibly.

## License

MIT — provided as-is, no warranty. See [LICENSE](./LICENSE) for details.
