---

layout: col-sidebar
title: OWASP Penetration Testing Kit
tags: Penetration Testing Kit
level: 3
type: code
pitch: Open-source web application security testing from the live browser session, combining DAST, client-side SAST, in-browser IAST, SCA, and manual tools.

---

![OWASP Penetration Testing Kit logo](https://raw.githubusercontent.com/DenisPodgurskii/pentestkit/master/src/ptk/browser/assets/images/ptk_icon_small.png)

**Security testing where the browser is the source of truth.**

OWASP Penetration Testing Kit (PTK) is an open-source browser extension for testing web applications from the live browser session where they actually run.

PTK combines DAST, client-side SAST, in-browser IAST, SCA, traffic inspection, request replay, and JWT testing. It can test authenticated applications and single-page applications using the application state, traffic, and client-side code visible to the browser.

PTK provides its own extension interface. It does not use browser DevTools and does not require traffic to be routed through a separate desktop proxy for its normal testing workflows.

[Install for Chrome](https://chromewebstore.google.com/detail/owasp-penetration-testing/ojkchikaholjmcnefhjlbohackpeeknd) · [Install for Microsoft Edge](https://microsoftedge.microsoft.com/addons/detail/penetration-testing-kit/knjnghhnhcpcglfdjppffbpfndeebkdm) · [Install for Firefox](https://addons.mozilla.org/en-US/firefox/addon/owasp-penetration-testing-kit/) · [Open the browser-security playground](https://denispodgurskii.github.io/DOM-based-test-cases/)

[![OpenSSF Best Practices](https://www.bestpractices.dev/projects/11838/badge)](https://www.bestpractices.dev/projects/11838)

## Why browser context matters

Many security tools begin outside the application and must reconstruct authentication, navigation, and application state.

PTK starts from the browser session already being used by the tester. It can work with the authenticated user context, cookies, tokens, SPA routes, loaded JavaScript, DOM state, and browser-generated API traffic. This makes PTK particularly useful for testing authenticated workflows, single-page applications, and client-side behaviour.

## Core testing workflows

### Dynamic testing

Capture requests generated while using the application and run selected DAST attacks against specific requests, parameters, and request bodies. Findings include the request, payload, and evidence needed to review and reproduce the result.

### Client-side static analysis

Analyse JavaScript and HTML loaded by the browser for insecure patterns and client-side vulnerabilities. PTK can trace browser-controlled data from sources to dangerous sinks and report the relevant code and data flow.

### Runtime analysis

Instrument selected browser behaviour while the application executes. PTK can identify security-relevant DOM operations, navigation, browser messaging, and other client-side behaviour that only becomes visible at runtime.

### Component analysis

Identify client-side frameworks and libraries and report known vulnerable versions where matching vulnerability data is available.

### Manual testing

Inspect and replay browser traffic, modify requests, import or export cURL commands, analyse and test JWTs, manage cookies and browser storage, and review security headers, application technologies, and discovered routes.

### Automation and ZAP

OWASP PTK is the interactive extension for tester-driven security testing. **OWASP PTK Automation (PTK Auto)** is the separate browser runtime used by PTK Agent for automated tests, CLI workflows, CI/CD pipelines, and supported browser-testing platforms.

PTK automation supports browser workflows built with Playwright, Puppeteer, Selenium, and Cypress. PTK also integrates with OWASP ZAP so browser-side PTK analysis can be combined with broader ZAP testing.

[Read the automation and ZAP guide](https://github.com/DenisPodgurskii/pentestkit/blob/master/docs/guide/automation-and-zap.md) · [View the npm package](https://www.npmjs.com/package/pentestkit) · [Read the OWASP ZAP add-on documentation](https://www.zaproxy.org/docs/desktop/addons/owasp-ptk/)

## Where PTK fits

PTK complements full interception proxies, network scanners, and repository-level source-code analysis tools; it is not intended to replace all of them.

Its particular strength is testing what the browser can actually see and execute: authenticated workflows, browser-generated traffic, loaded client-side code, DOM behaviour, SPA navigation, and runtime application state.

## Quick start

1. Install PTK for Chrome, Microsoft Edge, or Firefox.
2. Open an application that you are authorised to test, preferably in a dedicated browser profile.
3. Sign in with a test account and navigate through the workflow you want to inspect.
4. Open PTK from the browser toolbar.
5. Inspect captured traffic or start a bounded DAST, SAST, IAST, or SCA scan.
6. Open a finding to review its evidence and reproduction details.

New users can begin with the public [browser-security playground](https://denispodgurskii.github.io/DOM-based-test-cases/), which contains deterministic test cases for client-side SAST, passive DAST, and IAST.

## Documentation

- [Pentester Guide](https://github.com/DenisPodgurskii/pentestkit/blob/master/docs/guide/README.md)
- [Automation and ZAP](https://github.com/DenisPodgurskii/pentestkit/blob/master/docs/guide/automation-and-zap.md)
- [PTK website and how-to guides](https://pentestkit.co.uk/howto.html)
- [Source code](https://github.com/DenisPodgurskii/pentestkit)
- [Browser-security playground](https://denispodgurskii.github.io/DOM-based-test-cases/)
- [YouTube channel](https://www.youtube.com/channel/UCbEcTounPkV1aitE1egXfqw)

## Contributing and support

Contributions, test cases, bug reports, and feature requests are welcome.

- [Report a bug or request a feature](https://github.com/DenisPodgurskii/pentestkit/issues)
- [Contribute to OWASP PTK](https://github.com/DenisPodgurskii/pentestkit)
- [Support OWASP PTK development](https://www.paypal.com/donate/?hosted_button_id=RNE87MVGX576E)

Sign in to GitHub before creating an issue. Do not include credentials, tokens, private application traffic, or undisclosed vulnerabilities in public issues.

## Responsible use

Use PTK only against systems where you have explicit authorisation. Active scanning, crawling, request modification, and token testing can generate load, modify application data, or trigger security monitoring. Confirm the permitted targets, test accounts, testing window, rate limits, and allowed test types before starting.
