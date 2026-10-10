# Dewey Wheel Generator

**[العربية](README.ar.md)** | English

A browser-based tool that generates a circular **Dewey Decimal Classification wheel** as a clean, editable **SVG** file. Everything runs client-side: edit the data, pick fonts and colors, preview the wheel, and export it.

The interface is multilingual. Languages live in simple JSON files, so anyone can add a new one without touching the code. Arabic (RTL) and English (LTR) are included.

## Features

- Wheel of main classes and subclasses generated from plain text data.
- Full control over fonts, font sizes and colors (text, backgrounds, circles, dividers).
- Two number orientations for the inner ring: *uniform* or *always readable*.
- Export to SVG with a custom or automatic date-time file name.
- Multilingual UI with RTL/LTR support, per-language digits (`0123` / `٠١٢٣`), fonts and sample data.
- No build step, no framework: one HTML file plus JSON language files.

## Quick start

The page loads its language files with `fetch`, so it must be served over HTTP (opening it directly with `file://` is blocked by most browsers).

```bash
git clone https://github.com/<your-user>/<repository-name>.git
cd <repository-name>
python -m http.server 8000
```

Open <http://localhost:8000>. Replace `<your-user>` and `<repository-name>` with your GitHub username and repository name.

To publish with **GitHub Pages**, choose *Settings → Pages → Deploy from a branch → `main` / root*. GitHub Pages serves `index.html` automatically.

If `lang/` cannot be loaded, the page shows a file picker so you can select the language JSON files manually.

> An internet connection is needed for Google Fonts and the jQuery CDN.

You can open a specific language with a URL parameter, e.g. `?lang=en`. Otherwise the last choice is remembered in the browser, falling back to the language marked `"is_default": true`.

## Data format

Each block describes one main class; blocks are separated by a line containing `###`.

```text
Religion = 200-299
Islam = 210
Bible = 220
Christianity = 230-280
###
Social Sciences = 300-399
Statistics = 310
```

- The **first line** of a block is the main class, the other lines are its subclasses.
- `=` separates the title from the number (the last `=` on the line is used).
- Digits are converted automatically to the selected language's digit set.
- Put `$` inside a subclass title to split it into two lines with the number in between, e.g. `Ancient Philosophy-$Medieval & Eastern = 180`.

## Data source

The Arabic Dewey classification data in `examples/data-text/` is in the public domain. It is reproduced from:

> *Mukhtaṣar al-taṣnīf fī al-maktabāt wa-niẓām Dīwī al-ʿashrī* (مختصر التصنيف في المكتبات ونظام ديوي العشري), Publications of the Ministry of Culture – Directorate of Cultural Centers, Damascus, 2011.

The cited publication is an abridgment of an Arabic work on Dewey Decimal Classification published by the Arab League Educational, Cultural and Scientific Organization (ALECSO). Dewey Decimal Classification is a registered trademark of OCLC. This project is independent and is not affiliated with or endorsed by OCLC.

## Language files

```
lang/
├─ index.json   # list of language files to load
├─ ar.json
└─ en.json
```

`lang/index.json` is a plain array: `["ar.json", "en.json"]`.

Each language file has this structure:

| Key | Description |
|---|---|
| `code` | Language code, e.g. `en`. Also used in `?lang=` and as the HTML `lang` attribute. |
| `name` | Native name shown in the language selector. |
| `dir` | Text direction: `"rtl"` or `"ltr"`. |
| `is_default` | `true` for the default language (set it on **one** file only). |
| `digits` | The ten digits for output, e.g. `"0123456789"` or `"٠١٢٣٤٥٦٧٨٩"`. |
| `fonts` | Font names offered in the font list. |
| `fonts_url` | Google Fonts stylesheet URL for those fonts (optional). |
| `font_fallback` | CSS fallback font stack written into the exported SVG. |
| `metrics.fit` | Average glyph width as a fraction of font size, used to shrink text to fit (≈ `0.35` Arabic, ≈ `0.55` Latin). |
| `metrics.wrap` | Width factor used to decide when titles wrap onto two lines. |
| `metrics.sub_wrap_below` | If a subclass title would need a font smaller than this size, it is split into two lines automatically (`0` disables it). |
| `center_text` | Default text in the center of the wheel. |
| `ui` | All interface strings (see `lang/en.json` for the full list of keys). |
| `default_data` | Sample data, one array item per line. |

Missing keys fall back to the default language.

### Adding a language

1. Copy `lang/en.json` to `lang/<code>.json` (e.g. `fr.json`).
2. Translate `name`, `ui`, `center_text` and `default_data`; set `dir`, `digits`, `fonts` and `metrics`. Keep `is_default` as `false`.
3. Add the file name to `lang/index.json`.
4. Reload the page, pick the language, and check the generated wheel. Adjust `metrics` if titles overflow.

See [CONTRIBUTING.md](CONTRIBUTING.md) for details.

## Credits

Idea and programming by **Abdurrhman Alsaeed** (عبد الرحمن بن ناصر السعيد), developed with the assistance of **Claude** (Anthropic).

## License

The project software is released under the [MIT License](LICENSE).

## Project structure

- `index.html` — the browser application.
- `lang/` — interface translations and sample data.
- `examples/data-text/` — source text data.
- `examples/svg/` — exported SVG examples.
- `examples/png-96dpi/` — PNG previews at 96 DPI.
