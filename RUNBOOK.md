# Sway creator brief site: team runbook

What it is: the Sway Korea creator brief as a bilingual (EN/KO) single-page site with two tabs, About Sway and Product Guide. Built from the client-cleared "Sway KOL Outreach Brief & Guide" Doc (November 17th, 2026). Same build as the Button panel site.

## Files
- `index.html`: English entry (opens in EN, unfurls in EN)
- `ko/index.html`: Korean entry (opens in KO, unfurls in KO)
- `vercel.json`: clean URLs, no trailing slash
- `og.png` / `og-ko.png`: Telegram/X link previews (EN and KO), referenced by absolute URL on sway-brief.vercel.app (the production URL), so the preview works on the Vercel link and on both subdomains
- Self-contained: logo, favicon and all 20 guide screenshots are embedded. Only fonts load from Google Fonts and Fontshare.

## Deploy (Vercel, team holo-hive)
1. Private GitHub repo `bolt-hh/sway-creator-brief` (same pattern as `button-council-brief`). Upload these files to `main`. Jdot pushes; never run git inside the shared mount.
2. Import into Vercel under team holo-hive as project `sway-creator-brief`, framework preset Other, no build command.
3. Enable Vercel Web Analytics on the project (the snippet is already in both entries).

## Subdomains (Andy)
- `sway.holohive.io` → the EN entry (`/`)
- `sway-kr.holohive.io` → the KO entry (`/ko`)
The EN/KO switch on the page navigates between these two hosts and keeps the hash, so `#guide` links survive a language switch. KOLs only ever get these two links, never a `*.vercel.app` URL. Korean creators get `sway-kr.holohive.io`.

## The guide lock
The Product Guide tab is locked by default: it shows a padlock and a "unlocks once you are onboarded" panel. After each creator's one-on-one onboarding, send them the unlock link instead of the plain one:
- Korean: `https://sway-kr.holohive.io/#guide-onboarded`
- English: `https://sway.holohive.io/#guide-onboarded`
The unlock survives a refresh and the EN/KO switch. It is front-end only, like Button's: anyone who has the unlock link can open the guide, so it is a soft gate, not access control. To retire the gate later (as Button did once its panel was seated), set `OPEN=true` in the script.

## Launch checks (site-audit)
- Real phone, both languages: both tabs, every screenshot opens and closes, chips jump to the right section, back-to-top appears.
- Every link opens (App Store, Google Play, website, docs, support, security review, X, Telegram, Discord).
- Paste `sway-kr.holohive.io` into Telegram: the preview must show the Korean title. Same for the EN host.
- Plain link shows the padlock and the locked panel; the `#guide-onboarded` link opens the guide, in both languages.
- Desktop at 1440px: the guide's section list sits on the left and highlights the section in view.

## Small edits later
Copy lives in `content.py` (About tab) and `guide.py` (Product Guide tab) in the source folder; rebuild with `python3 build.py <outdir>`. Fee numbers, the app links and the Cerebro figures are the likeliest to change. Re-run the HQC gate and a link check after any edit.
