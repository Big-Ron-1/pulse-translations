# Pulse translations

Community translations for the **Pulse** head-unit app. Pulse loads these JSON
files **at runtime**, so a translation you contribute here reaches every user
**without an app update** — they just refresh the language list in
**Settings → Language**.

**English (`translations/en.json`) is the source of truth.** Every key that
exists in the app lives there. Any string not yet translated in another language
automatically falls back to English, so **partial translations are welcome** —
translate what you can.

## Repo layout

```
.
├── languages.json          # the list of languages shown in the app
├── translations/
│   ├── en.json             # source of truth (English) — do not translate
│   ├── es.json             # Spanish (starter example)
│   └── <code>.json         # your language
└── README.md
```

## How to add or improve a language

1. **Pick a language code** — e.g. `es` (Spanish), `fr` (French), `de` (German),
   `pt_BR` (Brazilian Portuguese), `ar` (Arabic).

2. **Create `translations/<code>.json`.** The easiest way is to copy
   `translations/en.json` and translate **only the values** — never change the
   keys:

   ```json
   {
     "common.cancel": "Cancelar",
     "settings.title": "Ajustes",
     "language.title": "Idioma"
   }
   ```

   You don't have to include every key. Missing keys fall back to English, so a
   file with 50 keys is a perfectly good start.

3. **Add it to `languages.json`** so it appears in the app's picker:

   ```json
   {
     "code": "es",
     "name": "Spanish",
     "nativeName": "Español",
     "file": "translations/es.json",
     "rtl": false
   }
   ```

   | Field        | Required | Meaning                                              |
   |--------------|----------|------------------------------------------------------|
   | `code`       | yes      | Language code (`en`, `es`, `pt_BR`, …)               |
   | `name`       | yes      | English name (shown as a subtitle)                   |
   | `nativeName` | yes      | The language's own name (the main label)             |
   | `file`       | yes      | Path to the JSON, relative to the repo root          |
   | `rtl`        | no       | `true` for right-to-left scripts (Arabic, Hebrew, …) |

4. **Open a pull request.** Once merged into `main`, the app picks it up the next
   time someone opens **Settings → Language** (tap the refresh icon to fetch the
   latest list immediately).

## Translation rules

- ✅ Translate **values only**. Keep keys byte-for-byte identical to `en.json`.
- ✅ Keep **`{placeholders}`** exactly as they appear (e.g. `"{v} km"`,
  `"{count} more"`). They're filled in with live values at runtime — translate
  the words around them, not the placeholder.
- ✅ Keep emoji and symbols that appear in the English value.
- ✅ Save as **UTF-8** (no BOM).
- ❌ Don't add, rename, remove, or reorder keys (order doesn't matter, but don't
  rename them).
- ❌ Don't translate `en.json`.

## Keeping a language up to date

When the app adds new strings, they land in `translations/en.json` here first.
To find what's missing in your language, compare its keys against `en.json` —
any key in `en.json` that's absent from your file is currently showing in
English. Add and translate it.

## Notes

- `es.json` is a **starter** with only the most common keys translated, to show
  the format and prove the pipeline works in-app. It needs the rest of the keys
  filled in — contributions welcome!
- Questions or a new language you're not sure how to wire up? Open an issue.
