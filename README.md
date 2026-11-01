# biblioteka_portal

# Business website: project overview

## Goal
Replace our Tilda website with a simple, low-cost business site that shows business information and a schedule.

The business is Biblioteka, a library offering children's classes in Edinburgh, Scotland ([Instagram](https://www.instagram.com/biblioteka_edinburgh/)). Its Instagram page title lists Russian, art, books, theatre and maths.

## Decisions
- Do not use Wix or Tilda. Wix costs too much, and as far as we know Tilda's free plan has no custom domain.
- Technical complexity is not a concern, so choose the cheapest suitable setup.
- Build a static site using Astro or plain HTML.
- Host it on Cloudflare, with auto-deploy from GitHub.
- Buy the domain from Cloudflare Registrar, or Porkbun if the domain ending isn't available. Expected cost is about $10-11 per year for a .com (check at checkout).
- Do not use PHP, WordPress, or a database.
- The site is in Russian only.
- Show the schedule on the site. Parents only view it, with no online booking or payment.
- Do not copy photos from Instagram or Tilda. The logo is the only image we reuse.
- Do not collect or show parent or child details, so the site has no forms.

## Current status
- The Cloudflare account is created, and the project is a Workers project.
- Cloudflare copied this repo into a separate repo, `biblioteka-portal` (hyphen), and builds from that copy. Reconnect the project to this repo, `biblioteka_portal` (underscore), in the Cloudflare dashboard.
- Cloudflare's first deploy failed because that copy has no site files ("Could not detect a directory containing static files").
- A simple one-page version is in `public/index.html` (plain HTML, no build step). It has been deployed once from `main`, and it still has `TODO:` items for the name, classes, schedule and contact details.
- The logo is the БЫ lingvo logo, saved as `public/logo.jpg` (original in `figures_archive/logos/`). It is only 150x150px, so it is shown small.

## Planned free services
- Schedule display: embedded Google Calendar
- Contact: no form or service needed, just the business's published contact details and Instagram link

## First step: confirm the deploy works
1. Check the Cloudflare project type:
   - **Pages** (has "Build output directory"): set framework preset to None, leave the build command empty, and set the output directory to `public`.
   - **Workers** (has a deploy command, usually `npx wrangler deploy`): keep that command and add `wrangler.jsonc` to the repo root:
     ```jsonc
     {
       "name": "<exact Cloudflare project name>",
       "compatibility_date": "2026-11-01",
       "assets": { "directory": "./public" }
     }
     ```
2. Add a minimal `public/index.html` test page.
3. Commit and push to the main branch.
4. Confirm that the deploy succeeds and the `.pages.dev` or `.workers.dev` link opens the page.
5. If it fails, read the build log and fix the cause.

## Then build the site
1. Choose Astro or plain HTML. If using Astro, set the build command to `npm run build` and the output directory to `dist`, and update `assets.directory` to `./dist` if this is a Workers project.
2. Build the pages for business information, schedule, and contact details.
3. Reuse the text and logo from the Tilda site, and save them before cancelling Tilda.
4. Make the site mobile-friendly and add basic SEO: titles, descriptions, and a sitemap.
5. Add the custom domain in Cloudflare.
6. If the old site has a custom domain, redirect its URLs to the new pages to help keep search rankings. A `tilda.ws` address can't be redirected from Cloudflare, so otherwise add a link to the new site on the old one before cancelling.

## Questions to answer before building the site
- Is Biblioteka (@biblioteka_edinburgh) the same business as the Tilda site's Студия "БЫ lingvo" (https://bylingvo.tilda.ws/, @bylingvo)? The site now uses the БЫ lingvo logo, but its text says "Библиотека" and it links to @biblioteka_edinburgh. Which name and Instagram does the new site use?
- What are the schedule's days, times and venue? The Tilda site does not list them.
- How do parents sign up: WhatsApp, Telegram and email links, or the existing Google Form? The form collects child and parent details, so keeping it means moving the privacy policy too.
- Should the site show prices?
- Who will update the schedule and content after launch?
- Do we already own the domain? If so, where is it registered?