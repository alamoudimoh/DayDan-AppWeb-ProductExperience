# Migration Decisions - Product Experience

This is an audit-only decision record for the Product Experience repository at `origin/main` commit `764b6fb`. It does not authorize remediation.

## Product/UI Identity

1. Current identity: `DayDan` appears in navigation, authentication, onboarding, settings, offline, toast, support, export, version, copyright, and error-report copy.
2. Intended Dydan identity: English `Dydan`; apply Arabic `دَيْدَن` only to approved Arabic product-label surfaces.
3. Classification: A - Safe Rename.
4. Rationale: These are local display strings or comments with no persistence or external consumer.
5. Compatibility impact: None.
6. Cross-repository dependencies: None found.
7. Required remediation: Change the listed UI and copy entries in PX-002, PX-005, PX-008 through PX-020, and PX-024, PX-026 through PX-030.
8. Verification required: Typecheck, build, and Playwright accessibility/flow checks. Product owner must approve bilingual label placement because `دَيْدَن` is currently absent.

## Browser Storage

1. Current identity: The runtime app has no `localStorage`, `sessionStorage`, IndexedDB, cookie, or cache API call. The unbundled `src/imports/DayDan-Color_Palette.html` stores `taskier-lang` and `taskier-surface`.
2. Intended Dydan identity: No runtime key change is currently needed. If the standalone artifact is regenerated and served, its keys would become `dydan-lang` and `dydan-surface`.
3. Classification: D - Intentionally Preserve for PX-101 through PX-104.
4. Rationale: The imported HTML is not referenced by any source import, build configuration, or runtime route.
5. Compatibility impact: No Product Experience user state exists. If the artifact becomes deployed, existing artifact users may have persisted `taskier-*` values.
6. Cross-repository dependencies: None found.
7. Required remediation: Do not rename the keys unless the artifact lifecycle is explicitly approved; then reclassify as C and implement a migrate-on-read or accepted reset strategy.
8. Verification required: Confirm bundle inclusion and production serving before changing any key.

## PWA/Manifest

1. Current identity: No web manifest, service worker, cache name, PWA metadata, icon asset, or push handler is tracked.
2. Intended Dydan identity: No change until those facilities are introduced.
3. Classification: No occurrence.
4. Rationale: No applicable identifier exists.
5. Compatibility impact: None.
6. Cross-repository dependencies: None found.
7. Required remediation: None.
8. Verification required: Re-audit when PWA support is added.

## Notification/Push

1. Current identity: Notification preferences and a bell UI are local component state only; no browser notification, push payload, notification channel, or identifier exists.
2. Intended Dydan identity: No technical identifier exists to rename.
3. Classification: No occurrence.
4. Rationale: No Web Notification or push API appears in tracked runtime code.
5. Compatibility impact: None.
6. Cross-repository dependencies: No Dydan Server or Dydan Mobile push contract is implemented.
7. Required remediation: None.
8. Verification required: Re-audit before implementing browser push or a mobile-shared channel.

## Server Contracts

1. Current identity: Authentication, sync, sessions, offline, export, and support are simulated in local state/static text. `ERROR_REPORT` is clipboard-only and its SyncEngine text is illustrative.
2. Intended Dydan identity: Rename the report heading as display copy only.
3. Classification: A - Safe Rename for PX-016 and PX-017.
4. Rationale: There is no `fetch`, API base URL, API header, environment value, request path, or Server import.
5. Compatibility impact: None in this repository.
6. Cross-repository dependencies: None found with Dydan Server.
7. Required remediation: Before a future report submission endpoint is wired, verify its accepted product labels and payload schema.
8. Verification required: Confirm no network implementation is introduced in the same remediation change.

## Mobile Contracts

1. Current identity: The responsive web prototype has no deep-link scheme, package ID, native bridge, mobile URL, or Mobile contract.
2. Intended Dydan identity: No change.
3. Classification: No occurrence.
4. Rationale: Browser viewport tests do not create a mobile integration contract.
5. Compatibility impact: None.
6. Cross-repository dependencies: None found with Dydan Mobile.
7. Required remediation: None.
8. Verification required: Re-audit if Capacitor/native/mobile linking is added.

