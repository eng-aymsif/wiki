<div align="center">
<h1>📚 Wiki — Frappe Wiki App (eng-aymsif Fork)</h1>
<p>
<strong>Wiki App built on the <a href="https://frappeframework.com">Frappe Framework</a></strong><br>
تطبيق ويكيا مبنياً على إطار عمل فرابي
</p>
</div>

---

**English** | [**العربية**](#تحليل-المشروع-بالعربية)

> This repository is a fork of the official [frappe/wiki](https://github.com/frappe/wiki) app
> with the following fork-specific enhancements:
> - **🌐 Full Arabic (RTL) support** — all UI strings are translatable, an Arabic
>   translation file (`ar.csv`) is bundled, and pages render with the correct
>   `lang` / `dir` attributes.
> - **🔒 `Allow Editing` toggle** — a new Wiki Setting that globally gates edit
>   permissions (hides edit controls, blocks save/preview endpoints, and keys
>   the sidebar cache by permission state).
>
> هذا الريبو هو Fork من تطبيق [frappe/wiki](https://github.com/frappe/wiki) الرسمي
> مع إضافات خاصة بهذا الـ Fork: دعم عربي كامل (RTL) ومفتاح «السماح بالتحرير».

---

## 📋 Project Analysis / تحليل المشروع

### 🎯 Purpose / الغرض

**English:** Wiki is a dynamic, text-heavy knowledge base and documentation app.
It lets teams publish pages on the fly, maintain full revision history, compare
changes, and control updates through an approval workflow.

**العربية:** «Wiki» تطبيق قاعدة معرفة ووثائق ديناميكي غني بالنصوص. يتيح للفرق
نشر الصفحات مباشرة، والاحتفاظ بسجل كامل للمراجعات، ومقارنة التغييرات، والتحكم
بالتحديثات عبر سير عمل للموافقات.

### 👥 Target Audience / الجمهور المستهدف

**English:** Documentation and knowledge-management teams running Frappe/ERPNext
sites — product documentation, internal wikis, help centers, and public docs.

**العربية:** فرق التوثيق وإدارة المعرفة التي تشغّل مواقع Frappe/ERPNext —
توثيق المنتجات، والويكي الداخلية، ومراكز المساعدة، والوثائق العامة.

### 🧩 Modules / الوحدات

| Module / الوحدة | Description / الوصف |
|---|---|
| **Wiki Page** | The core content entity with Markdown/rich-text authoring and revision history / الصفحة الأساسية للمحتوى مع سجل مراجعات |
| **Wiki Group** | Hierarchical grouping of pages in the sidebar / تجميع هرمي للصفحات في الشريط الجانبي |
| **Wiki Settings** | Global configuration — logo, scripts, spaces, and the new `allow_editing` toggle / الإعدادات العامة |
| **Revisions** | Change approval, diff comparison, and revision listing / الموافقات على التغييرات ومقارنتها |

### 🗃️ Core DocTypes / الكيانات الأساسية

- `Wiki Page` — content page with route, content, and sidebar placement
- `Wiki Group` — sidebar group / page hierarchy
- `Wiki Group Item` — membership of a page in a group
- `Wiki Page Revision` / `Wiki Page Revision Item` — revision and diff tracking
- `Wiki Settings` — single-doctype configuration

### 🛠️ Tech Stack / التقنيات

- **Backend:** Python, Frappe Framework
- **Frontend:** JavaScript, TipTap (rich-text editor), jQuery
- **Database:** MariaDB
- **Tooling:** Node.js, Yarn, Bench, Cypress (E2E)

### ✨ Key Features / الميزات الأساسية

1. Create Wiki Pages & author in Markdown or Rich Text
2. Unlimited sidebar hierarchy (Wiki Groups)
3. Full revision history with diff comparison & approval workflow
4. Attachments, Table of Contents, caching
5. Custom Script support via `Wiki Settings`
6. *Fork:* `Allow Editing` permission toggle
7. *Fork:* Arabic (RTL) translations
8. *Fork:* `Jinja Template` content type — translatable pages

### 🌐 Jinja Template Content Type / نوع المحتوى «قالب Jinja»

**English:** A Wiki Page can set **Content Type = `Jinja Template`** (Desk only).
Its content is then rendered server-side through the same sandboxed Jinja
environment used by Print Format's `html` field, enabling translatable strings:

```html
<td class="table-primary">{{ _("Ticket Number") }}</td>
```

- Available context: `doc` (the Wiki Page), plus Frappe safe globals (`frappe.utils.*`, `_()`, …)
- Translations resolve per-request language; page cache is stored per language automatically
- These pages are protected from the web editor (Edit button hidden, API updates blocked) — edit them from the Desk where the content field is a code editor (CodeMirror)
- Template syntax is validated on save (`validate_template`)

**العربية:** يمكن لصفحة الويكي اختيار **نوع المحتوى = `Jinja Template`** (من Desk فقط)،
فيُصيَّر محتواها من جهة الخادم عبر نفس بيئة Jinja المعزولة المستخدمة في حقل HTML
بدوكتيب Print Format، مما يتيح نصوصاً قابلة للترجمة مثل المثال أعلاه:

- المتاح داخل القالب: `doc` (صفحة الويكي) ووظائف frappe الآمنة (`frappe.utils.*`, `_()`)
- تُترجم النصوص حسب لغة الزائر، ويُخزَّن كاش الصفحة لكل لغة على حدة تلقائياً
- هذه الصفحات محمية من محرر الويب (يُخفى زر التعديل ويُحجب التحديث عبر API) — عدّلها من Desk حيث يكون حقل المحتوى محرر أكواد
- تُفحص صياغة القالب عند الحفظ

### 🔗 Integrations / الترابط

- Runs on **Frappe Framework** (integrated with **ERPNext** sites)
- Serves via **Frappe Website** renderer with custom route rules
- Manageable from **Frappe Desk** (Wiki Settings)

---

## 📦 Installation / التثبيت

```bash
# get app
bench get-app https://github.com/eng-aymsif/wiki

# install on site
bench --site sitename install-app wiki

# add Arabic translations (after install)
bench --site sitename set-config website_language ar
```

> Note: `main` branch does not support Frappe/ERPNext v13.

---

## 🧪 Validation / التحقق

```bash
bench build --app wiki     # frontend assets
yarn run test              # unit tests (if configured)
bench --site sitename console  # runtime sanity checks
```

---

## 🔗 Links / روابط

- Repository: <https://github.com/eng-aymsif/wiki>
- Releases: <https://github.com/eng-aymsif/wiki/releases>
- Upstream: <https://github.com/frappe/wiki>

---

## 📄 License / الترخيص

MIT — see [frappe/wiki](https://github.com/frappe/wiki/blob/main/license.txt).

---

## تحليل المشروع بالعربية

**الغرض:** تطبيق «Wiki» هو تطبيق قاعدة معرفة ووثائق ديناميكي مبنٍ على إطار عمل
فرابي، مصمم لخدمة المحتوى النصي الكثيف مثل التوثيق وقواعد المعرفة. يسمح بنشر
صفحات جديدة وتعديلات صغيرة دون توقف، مع سجل مراجعات كامل وآلية موافقات على
التغييرات.

**الجمهور المستهدف:** فرق التوثيق وإدارة المعرفة على مواقع Frappe/ERPNext
(توثيق المنتجات، الويكي الداخلية، مراكز المساعدة، الوثائق العامة).

**الوحدات الرئيسية:** Wiki Page (الصفحة ومحتواها)، Wiki Group (التجميع الهرمي)،
Wiki Settings (الإعدادات العامة)، Revisions (المراجعات والموافقات).

**الكيانات الأساسية (DocTypes):** Wiki Page، Wiki Group، Wiki Group Item،
Wiki Page Revision، Wiki Page Revision Item، Wiki Settings.

**التقنيات:** بايثون + Frappe Framework (Backend)، جافاسكربت + TipTap
(Frontend)، MariaDB (قاعدة البيانات)، Node.js/Yarn/Bench (أدوات التطوير).

**الميزات الأساسية:** إنشاء صفحات الويكي، الكتابة بـ Markdown أو نص منسّق،
تسلسل هرمي غير محدود في الشريط الجانبي، سجل مراجعات مع مقارنة الفروقات،
المرفقات، جدول المحتويات، التخزين المؤقت، ودعم السكربتات المخصصة.

**إضافات هذا الـ Fork:** مفتاح «السماح بالتحرير» (allow_editing) الذي يقفل
أزرار التحرير ونقطتي الحفظ والمعاينة عند تعطيله، ودعم ترجمة عربية كاملة مع
اتجاه RTL.