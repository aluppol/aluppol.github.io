# Texts and languages

The site is in English and Russian. Every visible text lives in one file per language:

- `en.json`: English, the default, served at the site root (`/`, `/projects/`, `/privacy/`)
- `ru.json`: Russian, served under `/ru/`

The page layouts are the templates in `../src/` (one per page). A template shows a text by its key: `{{home.hero.title}}` is `"home" → "hero" → "title"` in the JSON files.

## Change a text

1. Edit the value in the JSON file of that language (keep the keys identical in both files).
2. In the repository root run `python3 build.py`. It rewrites `index.html`, `projects/`, `privacy/` and `ru/…`.
3. Commit the JSON together with the generated HTML. GitHub Pages serves the HTML as it is.

`python3 build.py --check` fails if the committed HTML is not what the sources produce; run it before pushing. If a key is missing in any language, the build stops, names the key and writes nothing.

## Inside a text

- `**bold**` makes bold text; `[text](address)` makes a link (a text must link to the same addresses in both languages).
- `\n` is a line break; `­` is a soft hyphen, a place where a long word may break on a narrow phone.
- `{{site.email}}` inserts another key's text.
- Texts used in the page title or meta tags must be plain; the build says so if one is not.

## Add a text or a page

Add the key to both files and use `{{key}}` in the template. A new page is a new `src/<name>.html`, served at `/<name>/` and `/ru/<name>/`. Links to this site's pages are written `{{@prefix}}/projects/` so that they stay in the reader's language; links to the live demos end in `{{@demo}}`, which adds `?lang=ru`.

## Rules

- Product names, technologies, and people's and company names stay in Latin script in every language.
- `/sig/` is not generated and stays English. Never move or rename anything in it: Gmail caches the signature images by address.
