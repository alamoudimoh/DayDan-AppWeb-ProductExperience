# Dydan Identity Audit - Product Experience

## Scope

- Repository: `alamoudimoh/DayDan-AppWeb-ProductExperience`
- Branch: `audit/dydan-identity-product-experience`
- Baseline: `origin/main` at `764b6fb` (`revert: restore clean product experience baseline after Figma sync`)
- Audit date: 2026-09-15
- Method: tracked-file inventory using `git ls-files` and exact searches for `DayDan`, `Daydan`, `daydan`, `DAYDAN`, `Taskier`, `taskier`, `TASKIER`, `Donetick`, `donetick`, `DONETICK`, plus Arabic derived forms.

## Results

| Metric | Count |
|---|---:|
| Tracked files scanned | 53 |
| Legacy content occurrences | 118 |
| Legacy path occurrences | 3 |
| Total audited occurrences | 121 |
| Affected tracked source files | 13 |
| Canonical English occurrences (`Dydan`) | 0 |
| Canonical Arabic occurrences (`دَيْدَن`) | 0 |

### Files Containing Legacy Identity

- `src/App.tsx`
- `src/data.ts`
- `src/imports/DayDan-Brand-Summary.md`
- `src/imports/DayDan-Color_Palette.html`
- `src/imports/Sovereign-Brand-Summary.md`
- `src/imports/pasted_text/daydan-product-brief.md`
- `src/index.css`
- `src/screens/AuthScreen.tsx`
- `src/screens/ErrorScreen.tsx`
- `src/screens/OnboardingScreen.tsx`
- `src/screens/SettingsScreen.tsx`
- `src/screens/SharedStatesScreens.tsx`
- `tests/closure.spec.ts`

### Classification Counts

| Classification | Count | Meaning |
|---|---:|---|
| A - Safe Rename | 21 | User-visible copy and comments in the prototype runtime. |
| B - Technical Rename | 10 | In-memory theme discriminant and one assertion that must change together. |
| C - Compatibility Required | 0 | No shipped persisted or external identifier found. |
| D - Intentionally Preserve | 90 | Historical imported design inputs, including their legacy paths. |
| E - Remove | 0 | No identity-only runtime artifact was proven dead enough to remove without owner direction. |
| F - Investigate | 0 | No legacy occurrence requires external verification; see the non-occurrence Arabic identity decision below. |

## Highest-Risk Items

1. `daydan` is the in-memory `Theme` discriminant in `src/App.tsx` and `src/screens/SettingsScreen.tsx`. It is not persisted in this prototype, but all producer, consumer, and test references must change atomically.
2. `src/imports/DayDan-Color_Palette.html` is an unbundled, standalone historical source file with `taskier-lang` and `taskier-surface` localStorage keys. It is not imported by runtime code. Do not rename those keys unless the asset is deliberately revived or shipped; then reclassify them as C and define migration behavior.
3. The error-report sample is local-only and copied to the clipboard; no reporting endpoint or parser is implemented. Treat its product label as a display rename, but confirm any future support ingestion contract before turning it into a network payload.

## Cross-Repository Dependencies

No implemented cross-repository contract was found. This prototype has no API client, API headers, environment identity value, browser storage, cookies, manifest/PWA metadata, service worker, cache name, push handler, deep link, route path, analytics identifier, package identity, Docker/deployment identity, or visual-baseline identity.

The app only models authentication, sessions, notifications, sync, and offline behavior in local React state or static copy. Those simulations are not contracts with Dydan Server, Dydan AppWeb, or Dydan Mobile.

## Unresolved Item

No product label currently renders the canonical Arabic identity `دَيْدَن`; the UI only exposes the generic language label `العربية`. Product/brand ownership must decide which bilingual shell surfaces require the Arabic product name before remediation. This is an audit decision, not a legacy occurrence, so it is not included in the occurrence totals above.

## Recommended Remediation Sequence

1. Obtain product/brand approval for English `Dydan`, Arabic `دَيْدَن`, and the intended bilingual display surfaces.
2. Rename runtime display text, accessibility-facing text, comments, and the error-report sample to the approved canonical identity.
3. Rename the in-memory `daydan` theme discriminant to `dydan` in one coordinated change with its Playwright assertion; verify no persistence was introduced before landing it.
4. Preserve imported source material as historical evidence or regenerate/archive it under owner direction. If any import becomes served content, assess `taskier-lang` and `taskier-surface` as persisted-browser compatibility keys first.
5. Rerun the tracked-file searches excluding this audit directory, then typecheck, build, and run the relevant Playwright coverage.

## Audit-Only Confirmation

No runtime code, test, build, deployment, route, package, environment, or asset was remediated. This branch adds only the audit artifacts in this directory.

## Reproduction

```bash
git ls-files -z -- ':!Dydan-Correction/**' | xargs -0 rg -n -I -e 'DayDan|Daydan|daydan|DAYDAN|Taskier|taskier|TASKIER|Donetick|donetick|DONETICK|تاسكير|دونتيك|ديدان|دايدان|داي[[:space:]-]*دان|دي[[:space:]-]*دان|ديدن'
```
