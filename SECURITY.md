# Security Policy — AutoClaw Legal Shield

AutoClaw Legal Shield is a single-file, client-side web application. Its security model is *isolation by architecture*: there is no server, no account, and no data channel to protect.

## 1. Isolation & Network Posture

- **Content-Security-Policy** (enforced via `<meta http-equiv>`):
  `default-src 'none'; style-src 'unsafe-inline'; script-src 'unsafe-inline'; img-src data:; font-src 'none'; connect-src 'none'; media-src 'none'; object-src 'none'; base-uri 'none'; form-action 'none'`
- `connect-src 'none'` blocks every outbound request at the browser level (verified: in-page `fetch()` to any origin is rejected).
- The only permitted resource is an inline `data:` SVG favicon. No CDN scripts, webfonts, analytics, or telemetry exist.
- `'unsafe-inline'` is required because the entire application is one self-contained HTML document; it cannot load anything external even if the code tried.

## 2. Cross-Site Scripting (XSS) Defenses

- Every dynamic string passes through a single escaping helper (`esc()`) before reaching an `innerHTML` sink; 37 escaping call sites cover all 42 sinks (remaining sinks are static markup or empty-string clears).
- Upload names, pasted text, clause excerpts, findings, redlines, timeline rows, scrub previews, error banners, and toasts are all rendered as text.
- Adversarial probe: a document named `<img src=x onerror=...><script>...` renders literally, injects zero DOM nodes, and fires no handlers.
- No inline `on*=` attributes exist in the markup; all behavior is delegated listeners in the one inline script.

## 3. Input Validation

| Guard | Behavior |
|---|---|
| Extension whitelist | Only `.pdf`, `.docx`, `.txt` are accepted; anything else is rejected before reading |
| Size cap | 10 MB per file, enforced before `FileReader` runs |
| Binary probe | Payloads starting `%PDF`/`PK` or containing control bytes are refused with a paste-instead recovery path |
| Empty file | Rejected with an explicit message |
| Analysis cap | Text beyond 200,000 characters is truncated for scanning, with a visible notice |

## 4. Export Safety

- CSV export doubles embedded quotes and prefixes cells beginning with `= + - @ <tab>` with `'` to neutralize spreadsheet formula injection.
- Downloads are user-initiated `Blob` objects; nothing is transmitted anywhere.

## 5. Data Retention

- All state lives in JavaScript memory for the life of the tab. There are no cookies, `localStorage`, `sessionStorage`, IndexedDB, or service workers. Closing the tab destroys everything.

## 6. Known Limitations

- PDF/DOCX binaries are not decoded in-browser; paste the text to run analysis (intentional demo scope).
- The clause playbook is a demonstration heuristic and must not be treated as legal review.
- CSP `img-src data:` and inline script/style are required by the single-file format.

## 7. Reporting

This is a demonstration project without a security team. Please open an issue in the repository describing the behavior, expected behavior, and reproduction steps. Do not include confidential contract text in reports.
