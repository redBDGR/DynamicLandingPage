# Dynamic Landing Page

An extremely basic, single-page holding site hosted on Azure Static Web Apps. Any domain can be pointed at it, and the page adapts itself to whichever domain it's being accessed from - so one deployment covers every parked domain until a proper website is built for it.

## How it works

- The whole site is a single [index.html](index.html) with inline CSS and JavaScript - no build step, no dependencies.
- On load, a small script reads `window.location.hostname`, strips any leading `www.`, takes the first label and capitalises it. That name is used as both the page heading and the browser tab title.
  - `example.com` -> **Example**
  - `www.another-domain.com.au` -> **Another-domain**
- The heading has a subtle animated sheen that replays every few seconds (disabled for users who prefer reduced motion).
- A contact button and footer provide a way to get in touch in the meantime.

## Deployment

Pushes to `main` are deployed automatically by the GitHub Actions workflow in [.github/workflows/](.github/workflows/), which publishes the repository root to Azure Static Web Apps.

## Adding a domain

1. In the Azure portal, open the Static Web App and go to **Custom domains**.
2. Add the domain (and `www.` variant if required) and follow the validation steps.
3. Create the DNS records at your registrar as instructed (CNAME for subdomains, TXT + ALIAS/A record for apex domains).

Once validated, the domain will serve the landing page with its own name displayed - no code changes required.

## Repurposing

To use this for your own domains, update the following in [index.html](index.html):

- The `mailto:` address on the **Email us** button.
- The footer business name and ABN.
- The `<meta name="description">` text.
- Colours and fonts via the CSS variables in `:root`.

When a domain gets its own website, simply remove it from the Static Web App's custom domains and point its DNS at the new site.
