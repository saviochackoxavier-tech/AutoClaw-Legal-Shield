# Privacy Policy — AutoClaw Legal Shield

**Effective date:** November 6, 2026

AutoClaw Legal Shield is a client-side demonstration application. This policy describes exactly what happens to information when you use it.

## 1. Data We Collect

**None.** The application runs entirely in your browser tab after the page loads. It makes no network requests: no servers are contacted, no analytics run, no fonts or scripts are fetched, and no telemetry of any kind is emitted. A Content-Security-Policy with `connect-src 'none'` blocks all outbound traffic at the browser level.

## 2. Data You Provide

- **Contracts** you upload, paste, or open from the sample library exist only in the memory of the tab (`JavaScript` objects). They are never transmitted, never written to disk by the app, and never persisted to browser storage. No cookies, `localStorage`, `sessionStorage`, IndexedDB, or service workers are used.
- Closing the tab (or using **Reset session**) permanently erases everything in the working session. There is no recovery copy because none exists.

## 3. Processing

- Clause analysis, risk scoring, redline drafting, fact extraction, and PII scrubbing are performed locally by regular expressions and deterministic rules running in your browser.
- The built-in **redaction bench** lets you strip names, organizations, financial figures, and trade-secret markers *before* running analysis. Redaction operates on a working copy inside the session.

## 4. Exports

- Redline memos (`.txt`) and fact timelines (`.csv`) are generated as local `Blob` downloads only when you click the export buttons. Nothing is uploaded in the process.

## 5. Third Parties

- None. The application contains no third-party code, fonts, images, or services.

## 6. Sample Documents

- The four sample agreements are illustrative templates written for this demo. They contain no real parties or personal data.

## 7. Changes

- Any future version that changes this posture must ship with an updated copy of this file in the repository.
