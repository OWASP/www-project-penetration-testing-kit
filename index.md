---

layout: col-sidebar
title: OWASP Penetration Testing Kit
tags: Penetration Testing Kit
level: 3
type: code
pitch: Open-source web application security testing from the live browser session, combining DAST, client-side SAST, in-browser IAST, SCA, manual tools, and browser automation.

---

![OWASP Penetration Testing Kit logo](https://raw.githubusercontent.com/DenisPodgurskii/pentestkit/master/src/ptk/browser/assets/images/ptk_icon_small.png)

**Security testing where the browser is the source of truth.**

OWASP Penetration Testing Kit (PTK) is an open-source browser extension for testing web applications from the live browser session where they actually run.

PTK combines DAST, client-side SAST, in-browser IAST, SCA, traffic inspection, request replay, and JWT testing. It can test authenticated applications and single-page applications using the application state, traffic, and client-side code visible to the browser.

PTK provides its own extension interface. It does not use browser DevTools and does not require traffic to be routed through a separate desktop proxy for its normal testing workflows.

[Install for Chrome](https://chromewebstore.google.com/detail/owasp-penetration-testing/ojkchikaholjmcnefhjlbohackpeeknd) · [Install for Microsoft Edge](https://microsoftedge.microsoft.com/addons/detail/penetration-testing-kit/knjnghhnhcpcglfdjppffbpfndeebkdm) · [Install for Firefox](https://addons.mozilla.org/en-US/firefox/addon/owasp-penetration-testing-kit/) · [Open the browser-security playground](https://denispodgurskii.github.io/DOM-based-test-cases/)

[![OpenSSF Best Practices](https://www.bestpractices.dev/projects/11838/badge)](https://www.bestpractices.dev/projects/11838)

## PTK components

| Component | Use | Get started |
| --- | --- | --- |
| **OWASP PTK** | Interactive browser security testing, manual tools, and tester-controlled scans. | [Chrome](https://chromewebstore.google.com/detail/owasp-penetration-testing/ojkchikaholjmcnefhjlbohackpeeknd) · [Edge](https://microsoftedge.microsoft.com/addons/detail/penetration-testing-kit/knjnghhnhcpcglfdjppffbpfndeebkdm) · [Firefox](https://addons.mozilla.org/en-US/firefox/addon/owasp-penetration-testing-kit/) |
| **PTK Auto** | Restricted browser-side security runtime controlled by an authorised automation session. | [Chrome](https://chromewebstore.google.com/detail/owasp-penetration-testing/aiebcfjmdihgeeigbbcdpbpehikbdcgk) · [Edge](https://microsoftedge.microsoft.com/addons/detail/owasp-penetration-testing/jpppfkdhfjdkljeakammiplbdacnpdjg) · [Firefox](https://addons.mozilla.org/en-US/firefox/addon/owasp-pentestingkit-automation/) |
| **PTK Agent** | The `pentestkit` npm package, CLI, browser-framework integrations, cloud-browser providers, and PTK Auto orchestration. | [npm](https://www.npmjs.com/package/pentestkit) · [Documentation and source](https://github.com/ptklabs/ptk-agent) |
| **PTK Action** | GitHub Actions security scans with PTK findings, normal scan artifacts, severity gates, and SARIF for GitHub Code Scanning. | [GitHub Marketplace](https://github.com/marketplace/actions/owasp-ptk-security-scan) · [Documentation and source](https://github.com/ptklabs/ptk-action) |
| **OWASP ZAP integration** | ZAP-managed browser sessions with PTK browser-side findings imported into the ZAP alert model. | [ZAP add-on documentation](https://www.zaproxy.org/docs/desktop/addons/owasp-ptk/) |

PTK Auto is not the interactive PTK extension and does not provide the complete manual testing interface. Most local PTK Agent users do not need to install PTK Auto separately: the `pentestkit` package includes the browser-specific automation artifacts and prepares them for supported workflows. Store installations are useful for dedicated automation profiles and environments that require a signed extension. Use a dedicated test profile rather than a personal browsing profile.

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

PTK Agent supports Playwright, Puppeteer, Selenium, and Cypress, together with supported cloud-browser providers. PTK also integrates with ZAP so browser-side PTK analysis can be combined with broader ZAP testing.

[Read the PTK Agent documentation](https://github.com/ptklabs/ptk-agent/blob/main/docs/npm/README.md) · [View the npm package](https://www.npmjs.com/package/pentestkit) · [Open PTK Action in GitHub Marketplace](https://github.com/marketplace/actions/owasp-ptk-security-scan) · [Read the ZAP add-on documentation](https://www.zaproxy.org/docs/desktop/addons/owasp-ptk/)

## Interactive quick start

1. Install PTK for Chrome, Microsoft Edge, or Firefox.
2. Open an application that you are authorised to test, preferably in a dedicated browser profile.
3. Sign in with a test account and navigate through the workflow you want to inspect.
4. Open PTK from the browser toolbar.
5. Inspect captured traffic or start a bounded DAST, SAST, IAST, or SCA scan.
6. Open a finding to review its evidence and reproduction details.

New users can begin with the public [browser-security playground](https://denispodgurskii.github.io/DOM-based-test-cases/), which contains deterministic test cases for client-side SAST, passive DAST, and IAST.

## Automate with PTK Agent

Install the `pentestkit` npm package and the Chromium browser used by the default scanner:

```bash
npm install -D pentestkit
npx playwright install chromium
npx ptk-agent --doctor-extension
```

Run a scan against an application you are authorised to test:

```bash
npx ptk-scan https://your-authorised-target.example \
  --engine DAST,IAST,SAST,SCA \
  --require-ptk-bridge \
  --require-ptk-findings-export \
  --wait-for-ptk-complete
```

PTK Agent can also wrap existing Playwright, Puppeteer, Selenium, and Cypress journeys so security checks use the same authenticated browser workflow as the test. Provider helpers are available for supported Browserbase, Browserless, BrowserStack, Hyperbrowser, Steel, and TestMu workflows. Check the [provider support matrix](https://github.com/ptklabs/ptk-agent/blob/main/docs/npm/provider-browser-matrix.md) before selecting a framework and provider combination.

## Run PTK in GitHub Actions

[OWASP PTK Security Scan](https://github.com/marketplace/actions/owasp-ptk-security-scan) runs PTK Agent and PTK Auto in a GitHub-hosted Linux Chromium session. It can export normal PTK artifacts and GitHub Code Scanning-compatible SARIF, and it can fail a workflow when findings meet a configured severity.

Start the application in the workflow before running the PTK step:

```yaml
- name: Run OWASP PTK
  id: ptk
  uses: ptklabs/ptk-action@v1
  with:
    target: http://127.0.0.1:3000
    engines: DAST,IAST,SAST,SCA
    fail-on: high
```

See the [PTK Action documentation](https://github.com/ptklabs/ptk-action) for application startup, authentication, SARIF upload, artifact retention, permissions, and complete workflow examples.

## Use PTK with OWASP ZAP

The OWASP PTK add-on lets ZAP launch supported browsers with PTK, coordinate the browser scan lifecycle, and import PTK findings into the ZAP alert model. Use the PTK active scan rule in current ZAP automation plans and enable the PTK rules required by the scan policy.

[Read the OWASP PTK add-on documentation](https://www.zaproxy.org/docs/desktop/addons/owasp-ptk/) · [Read the automation and ZAP guide](https://github.com/DenisPodgurskii/pentestkit/blob/master/docs/guide/automation-and-zap.md)

## Where PTK fits

PTK complements full interception proxies, network scanners, and repository-level source-code analysis tools; it is not intended to replace all of them.

Its particular strength is testing what the browser can actually see and execute: authenticated workflows, browser-generated traffic, loaded client-side code, DOM behaviour, SPA navigation, and runtime application state.

## Documentation

- [Pentester Guide](https://github.com/DenisPodgurskii/pentestkit/blob/master/docs/guide/README.md)
- [PTK Agent and npm documentation](https://github.com/ptklabs/ptk-agent/blob/main/docs/npm/README.md)
- [PTK Agent CLI reference](https://github.com/ptklabs/ptk-agent/blob/main/docs/npm/cli.md)
- [Browser-framework integrations](https://github.com/ptklabs/ptk-agent/blob/main/docs/npm/frameworks.md)
- [Cloud-browser providers](https://github.com/ptklabs/ptk-agent/blob/main/docs/npm/providers.md)
- [GitHub Actions](https://github.com/marketplace/actions/owasp-ptk-security-scan)
- [Automation and ZAP](https://github.com/DenisPodgurskii/pentestkit/blob/master/docs/guide/automation-and-zap.md)
- [PTK website and how-to guides](https://pentestkit.co.uk/howto.html)
- [Browser-security playground](https://denispodgurskii.github.io/DOM-based-test-cases/)
- [YouTube channel](https://www.youtube.com/channel/UCbEcTounPkV1aitE1egXfqw)

## Contributing and support

Contributions, test cases, bug reports, and feature requests are welcome.

- [OWASP PTK extension source and issues](https://github.com/DenisPodgurskii/pentestkit)
- [PTK Agent source and issues](https://github.com/ptklabs/ptk-agent)
- [PTK Action source and issues](https://github.com/ptklabs/ptk-action)
- [Support OWASP PTK development](https://www.paypal.com/donate/?hosted_button_id=RNE87MVGX576E)

Sign in to GitHub before creating an issue. Do not include credentials, tokens, private application traffic, or undisclosed vulnerabilities in public issues. Report security vulnerabilities privately through the relevant repository's security-advisory channel.

## Responsible use

Use PTK only against systems where you have explicit authorisation. Active scanning, crawling, request modification, and token testing can generate load, modify application data, or trigger security monitoring. Confirm the permitted targets, test accounts, testing window, rate limits, and allowed test types before starting.
