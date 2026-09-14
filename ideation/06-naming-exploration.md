# Naming exploration — round 1

Date: 2026-09-14. Status: candidates for discussion; no replacement name selected.

## Revised brief

The owner rejected the descriptive working name. Aim for the personality and brevity of Django, Flask, Gin, or Ninja: one memorable word, easy to say, easy to type, and comfortable in a README or command line. The brand should survive a change in implementation language or product layer.

Prefer 4–6 letters and one or two syllables. Avoid forced acronyms and suffixes such as NetworkRuntime. Meanings below describe our intended associations, not invented etymologies.

## Creative shortlist

| Name | Suggested pronunciation | Character | Example |
| --- | --- | --- | --- |
| **Kipra** | KIP-rah / 키프라 | Quick, playful, distinctive; strongest overall candidate in this round | “Built with Kipra.” |
| **Varko** | VAR-koh / 바르코 | Solid, mechanical, suited to infrastructure | “Varko handles the traffic.” |
| **Brim** | BRIM / 브림 | Compact English word; capacity and an edge give it a useful visual identity | “Start a Brim server.” |
| **Riff** | RIF / 리프 | Expressive and developer-friendly; room for a musical identity | “Build your next service with Riff.” |
| **Fenn** | FEN / 펜 | Quiet, minimal, approachable | “Fenn makes serving simple.” |

Recommendation: discuss **Kipra** first; **Varko** if we want a heavier systems identity; **Riff** if personality matters most. These are aesthetic judgments, not availability rankings.

## Initial collision screening

Limited web searches on 2026-09-14; no name is established as available. Package registries depend on the language we eventually choose. Domains and comprehensive name clearance have not been checked.

- **Kipra:** an existing [Kipra keyboard project](https://github.com/focusaurus/kipra-keyboard) appeared. Different category, but not a globally unique word.
- **Varko:** [Varko AI](https://varko.ai/) already uses the name for business automation. Existing software-adjacent use weakens distinctiveness.
- **Brim, Riff, Fenn:** creative candidates only; targeted collision checks still pending.
- **Tavo:** remove from the shortlist because [Tavo.js](https://tavojs.dev/docs/cli/) already uses it for a framework and CLI.
- **Kova:** lower priority because a [Kotlin validation library](https://github.com/komapper/kova) already uses it.
- **Rovik:** lower priority because [Rovik Systems](https://roviksystems.com/) uses it for software products.
- **Rokka:** lower priority because an existing [npm package](https://www.npmjs.com/package/rokka) uses it.

## Brand test

Illustrative only: `kipra serve`, “Kipra documentation”, “Kipra 0.1”, `kipra-core`. No CLI, package, or release exists yet.

Read each finalist aloud, ask someone to spell it after hearing it, and check whether its search results can plausibly become recognizable. Select the name before changing repository URLs and local directories.

## Rename scope after selection

Rename the GitHub repository, local project directory, root README title, current-name references, and remote URL. Preserve previous names only where they explain decision history. Verify pushes and document links afterward. No packages or application identifiers exist to migrate.
