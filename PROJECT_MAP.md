# PROJECT MAP — eng-aymsif/wiki

## Repository / الريبو

- **Repository:** https://github.com/eng-aymsif/wiki
- **Visibility:** Private / خاص
- **Default branch:** `main`
- **Upstream:** https://github.com/frappe/wiki (remote `upstream`)
- **License:** MIT

## Releases / الإصدارات

| Version / الإصدار | Link / الرابط |
|---|---|
| [v1.0.0](https://github.com/eng-aymsif/wiki/releases/tag/v1.0.0) | Initial stable release of the fork — Allow Editing toggle + Arabic (RTL) translations / الإصدار المستقر الأولي للـ Fork |
| [v1.1.0](https://github.com/eng-aymsif/wiki/releases/tag/v1.1.0) | Jinja Template content type — translatable Wiki Page content via `{{ _("...") }}` (Print Format-style rendering) / نوع محتوى قالب Jinja للصفحات القابلة للترجمة |

## App Structure / بنية التطبيق

```
wiki/
├── wiki/
│   ├── api/                  # REST API endpoints
│   ├── wiki/
│   │   ├── doctype/
│   │   │   ├── wiki_page/    # core content entity + templates + renderer
│   │   │   ├── wiki_group/   # sidebar hierarchy
│   │   │   └── wiki_settings/# single-doctype config (allow_editing)
│   ├── public/js/            # editor, wiki, render_wiki client scripts
│   ├── translations/ar.csv   # Arabic (RTL) translations
│   ├── www/                  # drafts & contributions pages
│   ├── hooks.py              # app lifecycle / routes
│   └── patches.txt
├── README.md                 # bilingual project analysis
└── pyproject.toml
```

## Commit Conventions / اصطلاحات الـ Commits

- [Conventional Commits](https://www.conventionalcommits.org): `feat:`, `fix:`,
  `refactor:`, `docs:`, `style:`, `test:`, `chore:`
- Every commit body is bilingual (English + Arabic), referencing affected files
- كل رسالة Commit ثنائية اللغة (إنجليزي + عربي) مع روابط للملفات المتأثرة

## Maintenance Notes / ملاحظات الصيانة

- Sync with upstream: `git fetch upstream && git merge upstream/main`
- Bump version: follow [SemVer](https://semver.org) with annotated tags
- Validation: `bench build --app wiki` before tagging

## Jinja Template Mode / وضع قالب Jinja

- Wiki Page `content_type` field: `Markdown` (default) | `Jinja Template`
- Rendering: `get_jenv().from_string(content).render({"doc": self})` — same mechanism as Print Format `html` field (frappe/www/printview.py)
- Guards: web Edit button hidden (`content_editable`), `update()` API blocked, `update_page()` blocked, syntax validated on save
- Translations: add strings via Translation doctype or app CSVs; resolved per-request language; page cache is per-language (`cache_html`)