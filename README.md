# biblioteka-portal

# Business website: project overview

## Goal
Replace our Tilda website with a simple, low-cost business site that shows business information and a schedule.

The business is Biblioteka, a library offering children's classes in Edinburgh, Scotland ([Instagram](https://www.instagram.com/biblioteka_edinburgh/)). Its Instagram page title lists Russian, art, books, theatre and maths.

## Decisions
- Do not use Wix or Tilda. Wix costs too much, and as far as we know Tilda's free plan has no custom domain.
- Technical complexity is not a concern, so choose the cheapest suitable setup.
- Build a static site with Astro, which generates plain HTML and needs no client-side JavaScript. Astro stays on version 6 and Node is pinned in `.node-version`, because Astro 7 needs Node 22.23.4 or newer. `npm audit` reports issues in Astro 6 that are fixed in Astro 7.3.8 (server rendering, image optimisation and the dev server). This static site has no server or image optimisation, but upgrade Node and Astro together soon.
- Host it on Cloudflare, with auto-deploy from GitHub.
- Buy the domain from Cloudflare Registrar, or Porkbun if the domain ending isn't available. Expected cost is about $10-11 per year for a .com (check at checkout).
- Do not use PHP, WordPress, or a database.
- The site is in Russian only.
- Show the schedule on the site. Parents only view it, with no online booking or payment.
- Do not copy photos from Instagram or Tilda. We reuse only the logo and event covers cleared one by one, kept in `public/events/`.
- Do not collect or show parent or child details, so the site has no forms.
- The structure follows https://abracadabra-online.com/ (structure only, none of its text or photos), with these pages: Главная, Занятия, Расписание, Библиотека, Взрослым, Мероприятия, О нас.
- The design follows the same layout: a top bar with round social icons, a bold hero, sage buttons, a coloured section of white cards and a sage FAQ. Its colours come from a five-colour palette (sage, dusty blue, mustard, terracotta, dark aubergine), set as variables at the top of `src/styles/global.css`, and PT Sans, self-hosted through `@fontsource/pt-sans` so visitors make no requests to Google.

## Current status
- The Cloudflare project is a Workers project named `biblioteka-portal`, and it builds from this repo. Do not press Retry on an old build: it redeploys that old commit.
- The live site was last built from the one-page plain HTML version. The Astro site below has not been deployed yet.
- The build runs from `build.command` in `wrangler.jsonc`, so `npx wrangler deploy` builds the site itself. The Cloudflare dashboard needs no build command, and its settings page did not show that field.
- All 7 pages exist in `src/pages/`, with shared layout in `src/layouts/Base.astro`, styles in `src/styles/global.css`, and class data in `src/data/classes.js`.
- Pages with no real content yet show a dashed placeholder block and a `TODO:` comment in the source: Библиотека and Взрослым.
- The logo is the БЫ lingvo logo, saved as `public/logo.jpg` (original in `figures_archive/logos/`). It is only 150x150px, so it is shown small.

## Pages
| Page | Path | Content | Status |
|---|---|---|---|
| Главная | `/` | Hero, section cards, upcoming events, FAQ, contacts | Done; events are a placeholder, FAQ needs review |
| Занятия | `/zanyatiya/` | Age groups, classes, duration, price | Done; text and prices supplied directly, replacing Tilda's |
| Расписание | `/raspisanie/` | Tables by group, venue, holidays | Done; classes with no days and times yet are left out |
| Библиотека | `/biblioteka/` | About, loan rules, where and when, catalogue | Numbers, loan rules, FAQ and a link to the Google Sheets catalogue done; where and when is a placeholder |
| Взрослым | `/vzroslym/` | Adult classes | All placeholders |
| Мероприятия | `/meropriyatiya/` | Upcoming and past events | One upcoming lecture on 8 November 2026 (move it to past after that date) and two past events |
| О нас | `/o-nas/` | Story, approach, teachers, contacts | Done; teachers need confirming |

## Planned free services
- Schedule display: tables on the site, or an embedded Google Calendar if someone without git access updates the schedule
- Contact: no form or service needed, just the business's published contact details and Instagram link

## Remaining work
1. Deploy the Astro site and confirm that every page opens on the `.workers.dev` link.
2. Replace the placeholders as the answers below arrive.
3. Add the custom domain in Cloudflare.
4. Add a sitemap once the domain is known, because it needs the final address.
5. Save anything still needed from the Tilda site before cancelling it.
6. If the old site has a custom domain, redirect its URLs to the new pages to help keep search rankings. A `tilda.ws` address can't be redirected from Cloudflare, so otherwise add a link to the new site on the old one before cancelling.
7. Archive the old `biblioteka_portal` GitHub repo.

## Open questions
- Is Biblioteka (@biblioteka_edinburgh) the same business as the Tilda site's Студия "БЫ lingvo" (https://bylingvo.tilda.ws/, @bylingvo)? The site now uses the БЫ lingvo logo, but its text says "Библиотека" and it links to @biblioteka_edinburgh. Which name and Instagram does the new site use?
- What are the days and times for the classes not yet in the schedule (two 8-11 classes and four 12+ classes)? Who will update the schedule and content after launch?
- Library: who can borrow, and where and when are books given out?
- Adults: which classes, on which days, at what price?
- Events: what else is planned, with dates?
- Who teaches now? The Tilda site also has a bio with no name attached (a PhD on Russian-Italian bilingualism).
- How do parents sign up: WhatsApp, Telegram and email links, or the existing Google Form? The form collects child and parent details, so keeping it means moving the privacy policy too.
- Do we already own the domain? If so, where is it registered?
- Do we have our own hero photo, with parents' consent? The hero is a solid colour until then.
