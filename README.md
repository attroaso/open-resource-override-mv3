
# Open Resource Override (MV3)

A modern, Manifest V3–compatible **Resource Override** extension for Chrome.  
Redirect requests, mock responses (JSON/JS/CSS), modify response headers, inject JS/CSS, and control behavior per-rule with wildcards or regex — all with a clean, friendly UI.

> Created by **Annie Rosh** with **OpenAI**.

---

## ✨ Features

- **Redirect URL → URL** (classic replacement)
- **Mock response body** (JSON / JS / CSS / plain text)
  - **Immediate** mock (shows **307 Internal Redirect** + `data:` in DevTools)
  - **After response** mock (fetch/XHR only)
    - Option to **wait for the real network call** and then return your mock — keeps loaders/timing accurate
- **Modify response headers**
  - Add/override headers (e.g., `X-Debug: yes`)
  - **Expose to JS** option automatically adds `Access-Control-Expose-Headers` for the headers you set, so `fetch()`/XHR can read them across origins
- **Inject JavaScript / CSS** into matching pages
- **Per-rule enable/disable**, **priority**, **resource types**
- **Wildcard or regex** URL patterns, plus **exclusions**
- **Export/Import** rules
- Works under strict **CSP** pages (MAIN world injection for page hooks)

---

## 🚀 Install (Developer Mode)

1. Download the latest zip and extract the folder `open-resource-override-mv3`.
2. Open **`chrome://extensions`** → enable **Developer mode** (top-right).
3. Click **Load unpacked** → select the extracted `open-resource-override-mv3` folder.
4. Open **Details → Extension options** to configure rules.

> You can also drag the whole folder into `chrome://extensions`.

---

## 🧭 Usage Overview

### Rule Types

- **Redirect URL → URL**  
  Replace a URL with another URL. Good for swapping endpoints or static files.

- **Mock with text**  
  Return your own body (JSON/JS/CSS/plain).  
  - **Immediate**: uses Declarative Net Request to redirect to a `data:` URL → DevTools shows **307 Internal Redirect**.  
  - **After response (fetch/XHR only)**: page receives your mock, but DevTools still shows the real call.  
    - **Wait for real response**: first completes the real network (keeps loaders/timing), then delivers your mock to app code.

- **Modify response headers**  
  Add/override/remove response headers. For new headers to be readable from JS, enable **Expose to JS** (adds `Access-Control-Expose-Headers` automatically for the headers you set).

- **Inject JS / Inject CSS**  
  Injects content into matching pages.

### Patterns

- **Wildcard** (easiest):  
  `*/tenants/*/runtime/analytics/dashboards*`  
  Matches any tenant, with/without query.
- **Regex** (advanced): use full regular expressions.

You can also add **Exclusions** (comma-separated) that are applied as regex exclusions.

---

## 🔍 DevTools Behavior

- **Immediate mock** → shows **307 Internal Redirect** + a `data:` entry.
- **After response** mock → DevTools shows the **real** request; page receives your **mock**.
- Header modifications are visible in **Network → Response Headers**.  
  For JS to read custom headers on cross-origin responses, use **Expose to JS**.

---

## ⚠️ Notes & Limitations

- Some headers are **restricted** by Chrome and cannot be modified (e.g., certain hop‑by‑hop or security headers). Custom headers are fine.
- If a request is **redirected** (Immediate mock), header modifications for that same request won’t apply (DNR is single‑action).
- For **opaque `fetch`** responses (`mode: "no-cors"`), headers/body are not readable by JS regardless of exposure.
- JS/CSS injection is subject to page CSP, but the page hook (used for After-response mocks) runs in the **MAIN world** and is CSP‑safe.

---

## 🧰 Power Tips

- Use **Priority** to control which enabled rule wins when multiple match.
- Use **Resource Types** to target only `xmlhttprequest`/`fetch` (or include others).
- The **Prettify** button formats JSON/JS/CSS bodies for readability.
- Export your rules as a JSON file and share them with your team.

---

## 🙌 Credits

Created by **Annie Rosh** with **OpenAI**.  
Built as a modern successor to the classic “Resource Override” idea for today’s MV3 world.