## Environment, Package, Build, And Deployment

1. Current identity: `package.json` is the generic `figma-make-app`; `.figma/make` scripts deploy Figma artifacts. No legacy product identity appears in package metadata, environment variables, Docker/container files, deployment identifiers, GitHub workflows, domains, or analytics configuration.
2. Intended Dydan identity: No identity migration is presently required in these areas.
3. Classification: No occurrence.
4. Rationale: The configured Figma site metadata has no title, icon, Open Graph image, or analytics ID; Vite's optional analytics support has no configured value.
5. Compatibility impact: None.
6. Cross-repository dependencies: None found.
7. Required remediation: None; add the canonical identity only when the product owner provides official deployment metadata.
8. Verification required: Re-audit any new manifest, environment, deployment, or analytics configuration.

## Internal Theme Identifier

1. Current identity: `Theme = "daydan" | "sovereign"`, related conditionals, and one Playwright heading assertion use `daydan`.
2. Intended Dydan identity: `dydan` while retaining `sovereign`.
3. Classification: B - Technical Rename for PX-001, PX-003, PX-004, PX-006, PX-007, PX-021 through PX-023, PX-025, and PX-031.
4. Rationale: The identifier changes application behavior, but it is only in-memory React state and static tests.
5. Compatibility impact: No browser storage, route, API, or external consumer exists today.
6. Cross-repository dependencies: None found.
7. Required remediation: Rename the discriminant, all runtime comparisons, and the test assertion in one atomic change. Do not add a compatibility alias without evidence of persisted consumers.
8. Verification required: Typecheck and run `pnpm test:e2e`; grep for the old identifier excluding audit evidence.

## Testing/Visual Baselines

1. Current identity: `tests/closure.spec.ts` has one case-insensitive `daydan` text assertion. No snapshots, screenshots, visual-regression baseline, or fixture filename contains a legacy identity.
2. Intended Dydan identity: Update the assertion to `dydan` with the visible heading.
3. Classification: B - Technical Rename for PX-031.
4. Rationale: The assertion follows runtime display text.
5. Compatibility impact: None.
6. Cross-repository dependencies: None.
7. Required remediation: Update it only in the coordinated UI/theme remediation.
8. Verification required: Run the relevant Playwright project after the text change.

## Documentation And Historical Imports

1. Current identity: Historical Figma input files under `src/imports/` contain 87 content references and three legacy filenames. Their source material includes `DayDan`, `Taskier`, and the inherited Arabic form `تاسكير`.
2. Intended Dydan identity: Future regenerated design artifacts should use `Dydan` and `دَيْدَن`; historical provenance may retain legacy names.
3. Classification: D - Intentionally Preserve for PX-032 through PX-121.
4. Rationale: No tracked runtime module imports these assets. They record source/provenance rather than shipped product behavior.
5. Compatibility impact: None for the runtime application. The standalone palette's own localStorage keys need a fresh compatibility decision only if it is served.
6. Cross-repository dependencies: None found.
7. Required remediation: Product/design owner chooses whether to retain the inputs as historical evidence, regenerate them, or archive/remove them. Do not globally replace wording inside the historical source.
8. Verification required: Confirm an artifact's build/runtime inclusion before altering its internal IDs or storage keys.

## Legacy Compatibility

1. Current identity: `Taskier` and `تاسكير` occur only inside historical import material; no `Donetick` occurrence exists.
2. Intended Dydan identity: `Dydan` / `دَيْدَن` for future canonical material; preserve inherited names where they document source history.
3. Classification: D - Intentionally Preserve.
4. Rationale: The imports explicitly explain their inherited Taskier provenance and are not compatibility aliases in the product runtime.
5. Compatibility impact: None today.
6. Cross-repository dependencies: None found.
7. Required remediation: None until the artifact owner decides its lifecycle.
8. Verification required: If an inherited artifact is promoted into a deployed surface, repeat the contract audit before changes.

## Completion Condition

All 121 baseline occurrences are represented in `identity-inventory.csv`. No remediation was performed. The only unresolved non-occurrence is product/brand confirmation of where the canonical Arabic identity `دَيْدَن` must appear.
