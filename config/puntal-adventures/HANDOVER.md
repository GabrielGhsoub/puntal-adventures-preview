# Puntal Adventures, private enquiry demo: handover

Built 2026-10-10 for Roy ("Puntalito"), Lead Guide and Founder, Puntal
Adventures, Santa Cruz de Tenerife. He asked for the demo in his reply; the
cold email offered a short form that collects level, dates and group size
before he answers.

## Links

- Live demo: https://gabrielghsoub.github.io/puntal-adventures-preview/
- Owner panel: https://gabrielghsoub.github.io/puntal-adventures-preview/admin/puntal-adventures
  (deep links return HTTP 404 on GitHub Pages but render through 404.html;
  the requests inbox is the "Requests" / "Solicitudes" tab)
- Repo: GabrielGhsoub/puntal-adventures-preview (noindex meta plus robots.txt,
  written by build-poc; unlisted, not linked anywhere)
- Rebuild and republish: `npm run build-poc -- --slug puntal-adventures --publish`

## What the demo is

An ENQUIRY flow (`bookingMode: request`), not instant booking: the visitor
picks a day, the number of people, one of his activities, answers "Your
level", adds a note, accepts the conditions and sends. Nothing is booked, no
payment step exists, and every price line carries the note that the figures
are examples to be replaced by Roy's own. Roy sees the request, with the
level answer, in the owner panel and can approve or decline it there (all
simulated, browser only).

English first, Spanish second, both switchable in the header. The footer
reads "A private demonstration built for Puntal Adventures. Nothing is
booked and no payment is taken." (Spanish equivalent on the ES surface).

## Brand values and their sources

| value | used | source |
|---|---|---|
| business name | Puntal Adventures | header wordmark and footer on https://www.puntaladventures.com/ |
| primary (buttons) | #D35400 | `--color-primary` in https://www.puntaladventures.com/css/style.css, his `.btn-primary` background and the bold half of the "PuntalAdventures" wordmark |
| accent (headings, focus) | #2C3E50 | `--color-secondary` in the same stylesheet, his h1 to h4 colour and the dark contact card |
| neutral (surface tint) | #2C3E50 | same, so the grey surfaces lean cool like his `#F8F9FA` panels |
| font pairing | modern (Space Grotesk display, Inter body) | his site loads Manrope, a geometric sans; modern is the closest of the three curated pairings. The engine self hosts fonts, so Manrope itself is not an option |
| tagline EN | Premium rock climbing and adventure tours in Tenerife and the Canary Islands | his meta description on the home page |
| tagline ES | Escalada en roca premium y experiencias al aire libre en Tenerife y las Islas Canarias | his Spanish footer, https://www.puntaladventures.com/es/index.html |
| currency | EUR | Spain; he publishes no prices |
| address and phone (in the meeting point line) | Calle Doctor Fleming 10, Santa Cruz de Tenerife; +34 628 34 72 92, call or WhatsApp | https://www.puntaladventures.com/contact.html |
| registration | TA-4-0026562 | as given in the lead brief (active tourism register); not found on his pages, so say so if he asks where we got it |
| "replies within 24 hours" | confirmation and conditions text | his contact page: "our guides will get back to you within 24 hours" |

## Activities (his real four, climbing split in half and full day as his site does)

Descriptions are shortened from his own /experiences copy in each language,
nothing added. Capacities are NOT published anywhere on his site; the 6 and 8
below are modelling choices so the people stepper has a ceiling, and each
card says "larger groups ask Roy".

| unit | name | capacity (placeholder) | price (PLACEHOLDER) |
|---|---|---|---|
| climbing-half-day | Rock Climbing, half day | 6 | EUR 75 per person |
| climbing-full-day | Rock Climbing, full day | 6 | EUR 120 per person |
| hiking-teide | Hiking, Mount Teide and beyond (4 to 6 hours) | 8 | EUR 60 per person |
| canyoning | Volcanic Canyoning, half day | 8 | EUR 85 per person |
| multi-day | Multi-day Adventure, tailor-made | 6 | EUR 150 per person per day, as a starting point; the card says Roy quotes the whole trip |

## Prices: ALL placeholders

puntaladventures.com publishes no prices on any page (home, experiences,
about, contact, FAQ, terms, in either language; FAQ and Terms pages read
"Coming Soon"). Every figure above is an example value. The demo says so in
three places: the estimate note under every total ("Example prices for this
demo, to be replaced by Roy's own"), the conditions text, and the multi-day
card itself. When Gabriel or Emile sends the link, say it plainly: the
prices are placeholders and we drop his real ones in minutes.

Other placeholders or modelling choices:
- Cancellation terms: none published (his Terms page is "Coming Soon"); the
  conditions text says so and marks that line as a placeholder.
- Blocked dates and season: none. His FAQ says climbing runs comfortably
  October to May and shaded crags in summer, so no month is closed.
- The multi-day trip is booked as a single start date (experience kind);
  the note field asks for the number of days and islands.
- Group size above capacity: the stepper stops at the unit's ceiling.
- `images.hero` is set but the widget surface does not render a hero; the
  photographs show on the activity cards.

## Photographs

All his own, from https://www.puntaladventures.com/assets/images/, converted
to WebP (all under 120 KB). Full table in `images/CREDITS.md`. No stock, no
generated images, no minors. His portrait (foto_roy.jpg) was not used.

- hero.webp: hero_climbing_tenerife.png (home hero)
- climbing.webp: experience_climbing.png (half day card)
- sunset-climb.webp: hero_climbing_2.png (full day card, gallery)
- hiking.webp: experience_hiking.png
- canyoning.webp: experience_canyoning.png (carries his own wordmark in the corner)
- adventure.webp: experience_adventure.png (multi-day card)
- gorge-climb.webp: hero_climbing_3.png (gallery)

His site serves the photos at 640 by 640 px, which is the ceiling of what
the demo can show.

## The extra questions feature (new, generic, engine level)

Added in commit `d22ba4a`: a config may declare `extraQuestions`, an array of
`{ id, label (per language), type: select | text, options [{ id, label }],
hint, required }`. The engine renders them on the details step after the
phone field, validates required ones, repeats each answer on the
confirmation (a select by its label), stores them on the booking as
`answers` and shows them in the owner panel's request inbox under the
message. Default empty: every existing config is untouched (426 tests pass,
three new schema tests and three new store tests cover it). Two UI keys were
added in all five languages: `guest.selectPlaceholder` and
`guest.errorRequired`.

This config uses one required select, "Your level" / "Su nivel": Beginner,
first time; Some experience; Experienced; Expert. The free text "Anything
else?" / "Algo más" is the existing message field with a hint asking where
they stay, a preferred start time and, for multi-day, the days and islands.

## Verified on 2026-10-10

Playwright (Google Chrome, headless) drove both languages end to end on the
dev server and on the live Pages site: five cards render with his photos;
the level select is present with the four options; submitting without a
level shows the required error; the confirmation repeats "Your level:
Experienced" / "Su nivel: Algo de experiencia"; the private demo notice is
on screen; no dash characters and no inverted question mark on the details
or confirmation screens; the owner panel's Requests tab lists both requests
with their level answers. The live bundle carries only the
`puntal-adventures` slug (no wadi, escuela or resu config rides along).

## Commits (likwiid-direct, main)

- d22ba4a feat: config driven extra questions on the details step, repeated on the confirmation and in the request inbox
- ada8540 feat: puntal adventures per-lead enquiry demo on his four activities with a level question
- (this file) docs: puntal adventures handover
