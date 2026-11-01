# AGENTS.md

Static business website replacing a Tilda site. [README.md](README.md) holds the goal, decisions, current status, plan and open questions. Read it before planning work and follow its order: the deploy check comes before building the site.

## Rules

- **Static only.** The output is files served by Cloudflare. Cover dynamic needs with the services listed in the README. If a request seems to need a server or database, raise it with the user before building.
- **Light by default.** Build with HTML and CSS. Add JavaScript or a dependency only when a feature needs it.
- **Real business facts.** Hours, prices, addresses, phone numbers and names come from the user, the Tilda site or the Instagram account linked in the README. Mark anything missing with `TODO:` and list those gaps when you report back.
- **Logo only.** The logo is the only image taken from Instagram or Tilda. Anything committed stays in the public git history even after deletion.
- **Russian site.** Write all visitor-facing text in Russian, set `lang="ru"`, and choose fonts that include Cyrillic.
- **No personal data.** The site has no forms. Parents get in touch through the published contact details.
- **Public by default.** The GitHub repo and the built site are both public. Commit only what is safe to publish, and keep credentials and customer data out.
- **README stays current.** When a decision or the status changes, update the README in the same change.

## Deployment

- Cloudflare deploys automatically from GitHub, so a push to `main` publishes the live site. Push only when the user asks.
- Cloudflare project settings live in its dashboard and can't be seen from this repo. When a change needs a new setting, such as the build command or output directory, give the user the exact values to enter.
- When a deploy fails, ask the user for the build log and diagnose from that.
- Development is on Windows and Cloudflare builds on Linux, where paths are case-sensitive. Match the case of file names exactly in imports and links.

## Definition of done

A site change is done when all of these hold:

1. The build passes, if the project has a build step.
2. Each changed page renders correctly at phone width (375px) and desktop width, with no horizontal scrolling.
3. Links and embeds on those pages work.
4. Your report lists every `TODO:` you added and anything you could not verify.
