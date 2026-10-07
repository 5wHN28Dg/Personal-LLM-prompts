---
name: evidence-first-engineering
description: "Rules for evidence-first engineering in desktop, mobile and web apps: before adding a third-party dependency, framework or polyfill, replacing a platform-provided control with custom code, adding UI controls or features the platform may already provide (date pickers, dialogs, HTTP, storage), or choosing a stack, find out what the platform already provides and add only what it doesn't, keeping accessibility, security and measurement discipline. Not for bug fixes, refactors, or features built from existing project code."
---

# Evidence-first engineering

Condensed from two longer essays, [platform engineering policy](reference/platform-engineering-policy.md) and [web engineering policy](reference/web-engineering-policy.md). The essays carry the reasoning; this carries the rules. You don't need to read them to apply these rules; open one (if you can read files) only when a rule's reasoning is genuinely in question.

Before building or importing anything, find out what the target platform already provides, and add only what it doesn't. A mature platform is a library of solved problems; a good application orchestrates them instead of reimplementing them. Small size is not the goal: maintainability, tests, accessibility, localization and security still apply.

Apply this when adding a capability, adding a dependency, or replacing a platform feature. For a small feature, a one-line check of what the platform offers is enough. Bug fixes and changes that stay within existing choices skip the investigation procedure. The non-negotiables always apply.

## Which platform

- **Native desktop or mobile**: the platform is the vendor's supported stack for the declared target versions. Win32, WinUI 3 and the Windows App SDK; AppKit and SwiftUI; the Android framework, Jetpack and Compose; UIKit and SwiftUI. On Apple platforms SwiftUI vs AppKit/UIKit is a real choice: SwiftUI for short-to-medium lifespans and standard controls, AppKit or UIKit for long-lived or heavily custom UI; mixing them is fine. Linux has no single OS GUI layer, so name the stack explicitly (GTK or Qt, portals, D-Bus, systemd user units).
- **Apps that ship their own engine** (Electron, React Native) are native apps: they fall under the native rules, and the bundled engine is a cost to weigh. For routine work, the platform is that engine's APIs plus the OS features it exposes; raise a move to a native stack only when the task is about size or architecture, or I ask. UI rendered in a bundled web engine follows the web accessibility and escaping rules.
- **Scripts, CLIs and servers:** the platform is the language's standard library and the OS. **Game engines:** the engine's built-in features.
- **Web** (delivered over HTTP to a browser): the platform is standard HTML, CSS and Web APIs available in every browser the project claims to support, across all three engines (Blink, WebKit, Gecko), with a fallback where one is missing. Default to all three engines and treat WebKit as mandatory (most iOS users can only get WebKit). If the project declares a narrower set, follow it and note the iOS gap once. A Chrome-only feature is not a web feature.

## What counts as platform-provided

It must be vendor-supported for application development (web: standardized or on a standards track), work on every declared target version or browser, and not carry its own runtime that duplicates what the platform already guarantees. Vendor guidance churns: prefer guidance that has survived a platform generation and price in the risk of newer frameworks being replaced. A library the vendor names as its expected development model (Compose, SwiftUI) counts as platform. On the web, graceful degradation is a fallback; a polyfill is a dependency and needs the same justification as any other. Prefer the fallback; polyfill only when the degraded experience is unacceptable, and say why.

## Procedure, per feature and per target

1. What does the platform provide, directly or through optional components, and how reliably are those present?
2. What is genuinely missing?
3. What is the smallest custom code or dependency that closes the gap?
4. What is its full cost: size (on the web, paid on every visit), transitive dependency count, license, maintenance, security posture, and the cost of replacing it later?

Weigh the answers against the project's real constraints: team, number of targets, expected lifespan, amount of client state, SEO or server-rendering needs. Before choosing an architecture or stack, build a capability matrix per project from current sources (vendor docs, MDN, caniuse), not memory; keep it in your working notes and write it to a file only if asked. The architecture is an output of that investigation, not an input. When choosing a stack, if a constraint that would change the choice (targets, lifespan, team) isn't stated, ask; don't ask when I've already named the stack. For feature work, infer constraints from the repo.

On the web, prefer in this order, justifying each step by what the one below can't do: the browser, a small focused library, a framework, a meta-framework. For an app with meaningful client-side state, a framework is the expected endpoint; say so plainly. Safe-by-default escaping of user content is also a valid reason to take the framework step. Never mix two UI frameworks.

## Dependencies

Dependencies aren't guilty by default: a well-maintained library (SQLite, libcurl) often beats custom code. "Well-maintained" means recent releases, a findable security-response history, more than one active maintainer, a license compatible with distribution, and a track record across at least one major version. If those answers aren't clearly positive: write it yourself if the piece is small; otherwise name the risk and ask. If I asked for the dependency, pick the best candidate and state any criteria it misses; ask only when no candidate is acceptable.

## Non-negotiables

- **Accessibility is the first question when replacing a platform control.** Platform controls bring screen reader support, keyboard navigation, focus management and high contrast for free; a replacement loses them, even when the platform control is uglier. Raise that cost once; if a custom control is still wanted, prefer an established accessible component library over hand-rolled code. On the web use semantic elements (`<button>`, `<a>`, `<label>`, `<dialog>`, `<details>`, landmarks) and make sure it works keyboard-only, with a screen reader, at 200% zoom, in high contrast and with reduced motion.
- **Don't weaken or bypass platform security** to drop a dependency or simplify (CSP, same-origin policy, HTTPS, subresource integrity, sandboxing). Skipping a web framework means owning escaping: `textContent` by default, a maintained sanitizer when HTML must be inserted, and an audit of every place user data reaches markup, URLs or redirects.
- **An extension API makes you a platform.** Prefer a protocol or a sandboxed capability surface. If extensions run in-process against your internals, that is a one-way door: say so in the README.

## Measurement

Measure on the target, and set the regression rule before measuring.

- Native: installed size, startup time, steady-state memory, battery, on a clean device. No regression past the project's threshold without a written justification.
- Web: Core Web Vitals at the 75th percentile from real users (Google's current "good" thresholds unless the project sets its own), bundle size tracked in CI with any growth justified in the pull request, tested on a mid-range Android phone and run in CI against all three engines.

These are project standards, not steps for every change. Check what you can run yourself (keyboard flow, semantics, bundle size, tests) and list the manual checks you couldn't run; never claim a check you didn't do. For size or performance tasks, measure before and after locally and report; propose CI or real-user monitoring, but don't add it unless asked.

Orchestration-heavy code is harder to unit test: keep logic in pure modules and keep platform adapters thin, tested on the platform.

## Showing the work

When you add a dependency, framework or polyfill, or replace a platform feature with custom code, state in one or two lines what the platform offers, what's missing, and why this choice is the smallest total cost. Don't produce decision records unless asked.
