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
- Do not copy photos from Instagram or Tilda. The logo is the only image we reuse.
- Do not collect or show parent or child details, so the site has no forms.
- The structure follows https://abracadabra-online.com/ (structure only, none of its text or photos), with these pages: Главная, Занятия, Расписание, Библиотека, Взрослым, Мероприятия, О нас.
- The design follows the same layout: a top bar with round social icons, a bold hero, yellow buttons, a coloured section of white cards and a yellow FAQ. It uses its own colours, set as variables at the top of `src/styles/global.css`, and PT Sans, self-hosted through `@fontsource/pt-sans` so visitors make no requests to Google.

## Current status
- The Cloudflare project is a Workers project named `biblioteka-portal`, and it builds from this repo. Do not press Retry on an old build: it redeploys that old commit.
- The live site was last built from the one-page plain HTML version. The Astro site below has not been deployed yet.
- Before the first Astro deploy, set the Cloudflare build command to `npm run build` and keep the deploy command `npx wrangler deploy`.
- All 7 pages exist in `src/pages/`, with shared layout in `src/layouts/Base.astro`, styles in `src/styles/global.css`, and class data in `src/data/classes.js`.
- Pages with no real content yet show a dashed placeholder block and a `TODO:` comment in the source: the schedule's days, times and venue, plus Библиотека, Взрослым and Мероприятия.
- The logo is the БЫ lingvo logo, saved as `public/logo.jpg` (original in `figures_archive/logos/`). It is only 150x150px, so it is shown small.

## Pages
| Page | Path | Content | Status |
|---|---|---|---|
| Главная | `/` | Hero, section cards, upcoming events, FAQ, contacts | Done; events are a placeholder, FAQ needs review |
| Занятия | `/zanyatiya/` | Age groups, classes, duration, price | Done from Tilda; prices need confirming |
| Расписание | `/raspisanie/` | Tables by group, venue, holidays | Days, times and venue are placeholders |
| Библиотека | `/biblioteka/` | About, loan rules, where and when, catalogue | All placeholders |
| Взрослым | `/vzroslym/` | Adult classes | All placeholders |
| Мероприятия | `/meropriyatiya/` | Upcoming and past events | All placeholders |
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
- What are the schedule's days, times and venue? The Tilda site does not list them. Who will update the schedule and content after launch?
- Library: how many books, is there a list, who can borrow, for how long, is there a deposit, and where and when are books given out?
- Adults: which classes, on which days, at what price?
- Events: what is planned, with dates? Should past events be shown?
- Who teaches now? The Tilda site also has a bio with no name attached (a PhD on Russian-Italian bilingualism).
- Are the prices current, and should the site show them? Tilda lists £20 per 4 classes for ages 1-3 and £60 for the other groups.
- Is the 1-3 class called "Игровые встречи" (Tilda) or "Малыши с родителями" (the earlier one-page version)?
- How do parents sign up: WhatsApp, Telegram and email links, or the existing Google Form? The form collects child and parent details, so keeping it means moving the privacy policy too.
- Do we already own the domain? If so, where is it registered?
- What is the Facebook page address? The header icon is not a link until we have it (`socials` in `src/data/site.js`).
- Do we have our own hero photo, with parents' consent? The hero is a solid colour until then.
