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
- Do not copy photos from Instagram or Tilda. We reuse only the logo, plus event covers, teacher photos and book club photos cleared one by one, kept in `public/events/`, `public/teachers/` and `public/adults/`.
- Do not collect or show parent or child details, so the site has no forms.
- The structure follows https://abracadabra-online.com/ (structure only, none of its text or photos), with these pages: Главная, Занятия, Расписание, Библиотека, Взрослым, Мероприятия, О нас.
- The design follows the same layout: a top bar with round social icons, a bold hero, sage buttons, a coloured section of white cards and a sage FAQ. Its colours come from a five-colour palette (sage, dusty blue, mustard, terracotta, dark aubergine), set as variables at the top of `src/styles/global.css`, and PT Sans, self-hosted through `@fontsource/pt-sans` so visitors make no requests to Google.

## Current status
- The Cloudflare project is a Workers project named `biblioteka-portal`, and it builds from this repo. Do not press Retry on an old build: it redeploys that old commit.
- The live site was last built from the one-page plain HTML version. The Astro site below has not been deployed yet.
- The build runs from `build.command` in `wrangler.jsonc`, so `npx wrangler deploy` builds the site itself. The Cloudflare dashboard needs no build command, and its settings page did not show that field.
- All 7 pages exist in `src/pages/`, with shared layout in `src/layouts/Base.astro`, styles in `src/styles/global.css`, and class data in `src/data/classes.js`.
- Pages with no real content yet show a dashed placeholder block and a `TODO:` comment in the source: Библиотека (where and when) and Взрослым (adult classes).
- The logo is the Библиотека logo (a house with a sprout and roots), saved as `public/logo.jpg` at 300x300px and also used as the favicon. The original is `figures_archive/logos/biblioteka-logo-original.jpg`.

## Pages
| Page | Path | Content | Status |
|---|---|---|---|
| Главная | `/` | Hero, section cards, upcoming events, FAQ, contacts | Done; upcoming events show a short note until the next event is announced, FAQ needs review |
| Занятия | `/zanyatiya/` | Age groups, online classes, duration, price | Done; text and prices supplied directly, replacing Tilda's. Online classes are `onlineGroup` in `src/data/classes.js`, kept out of the home page counts and the schedule |
| Расписание | `/raspisanie/` | Tables by group, venue, holidays | Done; classes with no days and times yet are left out |
| Библиотека | `/biblioteka/` | About, loan rules, where and when, catalogue | Photos (`public/library/`), numbers, loan rules, FAQ and a link to the Google Sheets catalogue done; where and when is a placeholder |
| Взрослым | `/vzroslym/` | Book club, adult classes, hosting events | Book club «Литературный Эдинбург» done with six photos with no recognisable faces (`public/adults/`) and a call to host adult events in the library, but its meeting time, place, price and how to join are missing; adult classes are a placeholder |
| Мероприятия | `/meropriyatiya/` | Upcoming and past events | No upcoming events yet (placeholder); three past events, newest first: the cults lecture on 8 November 2026, the biologist lecture and the toy swap |
| О нас | `/o-nas/` | Story, approach, teachers, contacts | Done; four people for now (three teachers and Алёна, the library manager), more to come |

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
- The site now uses the name, logo, email and Instagram of Библиотека, but its Telegram link is still @bylingvo. Is that still the right Telegram?
- What are the days and times for the classes not yet in the schedule (two 8-11 classes and four 12+ classes)? Who will update the schedule and content after launch?
- Library: who can borrow, and where and when are books given out?
- Adults: which classes, on which days, at what price? When and where does the book club meet, does it cost anything, and how do people join?
- Events: what else is planned, with dates?
- Which other teachers should the site show? Катя is in the schedule but has no photo or bio yet.
- How do parents sign up: WhatsApp, Telegram and email links, or the existing Google Form? The form collects child and parent details, so keeping it means moving the privacy policy too.
- Do we already own the domain? If so, where is it registered?
- Do we have our own hero photo, with parents' consent? The hero is a solid colour until then.
