# TODO — Review Findings and Implementation Backlog

**Document status:** Controlled open backlog; no finding is closed by this revision.  
**Review date:** 2026-07-19  
**Backlog revision:** 2.1 (acceptance and dependency refinement)  
**Reviewed code revision:** `d68e78c`  
**Scope:** `index.html`, `main.js`, `package.json`, README/review documentation, repository contents, and Chromium browser runtime behavior.  
**Review environment:** Node.js 22.16.0 and Chromium 144.0.7559.96.  
**Finding count:** **49 open** — P0: 1, P1: 18, P2: 20, P3: 10.  
**Baseline rule:** File/line references and reproduced measurements apply to `d68e78c`; re-baseline them after code movement.

## Revision history

| Revision | Date | Controlled change |
|---|---|---|
| **2.1** | 2026-07-19 | Made the `iterations` similarity step branch-explicit, added numerical acceptance for `MATH-002`, quantified enabled-grid verification, strengthened render/security failure tests, replaced sequencing bullets with an implementation dependency matrix, and clarified demo/runtime validation criteria. |
| **2.0** | 2026-07-19 | Converted the flat review list into a controlled backlog with assumptions, decision records, finding classifications, root-cause workstreams, per-finding dependencies, evidence-retention requirements, limitations, and a phased execution plan. |

## Backlog control rules

Priority expresses remediation urgency, not implementation order. Classification metadata separates consequence, finding type, release-gate status, confidence, root-cause workstream, ownership, and target milestone.

A finding may be closed only when:

1. its disposition is approved: fixed, removed, accepted risk, or intentionally deferred;
2. the implementation is linked to the finding ID and has a defined rollback path;
3. a failing regression test or approved characterization baseline exists before the correction where practical;
4. acceptance criteria pass against the implementing revision;
5. verification evidence is retained under the **Evidence-retention requirements** in this document;
6. affected documentation, presets, diagnostics, and release artifacts are updated; and
7. the owner and independent verifier record completion.

Allowed status values are **Open**, **Decision pending**, **In progress**, **Fixed—verification pending**, **Closed**, **Accepted risk**, and **Deferred**. “Accepted risk” requires an owner, rationale, expiry/review date, and compensating controls.

## Assumptions and decision gates

These assumptions drive priority and release-gate classifications. The project owner must approve or revise them before implementation planning.

| ID | Provisional assumption | Effect if rejected |
|---|---|---|
| A1 | Mathematical fidelity and the equations presented in the UI/README are product requirements. | Several math, sampling, grid, and documentation findings may become documented limitations rather than release gates. |
| A2 | Public source, npm, and/or packaged desktop distribution is intended. | Licensing, packaging, signing, metadata, and repository-content gates may be reduced or removed for private use. |
| A3 | Standalone modern-browser use remains a supported product claim. | Responsive-layout and cross-browser requirements can be narrowed to the Electron runtime. |
| A4 | User-selected images are untrusted inputs. | File limits, format policy, navigation restrictions, and hostile-input testing remain mandatory for public use. |
| A5 | WCAG 2.2 Level AA is the accessibility target. | A different approved standard must replace it; accessibility cannot remain undefined. |
| A6 | Electron 28 is the intended baseline because it is declared by the reviewed package. | Runtime, security, and packaging tests must be re-baselined to the approved Electron version. |

## Required decision records

These decisions must be approved before dependent implementation. A decision may select an implementation path or intentionally narrow product scope, but it must update affected priorities, release gates, tests, and documentation.

| Decision | Required disposition | Principal findings | Accountable roles |
|---|---|---|---|
| D-001 | Source period, `iterations`/frequency semantics, and adjacent output-plane similarity reporting. | MATH-002, MATH-004, GRID-001, DOC-002 | Product + math/rendering |
| D-002 | Literal `r2` radius versus view-scale/extent semantics. | MATH-003, GRID-001, DOC-002 | Product + math/rendering |
| D-003 | Cartesian output shapes and out-of-domain boundary modes/default. | MODE-001, MODE-002 | Product + math/rendering |
| D-004 | Source-alpha preservation versus background compositing. | IMG-001, SAMPLE-001 | Product + rendering |
| D-005 | Grid availability and representation for folded, multi-valued, or non-invertible maps. | GRID-001, GRID-002 | Math/rendering |
| D-006 | Supported Electron/browser viewport matrix and platform-specific save-completion semantics. | UI-001, UI-003, SAVE-001, REL-002 | Product + platform |
| D-007 | Accessibility target and assistive-technology/platform verification matrix. | A11Y-001 | Product + quality |
| D-008 | Upload byte/pixel/memory limits and supported image formats, including SVG/animation policy. | FILE-001, FILE-003, SEC-001 | Product + security/platform |
| D-009 | Complete-snapshot versus documented-partial preset behavior. | STATE-001, STATE-003 | Product + frontend |
| D-010 | Independent semantics for content rotation and branch-cut position. | MATH-001 | Product + math/rendering |

## Priority and finding-type definitions

| Priority | Definition | Default target |
|---|---|---|
| **P0** | Public redistribution or production-release blocker. | Before any affected distribution. |
| **P1** | High-consequence defect, mandatory release control, or prerequisite for safe remediation. | Next production release or earlier stated gate. |
| **P2** | Material secondary defect, design debt, control gap, or foreseeable failure mode. | Next planned minor release or stated decision point. |
| **P3** | Low-consequence cleanup, diagnostics, metadata, or optional usability improvement. | Managed backlog. |

Finding types include **defect**, **risk**, **decision/specification gap**, **control gap**, **release task**, **architecture debt**, **documentation defect**, and **enhancement**. Type does not determine priority by itself.

## Root-cause workstreams

The findings should be implemented as six coordinated workstreams rather than 49 independent patches. Existing finding IDs remain the traceability keys.

| Workstream | Root cause and scope | Principal findings | Exit criterion |
|---|---|---|---|
| **WS1 — Canonical state, layout, and accessibility** | UI state is split across DOM values, CSS classes, duplicated defaults, and unvalidated assignments. | `UI-001`–`UI-005`, `STATE-001`–`STATE-003`, `SLIDER-001`, `A11Y-001` | One validated state model drives controls, derived text, classes, ARIA, reset, presets, and responsive layout. |
| **WS2 — Sampling and coordinate-domain policy** | One sampler and wrap policy are used for incompatible periodic, mirrored, Cartesian, shape, and alpha domains. | `SAMPLE-001`, `SAMPLE-002`, `DEMO-001`, `MODE-001`, `MODE-002`, `IMG-001` | Boundary modes are explicit, independently tested, and selected by transform/domain semantics. |
| **WS3 — Authoritative mathematical model and diagnostics** | Transform semantics, branch choices, grid inversion, displayed invariants, and documentation are independently derived. | `MATH-001`–`MATH-006`, `GRID-001`, `GRID-002`, `DOC-002` | One approved derivation produces renderer parameters, grid behavior, diagnostics, labels, and documentation. |
| **WS4 — Transactional load/render/save lifecycle** | Asynchronous operations lack durable job identity, cancellation, lifecycle state, and platform-accurate completion reporting. | `FILE-001`–`FILE-003`, `RENDER-001`–`RENDER-003`, `SAVE-001`, `UX-002`, `WORKER-001` | Load and render IDs, cancellation, state transitions, resource cleanup, and save gating are deterministic and tested. |
| **WS5 — Shared implementation and measured performance** | Page/worker algorithms are duplicated and hot paths allocate or recompute unnecessarily. | `ARCH-001`, `PERF-001`, `PERF-002`, `CODE-001`, `CODE-002` | Production code has one tested algorithm source; optimizations are benchmarked after correctness is locked. |
| **WS6 — Quality, security, configuration, and release governance** | Evidence, dependency, content, security, packaging, and change controls are incomplete. | `REL-001`, `REL-002`, `QA-001`, `BUILD-001`, `SEC-001`, `DOC-001`, `REPO-001`, `REPO-002`, `PKG-001`, `UX-001` | A reproducible, auditable, security-reviewed release process packages only approved content and retains verification records. |

## Dependency and sequencing rules

Priority does not define implementation order. The following dependencies are mandatory unless an approved decision record changes them.

| Prerequisite / gate | Dependent findings or work | Blocking condition |
|---|---|---|
| Assumptions `A1`-`A6` and decisions in `MATH-002`, `MATH-003`, `MODE-002`, `IMG-001`, and `GRID-001` | Mathematical, sampling, grid, documentation, and release claims | Do not implement a behavior whose product semantics remain undecided. |
| `BUILD-001`, `QA-001`, and the evidence-retention requirements | Every remediation merge | A clean checkout must be reproducible; the next defect must have a failing test/characterization and retained evidence before correction. |
| `UI-004` and `UI-005` | `STATE-001`-`STATE-003`, `SLIDER-001`, shape-state accessibility, and preset/reset work | Canonical schema and state ownership must exist before repairing individual state symptoms. |
| `RENDER-001` -> `RENDER-002` | `SAVE-001`, `RENDER-003`, `UX-002`, and persistent-worker work in `PERF-002` | Job identity and lifecycle states must be authoritative before save, cancel, coalescing, or worker reuse. |
| `ARCH-001` characterization baseline | `SAMPLE-001`, `SAMPLE-002`, `MATH-004`, `PERF-001`, `PERF-002`, `CODE-001` | Extract only after tests identify the exact production implementation and approved current behavior. |
| `SAMPLE-001`, `SAMPLE-002`, `MATH-001`-`MATH-004`, and output-domain decisions | `GRID-001`, `GRID-002`, `DEMO-001`, and `DOC-002` | Grid and documentation must be derived from corrected mapping and boundary semantics, not patched independently. |
| `REL-001`, `REPO-001`, `PKG-001`, `SEC-001`, and `BUILD-001` | `REL-002` and any public artifact | No public artifact may ship until content, package, security, and reproducibility gates are dispositioned. |

Critical path: **decision approval -> reproducible build/evidence -> canonical state and lifecycle -> shared mathematical/sampling core -> grid/UI/accessibility -> documentation/release -> optimization**.

- Legal/provenance work may proceed in parallel, but `REL-001` blocks public redistribution.
- Performance work begins only after correctness and golden baselines are approved.
- Every dependent finding must link its prerequisite finding or decision record in the implementation issue/commit.

---

## Evidence-retention requirements

The review recorded pixel hashes, seam differences, viewport measurements, and runtime observations, but those records are not yet reproducible from repository-controlled procedures. Retain automated tests in the normal test tree and use a review evidence area for one-time/manual evidence that does not belong in CI.

```text
review/
├── README.md
├── decisions/
├── fixtures/
├── scripts/
├── results/
└── screenshots/
```

For each retained result, record the finding/evidence ID, reviewed commit, environment, exact command or procedure, fixture checksum, expected result, actual result, threshold, verifier, and date. Every reproduced finding must have a stable evidence ID and a reproducible procedure or automated test before closure. Every closed finding must link to passing evidence generated against the implementing revision. Third-party fixtures and images remain subject to REL-001.

---

## P0 — Release blockers

### [ ] REL-001 — Establish licenses and provenance for bundled third-party material

**Classification:** Type: Release task · Severity: Critical · Release gate: Yes (A2) · Confidence: Code-confirmed · Workstream: WS6  
**Tracking:** Status: Open · Owner role: Project owner + legal/release · Target: Before any public redistribution
**Dependencies:** None; parallel containment activity and absolute redistribution gate

**Evidence:** `docs/` contains an AMS paper PDF, Escher-related artwork, photographs, a transcript, and other images. The repository has one MIT `LICENSE` and no asset inventory or `THIRD_PARTY_NOTICES` file. Nearly all of these files are unreferenced by the application.

**Risk:** The MIT license can cover the original code, but it does not automatically grant redistribution rights for papers, artwork, photographs, or transcripts. Public source archives and npm packages currently include these assets.

**Required action:**

1. Inventory every file in `docs/`, recording source, author/owner, license, intended use, and redistribution permission.
2. Remove files without a documented redistribution basis or replace them with permissively licensed equivalents.
3. Add `THIRD_PARTY_NOTICES.md` and state explicitly that the code license does not override third-party asset licenses.
4. Add an automated release check that only approved assets are packaged.

**Acceptance criteria:** Every distributed non-code asset has documented provenance and an explicit redistribution basis.

---

## P1 — High priority

### [ ] UI-001 — Constrain the application to the viewport; the intended split-pane layout is currently broken

**Classification:** Type: Defect · Severity: High · Release gate: Yes · Confidence: Reproduced · Workstream: WS1 · Evidence ID: `REP-001`  
**Tracking:** Status: Open · Owner role: Frontend engineering · Target: Next production release
**Dependencies:** QA-001; approved Electron/browser viewport support matrix

**Evidence:** `body` uses `min-height: 100vh` with an unconstrained grid row (`index.html:21-30`). The control panel's content expands the grid instead of scrolling inside `#ctrl-panel`. In a 1280×820 viewport, browser measurements were:

- document height: approximately **1,931 px**;
- control panel height: approximately **1,850 px**;
- canvas area height: approximately **1,850 px**;
- output pane and status message begin below the initial viewport.

`overflow-y: auto` on `#ctrl-panel` therefore has no effect because its client height equals its full content height.

**Impact:** At the default Electron size, the user sees the source pane but must scroll the entire document to reach the output. Render progress and completion status are off-screen. This contradicts the documented fixed split-canvas interface.

**Required action:** Set a definite viewport height and prevent body-level overflow, for example by using `height: 100dvh`, `min-height: 0` on grid children, and `overflow: hidden` on the body. Keep scrolling inside the control panel only.

**Acceptance criteria:** At 1280×820 and 900×600, `document.documentElement.scrollHeight <= window.innerHeight + 1` CSS pixel, the control panel scrolls independently, and both source and output panes plus render status remain visible without body-level scrolling.

### [ ] MATH-001 — Separate “rotate” from “cut position”; both controls currently perform the same operation

**Classification:** Type: Defect / specification gap · Severity: High · Release gate: Yes (A1) · Confidence: Reproduced · Workstream: WS3 · Evidence ID: `REP-011`  
**Tracking:** Status: Open · Owner role: Math/rendering engineering · Target: Next production release
**Dependencies:** QA-001; approved independent rotation and branch-cut semantics

**Evidence:** The renderer and grid use `p.rotate + p.cutOffset` as one angle (`index.html:847`, `index.html:1060`). The two values are algebraically interchangeable. With slider quantization disabled for the test, a 0.5-radian rotate produced a pixel-identical result to a 0.5-radian cut offset.

**Impact:** The UI claims that `rotate` pre-rotates content while `cut position` only relocates the branch-cut seam. The implementation cannot perform those operations independently: changing the cut also rotates/phases the image, and changing rotate also moves the cut.

**Required action:** Implement a custom argument branch for the cut position instead of pre-rotating `w`. Keep content rotation/phase as a separate operation. Add regression tests proving that moving the cut relocates the discontinuity without globally rotating a seamless periodic source.

**Acceptance criteria:** For a seamless periodic fixture, applying the same nonzero delta to rotate and cut produces different image hashes. The rotate test changes global orientation while leaving the configured cut coordinate fixed; the cut test moves the discontinuity coordinate without the same global rotation. Both behaviors are covered by automated image tests.

### [ ] SAMPLE-001 — Implement genuinely periodic bilinear sampling

**Classification:** Type: Defect · Severity: High · Release gate: Yes (A1) · Confidence: Reproduced · Workstream: WS2 · Evidence ID: `REP-007`  
**Tracking:** Status: Open · Owner role: Math/rendering engineering · Target: Next production release
**Dependencies:** QA-001; shared production-function test harness or ARCH-001 extraction plan

**Evidence:** `sampleImage()` wraps `u` and `v`, but maps them with `u * (w - 1)` / `v * (h - 1)` and clamps the second sample at the last pixel (`index.html:636-652`, duplicated in the worker at `index.html:752-768`). For a two-pixel red/blue periodic texture:

- `u = 0.999` samples almost pure blue;
- `u = 1.001` wraps to almost pure red;
- there is no interpolation across the tile boundary.

**Impact:** Uploaded and generated textures show hard seams unless the first and last rows/columns are manually duplicated. The source coordinate spacing is also nonuniform because the texture is treated as `w - 1` intervals rather than `w` periodic texels.

**Required action:** Use periodic neighbors, for example `px = u * w`, `x0 = floor(px) % w`, and `x1 = (x0 + 1) % w`, with the equivalent logic for `v`. Decide explicitly whether source files contain duplicated boundary pixels and document that convention.

**Acceptance criteria:** For periodic fixtures without duplicated edge pixels, samples at `1 - 1e-6` and `0 + 1e-6` differ by no more than one 8-bit channel value in both axes, and interpolation uses the last and first texels as neighbors across each boundary.

### [ ] SAMPLE-002 — Fix the angular-fold/reflection apex discontinuity

**Classification:** Type: Defect · Severity: High · Release gate: Yes (A1) · Confidence: Reproduced · Workstream: WS2 · Evidence ID: `REP-008`  
**Tracking:** Status: Open · Owner role: Math/rendering engineering · Target: Next production release
**Dependencies:** SAMPLE-001 boundary-mode architecture; QA-001

**Evidence:** The fold maps `v = 0.5` to exactly `1` (`index.html:863-865`), after which `sampleImage()` immediately applies modulo and converts `1` to `0` (`index.html:638-639`). With a two-row source whose top is red and bottom is blue:

- folded `v = 0.499999` samples blue;
- folded `v = 0.5` samples red;
- folded `v = 0.500001` samples blue.

**Impact:** The reflection intended to remove the angular wrap seam inserts a one-sample discontinuity at the fold apex. The current README explanation is also backwards: a correctly implemented mirrored repeat can join the original `v = 0/1` seam without requiring the source edges to match, while retaining a derivative kink at the reflection point.

**Required action:** Give mirror mode a nonperiodic/clamped endpoint sampler after folding, or implement a proper mirrored-repeat boundary mode. Keep the exact `v = 1` endpoint addressable. Update the label and README to distinguish value continuity from the derivative kink/frequency doubling.

**Acceptance criteria:** For a top-red/bottom-blue fixture, samples immediately below, at, and immediately above the fold apex differ by no more than one 8-bit channel value from the expected clamped endpoint. The original angular seam maps to the same source edge on both sides and has no value discontinuity.

### [ ] DEMO-001 — Make built-in “log-space” sources actually periodic, or stop presenting them as valid examples

**Classification:** Type: Defect / misleading example · Severity: High · Release gate: Yes (A1) · Confidence: Reproduced · Workstream: WS2 · Evidence ID: `REP-006`  
**Tracking:** Status: Open · Owner role: Math/rendering engineering · Target: Next production release
**Dependencies:** SAMPLE-001; QA-001 seam/golden harness

**Evidence:** The generated band source changes brightness, lightness, and grid frequency as a direct function of `u` (`index.html:1114-1129`). Measured mean RGB edge differences were:

- `generateLogSpaceBands()`: left/right **161.18**, top/bottom **91.46**;
- `generatePlainGrid()`: left/right and top/bottom **55.37**;
- `generateEscherScene()`: top/bottom **14.70**.

The README simultaneously says the demos were rewritten for “correct log-space periodicity” (`README.md:212-214`) and later admits they are not strictly periodic (`README.md:174-176`).

**Impact:** The primary demo teaches and displays seam artifacts that the application describes as source-data errors. It cannot serve as a validation fixture for the conformal map.

**Required action:** Generate textures from periodic functions in both axes and validate seam-adjacent samples numerically. Alternatively, rename the current demos as intentionally nonperiodic stress tests and add at least one mathematically valid periodic fixture.

**Acceptance criteria:**

1. At least one reference generator is analytically periodic: `f(0,v) = f(1,v)` and `f(u,0) = f(u,1)` within `1e-9` per normalized channel over the complete test grid.
2. With periodic sampling, samples at `1 - 1e-6` and `1e-6` differ by no more than one 8-bit level at each wrap boundary for that fixture.
3. With angular folding disabled, its approved golden render passes the documented seam-image threshold.
4. Any intentionally nonperiodic demo is labeled “nonperiodic stress test” in both UI and README.

### [ ] MATH-002 — Resolve the `iterations` parameter's conflict with the advertised scale factor

**Classification:** Type: Decision / specification gap · Severity: High · Release gate: Yes (A1) · Confidence: Mathematically confirmed · Workstream: WS3  
**Tracking:** Status: Open · Owner role: Math/rendering engineering · Target: Decision before implementation
**Dependencies:** Approved source-period/frequency decision; QA-001

**Evidence:** Let `k = iterations`. The horizontal source coordinate is `u = k * Re(log z) / log N` (`index.html:860`), so one source-tile period occurs when:

\[
\Delta\operatorname{Re}(\log z)=\frac{\log N}{k}.
\]

The corresponding radial factor in the intermediate/source `z`-plane is `N^(1/k)`. For the rendered output plane, where the standard map uses `z = w^alpha`, define the adjacent-layer similarity by the same exponent used to define the configured `gamma`:

\[
\delta_k := \frac{\log N}{k\alpha}, \qquad
\gamma_k := \exp(\delta_k), \qquad
\frac{w_{\mathrm{next}}}{w}=\gamma_k.
\]

`gamma_k` is sometimes written `gamma^(1/k)`, but that notation is branch-ambiguous for a complex number; the authoritative value is `exp(log(N) / (k * alpha))`. The visible scale and rotation increments are `|gamma_k|` and `arg(gamma_k)`. The UI currently reports `N` and the full-period `gamma` as though each adjacent rendered layer represented one complete source period.

**Impact:** The control changes the fundamental period represented by the rendered image; it is not merely a computational iteration count. The terms "iterations," "scale (N)," "one source zoom level," and displayed self-similarity factor can refer to different quantities.

**Required action:** Record and implement one approved mathematical/product disposition:

1. **One-period model:** use `u = Re(log z) / log N` and expose view extent or layer count separately; or
2. **Frequency-multiplier model:** retain `k`, rename it to "repetitions per N-period," and compute/display the active visible similarity as `gamma_k = exp(log(N) / (k * alpha))`, including `|gamma_k|` and `arg(gamma_k)`.

Update the grid, presets, status panel, README, serialization, and tests from the same definition.

**Acceptance criteria:** For `k = 1`, `k = 2`, and the maximum supported `k`, an automated numerical test using the renderer's approved branch convention verifies that one `gamma_k` output step changes the unwrapped horizontal source coordinate by exactly one tile period within `1e-9` and changes the angular source coordinate by `0 mod 1` within `1e-9`. Displayed magnitude and angle agree with the computed `gamma_k` within `1e-6`. Every control, equation, grid interval, status value, and help text uses the selected model.

### [ ] MATH-003 — Correct or explicitly rename the outer-radius factor-of-two behavior

**Classification:** Type: Decision / specification gap · Severity: High · Release gate: Yes (A1) · Confidence: Mathematically confirmed · Workstream: WS3  
**Tracking:** Status: Open · Owner role: Math/rendering engineering · Target: Decision before implementation
**Dependencies:** Approved radius versus view-scale decision; QA-001

**Evidence:** Screen coordinates span approximately `[-2*r2, 2*r2]`, and circle clipping also occurs at `2*r2` (`index.html:833-840`). The README and UI call `r2` the outer boundary and say the circle clips at `r2` (`README.md:121`, `README.md:153`).

**Impact:** The actual outer radius is twice the displayed value. Because coordinate scaling and clipping both use the same factor, the circle remains the same pixel size while `r2` behaves primarily as a view-scale parameter.

**Required action:** Record and implement one approved disposition:

1. **Radius semantics:** map the screen and clip so the numeric value is the actual outer radius; or
2. **View-scale semantics:** retain the current mapping, rename the control and symbols so they no longer claim that `r2` is the clip radius, and document the `2*r2` domain explicitly.

Update presets, grid inversion, equations, labels, and tests together.

**Acceptance criteria:**

- Under the radius-semantics disposition, the renderer and grid clip at exactly the displayed `r2` value and the approved image baseline reflects the intentional visual change.
- Under the view-scale disposition, no active label or equation calls the value the outer radius, and tests verify the documented `2*r2` mapping.

Only one disposition may be marked complete.

### [ ] MODE-001 — Apply output-shape behavior consistently in Cartesian transform modes

**Classification:** Type: Defect · Severity: High · Release gate: Yes · Confidence: Reproduced · Workstream: WS2 · Evidence ID: `REP-003`  
**Tracking:** Status: Open · Owner role: Math/rendering engineering · Target: Next production release
**Dependencies:** Approved Cartesian output-domain decision; QA-001

**Evidence:** `renderNonDrostePixels()` never reads `p.outputShape` (`index.html:881-934`). A `z2` render in circle mode and square mode produced identical canvas dimensions and identical pixel hashes.

**Impact:** The always-visible Output Shape control is a no-op for circle versus square in every non-Droste mode. Users receive a square image while the UI shows “circle” as active.

**Required action:** Either implement circle clipping in Cartesian modes, hide/disable unsupported shape controls by mode, or define a separate Cartesian clipping model.

**Acceptance criteria:** In every mode where Output Shape is enabled, circle and square produce different documented domains and image hashes. In any mode where shape selection is unsupported, the control is disabled or hidden, its state cannot affect parameters, and the limitation is explained accessibly.

### [ ] MODE-002 — Stop silently tiling Cartesian source images outside their domain

**Classification:** Type: Decision / defect · Severity: High · Release gate: Yes · Confidence: Code-confirmed · Workstream: WS2  
**Tracking:** Status: Open · Owner role: Math/rendering engineering · Target: Next production release
**Dependencies:** Approved Cartesian boundary policy; SAMPLE-001; QA-001

**Evidence:** Both renderers call the same modulo-wrapping `sampleImage()` (`index.html:922`). For `z^n`, `exp`, `log`, and multiplication, inverse-mapped coordinates outside `[-S, S]^2` re-enter from the opposite edge instead of being clipped, made transparent, or handled by an explicit texture-wrap option.

**Impact:** Cartesian maps can show repeated copies and discontinuities unrelated to the selected complex transform. The UI says the complex plane maps directly onto the source image, but does not disclose periodic tiling.

**Required action:** Split periodic log-space sampling from Cartesian sampling. Add an explicit Cartesian boundary mode such as background, clamp, mirror, or tile; default to a documented behavior.

**Acceptance criteria:** Each enabled Cartesian boundary policy has fixture-based tests at all four source edges and corners for every transform. The default policy is visible in state, documented, and produces no implicit modulo wrap unless Tile is explicitly selected.

### [ ] MATH-004 — Make all displayed alpha/gamma values correspond to the transform actually rendered

**Classification:** Type: Defect · Severity: High · Release gate: Yes (A1) · Confidence: Reproduced · Workstream: WS3 · Evidence ID: `REP-009`  
**Tracking:** Status: Open · Owner role: Math/rendering engineering · Target: Next production release
**Dependencies:** MATH-002 disposition; canonical state; QA-001

**Evidence:** The math panel always computes the standard Droste `alpha` and `gamma` from `N` (`index.html:1282-1304`). The worker always returns the standard `gamma` even for `droste-swapped`, arbitrary `power-explore`, and reverse/conjugate modes (`index.html:808-820`, `index.html:878`). For example, `c = 0 + 0i` renders a constant field while status still reports `|gamma| = 22.5837` and the math panel still shows `alpha = 1 - 0.8825i`.

**Impact:** Mathematical diagnostics are false for three supported transform variants. Users cannot use the panel to verify the active map.

**Required action:** Compute mode-specific invariants, label values as not applicable when no corresponding quotient/self-similarity exists, and include reverse state. Do not display the standard `gamma` for arbitrary powers.

**Acceptance criteria:** The math panel and completion status are derived from the exact `effectiveAlpha` and active mode, with tests for standard, swapped, reverse, and arbitrary-power cases.

### [ ] GRID-001 — Make the conformal grid represent the actual sampled mapping

**Classification:** Type: Defect / decision · Severity: High · Release gate: Yes (A1) · Confidence: Code-confirmed · Workstream: WS3  
**Tracking:** Status: Open · Owner role: Math/rendering engineering · Target: Decision before implementation
**Dependencies:** MATH-001 through MATH-004 dispositions; approved grid-availability policy; QA-001

**Evidence:** `drawConformalGrid()` inverts only the unfurled power map (`index.html:1049-1099`). It does not account for:

1. angular folding (`p.mirror`) even though folding is enabled by default;
2. square/rect output domains - the grid always rejects `|w| > 2*r2` (`index.html:1065`) while those renderers do not;
3. `effectiveAlpha = 0`, where `1/alpha` becomes nonfinite and grid drawing silently produces no useful lines.

**Impact:** The overlay advertised as "true conformal coordinate lines" is wrong or incomplete under common UI states.

**Required action:** Record and implement one approved disposition:

1. extend the overlay to model every supported post-map sampling operation and output domain; or
2. declare unsupported/non-invertible states, disable the overlay in those states, and provide an accessible explanation.

**Acceptance criteria:** For every state in which the grid remains enabled, a 1024x1024 reference test evaluates at least 200 nonsingular grid points for circle, square, rect, reverse on/off, and mirror on/off where the approved model defines an overlay. The 95th-percentile distance between projected reference points and the rendered overlay is no greater than `1.5` output pixels and the maximum is no greater than `3` pixels. For unsupported or non-invertible states, the grid is disabled or forced off, its unavailability is programmatically exposed and explained, no grid path is drawn, and no canvas path call receives a nonfinite coordinate. `effectiveAlpha = 0` follows the unsupported-state path unless an approved mathematical alternative is documented.

### [ ] FILE-001 — Add file-size and decoded-resource limits before upload processing

**Classification:** Type: Resource-exhaustion risk · Severity: High · Release gate: Yes (A4) · Confidence: Code-confirmed · Workstream: WS4  
**Tracking:** Status: Open · Owner role: Application engineering · Target: Next production release
**Dependencies:** Approved byte/pixel/memory limits and image-format policy; QA-001

**Evidence:** `loadFile()` reads the entire file as a base64 data URL before any size check (`index.html:1655-1694`). The 1024-pixel downscale occurs only after the browser has read and decoded the full source.

**Impact:** A very large or decompression-heavy image can consume excessive memory, freeze the renderer, or terminate the process. Data URLs add additional memory overhead.

**Required action:** Enforce documented limits before reading and before allocating a decode/output canvas. Prefer an object URL or `createImageBitmap`, revoke temporary resources, and report limit failures clearly. Unless an architecture decision record approves alternatives, use initial limits of **25 MiB encoded input** and **16,777,216 decoded pixels**.

**Acceptance criteria:** Tests reject a file of `MAX_UPLOAD_BYTES + 1` before `FileReader`/decode and reject decoded dimensions exceeding `MAX_DECODED_PIXELS` before full-size canvas allocation. A controlled stress test records peak renderer memory no greater than baseline plus **256 MiB**, and all temporary object URLs/bitmaps are released after success, failure, replacement, and cancellation.

### [ ] FILE-002 — Prevent asynchronous image-load races

**Classification:** Type: Race-condition defect · Severity: High · Release gate: Yes · Confidence: Code-confirmed · Workstream: WS4  
**Tracking:** Status: Open · Owner role: Application engineering · Target: Next production release
**Dependencies:** Canonical load ID/state; QA-001 delayed-callback harness

**Evidence:** FileReader and Image callbacks have no load-generation token or cancellation. Selecting file B while file A is still reading/decoding allows A's later callback to overwrite B. The same race exists between a pending file load and a built-in demo button.

**Impact:** The source shown/rendered can differ from the user's most recent selection.

**Required action:** Track a monotonically increasing load ID, abort the previous reader where possible, and ignore callbacks that are not current.

**Acceptance criteria:** A deterministic delayed-load test proves that only the latest file or demo selection can update source state.

### [ ] A11Y-001 — Meet a defined accessibility baseline for names, focus, status, state, and contrast

**Classification:** Type: Compliance / usability defect · Severity: High · Release gate: Yes (A5) · Confidence: Reproduced and code-confirmed · Workstream: WS1  
**Tracking:** Status: Open · Owner role: Frontend engineering + quality · Target: Next production release
**Dependencies:** Approved accessibility target/support matrix; UI-001; canonical state

**Evidence:** Nineteen visible `<label>` elements are neither associated with a control using `for` nor wrapping one. Range inputs have `outline: none` and no replacement focus style (`index.html:62-78`). The status and progress elements have no live-region/progress semantics, and shape buttons expose selected state only through CSS. The muted `#666` text on `#0d0d0d` has a measured contrast ratio of approximately **3.38:1**.

**Impact:** Screen-reader users encounter unnamed sliders/selects; keyboard users cannot reliably see range focus; render completion is not announced; selected shape is not conveyed; several small-text elements fail normal-text contrast targets.

**Required action:** Adopt **WCAG 2.2 Level AA** as the provisional conformance target and:

- add `for`/`id` associations or wrap controls in labels;
- add visible `:focus-visible` styles, including `#drop-zone:focus-within`;
- use `role="status"`/`aria-live`, a semantic progress element or valid progressbar ARIA, and `aria-busy` while rendering;
- add `aria-pressed` or a radio-group model for shape buttons;
- adjust colors to meet applicable contrast requirements;
- document the supported keyboard and screen-reader test matrix.

**Acceptance criteria:** Automated accessibility testing reports zero critical or serious violations and no unnamed controls or contrast failures. A manual keyboard test reaches and operates every interactive element with visible focus. Render start, failure, cancellation, and completion are announced in at least one supported screen reader on each release platform. Any exception is documented with rationale and an approved remediation date.

### [ ] QA-001 — Establish automated characterization, regression, integration, visual, and packaging tests

**Classification:** Type: Quality-system control gap · Severity: Medium · Release gate: Yes · Confidence: Code-confirmed · Workstream: WS6  
**Tracking:** Status: Open · Owner role: Quality engineering · Target: Before first remediation merge
**Dependencies:** Approved support matrix and baseline fixtures; no code-correction dependency

**Evidence:** `package.json` has no `test`, `lint`, `format`, or validation scripts (`package.json:6-10`). The current defects include invalid preset values, stale reset state, control no-ops, race conditions, and mathematical/display drift that automated tests would detect.

**Impact:** Functional corrections cannot be distinguished reliably from regressions, and intentional mathematical output changes have no controlled approval path.

**Required action:**

1. Before changing each reproduced defect, add a failing regression test or a characterization test that captures the current behavior and the approved expected change.
2. Add unit tests for complex arithmetic, parameter derivation, sampling boundary modes, color modes, and coordinate transforms.
3. Add browser tests for every mode, preset, shape, reset, auto-render path, file-load race, save-readiness state, and viewport matrix.
4. Add visual/golden tests for periodic seams, branch-cut behavior, output domains, and grid alignment.
5. Add Electron launch and packaged-artifact smoke tests.
6. Run syntax, lint, tests, and packaging checks in CI.

**Acceptance criteria:** CI blocks merging when a preset is invalid, a documented control is an unexpected no-op, output dimensions/state are wrong, a stale job mutates current state, or a golden rendering changes without an explicit baseline-approval record. Each closed finding links to the test that would fail if the defect recurred.

### [ ] RENDER-002 — Add a real render state and handle synchronous worker/canvas failures

**Classification:** Type: Defect · Severity: High · Release gate: Yes · Confidence: Code-confirmed · Workstream: WS4  
**Tracking:** Status: Open · Owner role: Application engineering · Target: Next production release
**Dependencies:** Canonical render state; RENDER-001 job identity; QA-001

**Evidence:** `new Worker()`, canvas allocation, and `postMessage()` are outside a `try/catch`. The output canvas is resized and shown before work succeeds (`index.html:975-988`). On worker failure, the placeholder remains hidden and a blank canvas remains saveable. Buttons are not disabled or marked busy.

**Required action:** Track `idle/rendering/succeeded/failed`, retain the last successful image until replacement succeeds, catch synchronous failures, and disable or gate Save while no successful frame exists.

**Acceptance criteria:** Tests force failure at worker construction, output-canvas allocation/resize, and `postMessage()`. Each failure transitions `rendering -> failed`, reports the failing stage, preserves the last successful frame and render ID, clears busy/progress state, rejects late messages, and prevents Save from treating the failed job as valid. A subsequent valid render can recover without reloading the page.

### [ ] SAVE-001 — Save only completed renders and report platform-accurate download outcomes

**Classification:** Type: Defect · Severity: High · Release gate: Yes · Confidence: Code-confirmed · Workstream: WS4  
**Tracking:** Status: Open · Owner role: Application engineering · Target: Next production release
**Dependencies:** RENDER-002; approved browser/Electron save semantics; QA-001

**Evidence:** Save checks only `out.style.display !== 'none'` (`index.html:1582-1593`). The canvas becomes visible and is cleared at render start, so Save can export an incomplete or blank image during rendering or after a worker error. The status immediately says “PNG saved” without confirmation from the browser or Electron download system.

**Impact:** Users can produce an invalid deliverable while the application reports success.

**Required action:** Gate Save on the ID of the latest successful render, disable it during rendering and failure states, catch serialization/download errors, and use a mode/parameter-aware filename. In standalone-browser mode, report only that a download was initiated unless the platform exposes completion. In Electron, use a save dialog or download event integration to report confirmed completion or failure.

**Acceptance criteria:** Save is unavailable before the first successful render, while a render is active, and after a failed replacement when no valid prior frame exists. A browser test verifies “download initiated” wording; an Electron integration test verifies confirmed success/failure reporting and prevents a blank or partial frame from being written.

### [ ] SEC-001 — Define and enforce an Electron/content security policy

**Classification:** Type: Security-control gap · Severity: High · Release gate: Yes (A2, A4) · Confidence: Code-confirmed · Workstream: WS6  
**Tracking:** Status: Open · Owner role: Security/platform engineering · Target: Before public desktop release
**Dependencies:** Approved Electron runtime/threat model and image-format policy; QA-001

**Evidence:** There is no CSP, the renderer uses a large inline script/style and a `blob:` worker, and the Electron main process does not explicitly restrict navigation or window creation. The file picker accepts all `image/*`, including formats such as SVG that require a deliberate policy.

**Required action:**

- move script/style to external files or use nonces/hashes;
- add a CSP that explicitly permits only required sources, including the worker strategy;
- explicitly set renderer sandboxing and deny unexpected navigation/new-window requests;
- define whether SVG is rejected, sanitized, or supported and tested.

**Acceptance criteria:** A packaged-Electron integration test completes a normal load/render/save flow with zero unexpected CSP violations. `nodeIntegration` remains false, `contextIsolation` and sandboxing are enabled, test navigation and `window.open` attempts are denied, unapproved external network requests fail, and the approved SVG policy is enforced by automated fixtures. Any required CSP source (including the chosen worker strategy) is documented and no broader source is permitted.

---

## P2 — Medium priority

### [ ] UI-002 — Update or remove the hard-coded `N = 256` formula in the header

**Classification:** Type: Defect · Severity: Medium · Release gate: No · Confidence: Reproduced · Workstream: WS1 · Evidence ID: `REP-004`  
**Tracking:** Status: Open · Owner role: Frontend engineering · Target: Next planned minor release
**Dependencies:** QA-001 characterization coverage; canonical validated state design

**Evidence:** The header text is static (`index.html:266`). After changing `N` to 16, the alpha panel and footer show 16 while the header still says `log 256`.

**Impact:** The page simultaneously presents incompatible parameter values, which undermines mathematical verification.

**Required action:** Bind the header formula to canonical application state, or label it explicitly as a fixed historical Escher example and separate it visually from live diagnostics.

**Acceptance criteria:** Every displayed formula either updates from current state in the same render cycle or is explicitly labeled as a fixed reference value. A browser test changes `N` and verifies all live formula locations.

### [ ] STATE-001 — Fix the broken Print Gallery color preset

**Classification:** Type: Defect · Severity: Medium · Release gate: No · Confidence: Reproduced · Workstream: WS1 · Evidence ID: `REP-002`  
**Tracking:** Status: Open · Owner role: Frontend engineering · Target: Next planned minor release
**Dependencies:** UI-004 schema validation; QA-001 preset tests

**Evidence:** The preset assigns `sel-color: 'none'` (`index.html:1534-1539`), but valid option values are `retain`, `grayscale`, `sepia`, `invert`, `warm`, `cool`, `red`, `green`, and `blue` (`index.html:436-446`). After clicking the preset, runtime state was `value === ''` and `selectedIndex === -1`.

**Impact:** The color selector becomes blank. Rendering happens to retain color only because the color switch has an identity default path; the UI and state are invalid.

**Required action:** Use `retain`, validate every preset assignment against the target control, and fail loudly in development when an invalid value is supplied.

**Acceptance criteria:** Every preset leaves every select element with `selectedIndex >= 0`; add an automated preset-state test.

### [ ] STATE-002 — Reset every parameter, including aspect ratio, from one source of truth

**Classification:** Type: Defect · Severity: Medium · Release gate: No · Confidence: Reproduced · Workstream: WS1 · Evidence ID: `REP-005`  
**Tracking:** Status: Open · Owner role: Frontend engineering · Target: Next planned minor release
**Dependencies:** Canonical default-state object; QA-001

**Evidence:** The reset handler does not reset `sel-aspect`. After setting 9:16 portrait and clicking Reset, the active shape becomes circle but `sel-aspect` remains `1.7778`; choosing rect again restores the stale portrait value. Defaults are duplicated between HTML attributes and JavaScript (`index.html:1595-1638`).

**Required action:** Define a canonical default-state object, include every control, and derive/reset UI state from it.

**Acceptance criteria:** A test mutates every control, runs reset, and confirms all values and selected/visible states match canonical defaults.

### [ ] STATE-003 — Make presets deterministic rather than dependent on hidden prior state

**Classification:** Type: Defect / behavior decision · Severity: Medium · Release gate: No · Confidence: Code-confirmed · Workstream: WS1  
**Tracking:** Status: Open · Owner role: Frontend engineering · Target: Next planned minor release
**Dependencies:** Approved complete-versus-partial preset semantics; canonical state; QA-001

**Evidence:** Most presets set only a subset of parameters. Reverse, mirror, grid, color, cut, phase, zoom, shape, and other values can carry over. The Print Gallery preset can also be used while `droste-swapped` remains active because it does not switch modes.

**Impact:** The same preset can produce different output depending on prior interactions, undermining reproducibility and support.

**Required action:** Define whether presets are complete snapshots or partial adjustments. Prefer complete named snapshots; show exactly what is preserved if partial behavior is intentional.

**Acceptance criteria:** Applying the same preset from arbitrary initial states produces the same parameter object and image hash.

### [ ] SLIDER-001 — Align the cut slider's range, step, stored value, and displayed value

**Classification:** Type: Defect · Severity: Medium · Release gate: No · Confidence: Reproduced · Workstream: WS1 · Evidence ID: `REP-010`  
**Tracking:** Status: Open · Owner role: Frontend engineering · Target: Next planned minor release
**Dependencies:** UI-004; canonical numeric state; QA-001

**Evidence:** `sl-cut` has `min=-3.14159`, `step=0.01`, and default `1.5708` (`index.html:405`). Chromium sanitizes the initial value to **1.56841**, while the UI displays `pi/2`. Assigning 0 is sanitized to approximately **-0.00159**, yet `fmtCut()` displays 0. Preset displays are formatted from requested values rather than the sanitized control value.

**Impact:** The UI can report a mathematically special angle that is not actually in use, and exact zero is not representable.

**Required action:** Use an aligned integer/fraction-of-pi representation or `step="any"`; always format `element.valueAsNumber` after assignment.

**Acceptance criteria:** Zero, +/-pi/2, and +/-pi are exactly representable and displayed state equals `getParams()` state.

### [ ] RENDER-001 — Reject stale worker messages with an explicit render generation/job ID

**Classification:** Type: Race-condition risk · Severity: Medium · Release gate: Conditional · Confidence: Inferred from code · Workstream: WS4  
**Tracking:** Status: Open · Owner role: Application engineering · Target: Next planned minor release
**Dependencies:** Render job identity/state; QA-001 delayed-worker harness

**Evidence:** A new render terminates `_activeWorker`, but message handlers do not check that the emitting worker is still current before updating progress or drawing (`index.html:966-1028`). The identity comparison is used only when clearing the reference.

**Risk:** A queued message from a superseded worker could overwrite current progress or output. Worker termination usually reduces this window, but the code has no correctness guard.

**Required action:** Attach a render ID to every request/message and return immediately from handlers when it is stale.

**Acceptance criteria:** A test with delayed/fake workers proves old progress and completion messages cannot affect the current render.

### [ ] IMG-001 — Preserve or explicitly flatten source alpha

**Classification:** Type: Behavior decision / defect · Severity: Medium · Release gate: Conditional · Confidence: Code-confirmed · Workstream: WS2  
**Tracking:** Status: Open · Owner role: Math/rendering engineering · Target: Decision before implementation
**Dependencies:** Approved alpha/compositing policy; SAMPLE-001; QA-001

**Evidence:** `sampleImage()` returns only RGB and every output pixel is assigned alpha 255 (`index.html:649-652`, `index.html:870-874`, and worker copies). Transparent source pixels therefore become opaque, usually black.

**Required action:** Bilinearly sample alpha and decide whether output preserves transparency or composites onto a configurable background.

**Acceptance criteria:** A transparent test PNG produces the documented alpha behavior in the saved output.

### [ ] GRID-002 — Add finite/bounds guards to grid projection

**Classification:** Type: Defect · Severity: Medium · Release gate: Conditional · Confidence: Code-confirmed · Workstream: WS3  
**Tracking:** Status: Open · Owner role: Math/rendering engineering · Target: Next planned minor release
**Dependencies:** GRID-001 disposition; finite-coordinate guards; QA-001

**Evidence:** `uvToScreen()` can return coordinates containing `NaN`/`Infinity` when `alpha` is zero or near zero, because it checks only radial comparisons and not finiteness (`index.html:1053-1069`). Canvas currently ignores the unusable geometry silently.

**Required action:** Return `null` for nonfinite inverse parameters/coordinates and show an “overlay unavailable” state for non-invertible maps.

**Acceptance criteria:** No canvas path call receives a nonfinite coordinate under the full slider range.

### [ ] ARCH-001 — Eliminate duplicated math/sampling/color implementations

**Classification:** Type: Architecture debt · Severity: Medium · Release gate: No · Confidence: Code-confirmed · Workstream: WS5  
**Tracking:** Status: Open · Owner role: Application architecture · Target: Before broad math refactoring
**Dependencies:** QA-001 characterization coverage for exact production behavior

**Evidence:** `C`, `computeParams`, `sampleImage`, and `applyColorMode` are manually duplicated between page scope and the worker template (`index.html:550-711`, `index.html:716-806`). The page-scope sampler and color function are effectively dead in normal rendering.

**Impact:** Fixes can be applied to one copy and not the other. Unit tests may exercise a different implementation than production worker code.

**Required action:** Move shared pure functions into one worker/module source or generate the worker from imported modules. Test the exact production functions.

**Acceptance criteria:** Each algorithm has one implementation and one test suite.

### [ ] PERF-001 — Remove redundant per-pixel transcendental work and allocations

**Classification:** Type: Performance improvement · Severity: Medium · Release gate: No · Confidence: Code-confirmed · Workstream: WS5  
**Tracking:** Status: Open · Owner role: Application architecture + rendering engineering · Target: After correctness baseline
**Dependencies:** ARCH-001 or equivalent shared hot path; approved performance baseline

**Evidence:** The Droste loop computes `fromPolar -> log -> exp -> log` (`index.html:847-851`). The final `log(exp(q))` can be replaced by the already available unwrapped complex value for source-coordinate normalization. `sampleImage()` and `applyColorMode()` each allocate an array per pixel.

**Impact:** At high resolution this creates millions of temporary arrays and performs avoidable trigonometric, exponential, and logarithmic operations.

**Required action:** Establish a benchmark before modification. Normalize directly from the complex product, avoid reconstructing `w` where possible, write channels into scalars or the destination buffer, and fast-path retain/zero-intensity cases.

**Acceptance criteria:** On a documented reference machine, using the same 2048×2048 fixture and parameters for at least 10 measured runs after two warm-ups, median render time improves by at least **20%** or allocation volume decreases by at least **50%**. Pixel output is identical for unchanged mathematics, or any intentional difference has an approved golden-baseline record.

### [ ] RENDER-003 — Remove redundant render scheduling

**Classification:** Type: Scheduling defect · Severity: Medium · Release gate: No · Confidence: Code-confirmed · Workstream: WS4  
**Tracking:** Status: Open · Owner role: Application engineering · Target: Next planned minor release
**Dependencies:** RENDER-001 and RENDER-002; canonical scheduler; QA-001

**Evidence:** Built-in demo handlers call `applyPreset()` and then `render()` explicitly (`index.html:1446-1477`). With auto-render enabled, `applyPreset()` already starts a render, so the explicit call immediately terminates and replaces it. Pending slider debounce timers are also not canceled by explicit renders/reset/presets.

**Required action:** Route all render requests through one scheduler that coalesces changes, cancels pending debounce work, and records the reason/job state.

**Acceptance criteria:** One user action starts at most one final render unless an intermediate preview mode is explicitly enabled.

### [ ] DOC-001 — Replace or clearly retire the stale `CODE_REVIEW.md`

**Classification:** Type: Documentation defect · Severity: Medium · Release gate: No · Confidence: Code-confirmed · Workstream: WS6  
**Tracking:** Status: Open · Owner role: Technical writing + engineering · Target: Next planned minor release
**Dependencies:** Approval of this controlled backlog as the active review record

**Evidence:** `CODE_REVIEW.md` describes a 1,558-line file, main-thread chunked rendering, a generation counter, an `innerHTML` XSS issue, and an unguarded `C.div`. The current file is 1,702 lines, uses a Web Worker, no longer uses the described `innerHTML`, and guards division by zero. It also recommends a CSP that omits the `blob:` worker requirement and would break the current renderer.

**Impact:** The repository's authoritative-looking review gives maintainers false risk and architecture information, obsolete line references, and a potentially breaking remediation.

**Required action:** Mark it superseded and replace it with a dated review tied to a commit, or remove it. Keep findings in an issue tracker or this TODO with verification status.

**Acceptance criteria:** No active review document refers to removed code paths or supplies a CSP incompatible with the worker implementation.

### [ ] DOC-002 — Bring README and in-app theory text into sync with the current application

**Classification:** Type: Documentation defect · Severity: Medium · Release gate: Yes (A1, A3) · Confidence: Code-confirmed · Workstream: WS3  
**Tracking:** Status: Open · Owner role: Technical writing + math/rendering engineering · Target: Before release claims are updated
**Dependencies:** Verified dispositions/implementations for affected math, sampling, grid, mode, and platform findings

**Evidence:** Confirmed drift includes:

- `index.html` is about 1,702 lines, not approximately 1,150 (`README.md:186`).
- README does not document the Transform Mode section, Cartesian maps, power-explore, reverse, or new presets.
- It describes the old generation-counter architecture rather than worker termination (`README.md:201-204`).
- It says any image becomes vertically periodic after wrapping (`README.md:67`), which is false with the current non-cross-boundary sampler and arbitrary unmatched edges.
- It claims demo generators have correct periodicity (`README.md:212-214`), contradicted by both measurements and the Known limitations section.
- Its angular-fold description says source edges must match for seam removal (`README.md:132`); a correct mirrored repeat joins the original seam without matching edges, while the current implementation has a separate endpoint-wrap defect.
- “circle: radial clip at r2” conflicts with the `2*r2` implementation.
- The in-app theory says “No hole” (`index.html:509`) while the renderer deliberately clips an inner radius and the map is singular at the origin.

**Impact:** Users and maintainers cannot determine which equations, controls, limitations, or architecture statements are authoritative.

**Required action:** Update documentation only after the associated mathematical and product decisions are approved. Generate or validate control/value references from canonical state where practical. Add a documentation review checklist that covers equations, mode availability, boundary policies, security constraints, supported platforms, and known limitations.

**Acceptance criteria:** README and in-app theory describe the implemented controls, equations, boundary modes, and architecture without contradiction. Documentation tests or review scripts flag stale control IDs, unsupported option values, and fixed parameter claims that conflict with live state.

### [ ] REPO-001 — Reduce package/repository bloat and remove duplicate/unreferenced files

**Classification:** Type: Release-content control gap · Severity: Medium · Release gate: Yes (A2) · Confidence: Code-confirmed · Workstream: WS6  
**Tracking:** Status: Open · Owner role: Release engineering · Target: Before public packaging
**Dependencies:** REL-001 asset disposition; approved package allowlist

**Evidence:** `npm pack --dry-run` includes approximately **8.0 MB** of docs/assets because there is no npm `files` allowlist or `.npmignore`. Most `docs/` files are unreferenced. `docs/regdivbirds.jpg` and `docs/regdivbirds (1).jpg` are byte-identical.

**Required action:** Remove duplicates, delete or archive unused research files outside the distributable repository, and add an npm package allowlist if publication is intended.

**Acceptance criteria:** The source/npm package contains only approved, referenced material and no duplicate binaries.

### [ ] REL-002 — Complete distributable-release configuration and validation

**Classification:** Type: Release task · Severity: Medium · Release gate: Yes (A2) · Confidence: Code-confirmed · Workstream: WS6  
**Tracking:** Status: Open · Owner role: Release engineering · Target: Before production release
**Dependencies:** REL-001; BUILD-001; SEC-001; QA-001; REPO-001

**Evidence:** Build targets are declared, but there is no committed lockfile, icon set, signing/notarization configuration, publisher metadata, release workflow, or packaged-app smoke test. `author` is blank (`package.json:13`).

**Required action:** Define supported platforms, artifact naming, icons, signing/notarization policy, update strategy, and release verification. Do not describe the project as production-ready until packaged artifacts are tested.

**Acceptance criteria:** CI produces and smoke-tests intended artifacts; release requirements and known unsigned-build limitations are documented.

### [ ] BUILD-001 — Commit a dependency lockfile and define the supported runtime

**Classification:** Type: Build-control gap · Severity: Medium · Release gate: Yes (A2) · Confidence: Code-confirmed · Workstream: WS6  
**Tracking:** Status: Open · Owner role: Release engineering · Target: Before release packaging
**Dependencies:** Approved Node/npm/Electron support matrix

**Evidence:** `package.json` uses caret ranges for Electron and electron-builder (`package.json:15-17`) and no lockfile is present. The README states Node.js >=18, but `package.json` has no `engines` declaration.

**Impact:** Fresh installs are not byte-for-byte reproducible and may resolve different transitive dependency trees. Build failures cannot be reliably reproduced from the repository revision alone.

**Required action:** Generate and commit `package-lock.json`, use `npm ci` in CI, document the supported Node/npm/Electron matrix, and add an `engines` field.

**Acceptance criteria:** A clean checkout builds with `npm ci` using the committed lockfile in CI.

### [ ] UI-003 — Add responsive behavior for standalone-browser use

**Classification:** Type: Compatibility defect / enhancement · Severity: Medium · Release gate: Yes (A3) · Confidence: Code-confirmed · Workstream: WS1  
**Tracking:** Status: Open · Owner role: Frontend engineering · Target: Before claiming standalone-browser support
**Dependencies:** Approved standalone-browser support matrix; UI-001; A11Y-001

**Evidence:** The layout has a fixed 340 px control column and no media queries (`index.html:21-30`). The README advertises direct use in any modern browser, but narrow windows leave very little canvas space and no stacked/mobile layout.

**Required action:** Add breakpoints that stack controls/canvases or provide a collapsible control panel while preserving the intended Electron desktop layout. Document the minimum supported browser viewport.

**Acceptance criteria:** At **360×640**, **390×844**, **768×1024**, **900×600**, and **1280×820** CSS pixels, there is no unintended horizontal body scroll; every control, canvas, status message, and primary action remains reachable; focus order follows the visual order; and a render can be started, observed, and saved or canceled.

### [ ] FILE-003 — Make supported image-format behavior explicit and retry-safe

**Classification:** Type: Compatibility / input defect · Severity: Medium · Release gate: Yes (A4) · Confidence: Code-confirmed · Workstream: WS4  
**Tracking:** Status: Open · Owner role: Application engineering · Target: Next planned minor release
**Dependencies:** Approved image-format policy; FILE-001; FILE-002; SEC-001

**Evidence:** The picker accepts `image/*`; the rejection message lists only PNG/JPEG/WEBP/GIF; animated GIF behavior and SVG policy are undocumented. The file input value is not cleared, so selecting the same file again may not fire `change` after a failure or intentional reload.

**Required action:** Publish a tested format list, clear/reset the input after handling, and report animation/alpha/SVG behavior accurately.

**Acceptance criteria:** Each advertised format has an automated load test, and reselecting the same file reliably triggers a load.

### [ ] MATH-005 — Document inverse-sampling branches and singularities for Cartesian maps

**Classification:** Type: Specification / documentation gap · Severity: Medium · Release gate: Yes (A1) · Confidence: Code-confirmed · Workstream: WS3  
**Tracking:** Status: Open · Owner role: Math/rendering engineering · Target: Before mathematical claims are finalized
**Dependencies:** Approved Cartesian mode/branch specification; DOC-002

**Evidence:** The UI calls `z^2` and `z^3` conformal, but rendering uses only the principal inverse root (`index.html:899-901`). `exp` uses principal `log`, `log` uses `exp`, and all have branch/non-injectivity implications. `z^2` is not conformal at the origin, and arbitrary half-step `n` values introduce branch-defined powers.

**Required action:** Explain that image warping uses one inverse branch, mark singular/branch-cut locations, and decide whether `n` should be integer-only or renamed as a general exponent.

**Acceptance criteria:** Mode documentation and labels accurately state branch choice and domains where the map is locally conformal.

### [ ] UI-004 — Validate control assignments after browser sanitization

**Classification:** Type: Preventive control gap · Severity: Medium · Release gate: No · Confidence: Reproduced and code-confirmed · Workstream: WS1  
**Tracking:** Status: Open · Owner role: Frontend engineering · Target: Before preset/state refactoring
**Dependencies:** Canonical typed state/schema design; QA-001

**Evidence:** `applyPreset()` silently skips missing IDs and formats requested values rather than the control's actual sanitized value (`index.html:1486-1517`). The cut-slider and invalid Print Gallery option defects demonstrate that requested values can differ from effective control state.

**Impact:** Invalid or out-of-range assignments can leave the DOM, displayed values, and renderer parameter object inconsistent.

**Required action:** Validate presets and programmatic assignments against a typed control schema, then read back and store the browser-effective value. Reject missing IDs, invalid select options, nonfinite values, and unexpected range coercion in development and tests.

**Acceptance criteria:** A generated test applies every preset and boundary value, confirms that DOM values equal canonical state, and fails on a missing control, invalid option, or unapproved browser sanitization.

---

## P3 — Low priority / cleanup

### [ ] MATH-006 — Use the exact Escher alpha in the “Escher alpha” power preset

**Classification:** Type: Defect · Severity: Low · Release gate: No · Confidence: Code-confirmed · Workstream: WS3  
**Tracking:** Status: Open · Owner role: Math/rendering engineering · Target: Backlog
**Dependencies:** MATH-004 shared derivation; canonical parameter state

**Evidence:** The preset uses `Im(c) = -0.88` (`index.html:1543-1545`) rather than the computed `-log(256)/(2*pi)`, approximately `-0.88254`.

**Impact:** A preset presented as mathematically exact is only approximate and will drift if `N` changes.

**Required action:** Compute the preset value from the active or explicitly fixed `N`, or rename it to identify the approximation.

**Acceptance criteria:** The preset either matches the computed value within `1e-12` for its declared `N`, or its label and documentation state the approximation and fixed parameter basis.

### [ ] UX-001 — Improve export naming and provenance

**Classification:** Type: Enhancement · Severity: Low · Release gate: No · Confidence: Code-confirmed · Workstream: WS6  
**Tracking:** Status: Open · Owner role: Product + release engineering · Target: Backlog
**Dependencies:** SAVE-001; canonical parameter state and release/build identifier

**Evidence:** The filename is always `droste-escher.png`, including for Cartesian modes, and exported images contain no readily associated parameter record.

**Impact:** Multiple exports are easy to overwrite or misidentify, and rendered results are difficult to reproduce.

**Required action:** Include mode and dimensions in the default filename and optionally a timestamp. Provide a sidecar JSON or another documented metadata mechanism containing the source identifier, parameters, application version, and reviewed commit/build identifier.

**Acceptance criteria:** Two exports from different modes receive distinguishable default names, and a retained metadata record can reconstruct the parameter object used for an exported image.

### [ ] UX-002 — Add explicit source-clear and render-cancel actions

**Classification:** Type: Enhancement · Severity: Low · Release gate: No · Confidence: Code-confirmed · Workstream: WS4  
**Tracking:** Status: Open · Owner role: Product + application engineering · Target: Backlog
**Dependencies:** FILE-002; RENDER-001; RENDER-002

**Evidence:** There is no way to return to the initial “No image loaded” state, and cancellation is available only indirectly by starting another render.

**Impact:** Users cannot deliberately abandon a load/render operation or clear sensitive source content from the visible application state.

**Required action:** Add explicit Clear Source and Cancel Render actions integrated with the canonical load/render lifecycle.

**Acceptance criteria:** Cancel stops the active job without changing the last successful output and announces the canceled state. Clear invalidates pending loads/renders, releases source resources, restores the initial placeholder, and disables rendering/saving until a new source is loaded.

### [ ] CODE-001 — Remove dead and misleading code

**Classification:** Type: Maintainability improvement · Severity: Low · Release gate: No · Confidence: Code-confirmed · Workstream: WS5  
**Tracking:** Status: Open · Owner role: Application architecture + rendering engineering · Target: Backlog
**Dependencies:** ARCH-001; static analysis; full regression suite

**Evidence:** Confirmed cleanup candidates include unused CSS variables `--panel` and `--danger`; unused page-scope `C.add`, `C.scale`, `sampleImage`, and `applyColorMode` after shared-worker refactoring; unused `path` import in `main.js:2`; empty `class=""` attributes; and `async function render()` despite no `await` or completion Promise.

**Impact:** Dead paths increase review effort and can cause maintainers to test or modify code that production does not execute.

**Required action:** Remove confirmed dead code after coverage or reference analysis, or document why a candidate remains required.

**Acceptance criteria:** Lint/static analysis reports no unused imports, variables, or functions in the supported build; removal does not change approved functional or visual tests.

### [ ] CODE-002 — Stop recalculating the Droste math display for unrelated controls

**Classification:** Type: Maintainability improvement · Severity: Low · Release gate: No · Confidence: Code-confirmed · Workstream: WS5  
**Tracking:** Status: Open · Owner role: Application architecture + rendering engineering · Target: Backlog
**Dependencies:** Canonical derived-state dependency model; instrumentation test

**Evidence:** `wireSlider()` calls `updateMathDisplay()` for resolution, color intensity, view scale, arbitrary-power controls, and multiplication controls (`index.html:1350-1374`).

**Impact:** Unrelated state changes trigger unnecessary DOM work and blur the dependency model for live diagnostics.

**Required action:** Define derived-state dependencies and update only the displays affected by each change, preferably through the canonical state/render pipeline.

**Acceptance criteria:** Instrumented browser tests show that unrelated controls do not invoke Droste-math recomputation, while every parameter that affects displayed math updates it exactly once per committed state change.

### [ ] WORKER-001 — Revoke the Blob URL and improve worker diagnostics

**Classification:** Type: Maintainability / diagnostics improvement · Severity: Low · Release gate: No · Confidence: Code-confirmed · Workstream: WS4  
**Tracking:** Status: Open · Owner role: Application engineering · Target: Backlog
**Dependencies:** RENDER-001/002; SEC-001 worker strategy

**Evidence:** `_workerURL` is never revoked, and generated worker stack traces do not map cleanly to a maintained source file.

**Impact:** The worker resource persists for the page lifetime and production failures are harder to diagnose.

**Required action:** Revoke obsolete Blob URLs on replacement/unload, or move to an external/module worker. Add a stable source name and source map where supported.

**Acceptance criteria:** Repeated worker replacement does not increase the count of live Blob URLs, and an intentional worker exception reports a stable source filename and actionable line information.

### [ ] UI-005 — Avoid visual-only state storage

**Classification:** Type: Architecture debt · Severity: Low · Release gate: No · Confidence: Code-confirmed · Workstream: WS1  
**Tracking:** Status: Open · Owner role: Frontend engineering · Target: Backlog
**Dependencies:** Canonical state model; STATE-002/003

**Evidence:** Output shape is inferred from `.shape-btn.active` (`index.html:621`) rather than a typed application-state value.

**Impact:** CSS classes become an implicit data store, making reset, preset, accessibility, and test behavior easier to desynchronize.

**Required action:** Store output shape and all other selectable state in one validated state object; render classes and ARIA state from that object.

**Acceptance criteria:** Removing or altering presentation classes cannot change `getParams()` output, and state-to-DOM tests verify class, label, and ARIA synchronization.

### [ ] REPO-002 — Improve change traceability

**Classification:** Type: Configuration-management control gap · Severity: Low · Release gate: No · Confidence: Code-confirmed · Workstream: WS6  
**Tracking:** Status: Open · Owner role: Project maintainer · Target: Adopt immediately for new changes
**Dependencies:** Finding/verification workflow approved for all new changes

**Evidence:** Recent commit messages such as `a` and generic “initial” entries do not identify intent, fixes, validation, or rollback boundaries.

**Impact:** Defect provenance, verification history, and safe rollback are difficult to establish.

**Required action:** Adopt issue-linked descriptive commits and retain verification evidence for mathematical and release-impacting changes. Keep correction commits independently revertible where practical.

**Acceptance criteria:** Each remediation commit references one or more finding IDs, states the validation performed, and can be reverted without unintentionally removing unrelated fixes.

### [ ] PKG-001 — Complete package metadata and publication intent

**Classification:** Type: Release metadata task · Severity: Low · Release gate: Conditional (A2) · Confidence: Code-confirmed · Workstream: WS6  
**Tracking:** Status: Open · Owner role: Release engineering · Target: Before npm publication
**Dependencies:** Approved private/public publication decision; REL-001; REPO-001

**Evidence:** Package author/maintainer, repository, bugs, homepage, engines, and explicit private/public publication intent are missing or incomplete.

**Impact:** Consumers cannot identify support channels or compatibility, and accidental npm publication remains possible.

**Required action:** Add complete metadata. Set `"private": true` unless npm publication is an approved release channel; otherwise define publish access, package contents, and provenance controls.

**Acceptance criteria:** `npm pack --dry-run` contains only approved files, package metadata resolves to maintained project locations, the supported runtime is declared, and CI prevents publication contrary to the approved private/public decision.

### [ ] PERF-002 — Avoid recreating a worker and copying the full source on every render

**Classification:** Type: Performance improvement · Severity: Low · Release gate: No · Confidence: Code-confirmed · Workstream: WS5
**Tracking:** Status: Open · Owner role: Application architecture + rendering engineering · Target: Backlog
**Dependencies:** RENDER-001 through RENDER-003; WORKER-001; approved performance budget

**Evidence:** Every render copies `srcImageData`, creates a new Blob worker, transfers the copy, and terminates the worker after completion (`index.html:985-1046`). Auto-render repeats this for each settled control change.

**Impact:** Parameter-only rerenders may incur avoidable worker-startup and source-transfer cost, but a persistent worker also adds lifecycle and cancellation complexity.

**Required action:** Measure startup/transfer cost after RENDER-001 through RENDER-003 and WORKER-001 are complete. Adopt a persistent source-caching worker only when benchmark evidence justifies the additional state model.

**Acceptance criteria:** Either (a) repeated parameter renders do not retransmit unchanged source data and all lifecycle/race tests pass, or (b) an approved benchmark record shows the current design is within the defined performance budget and the item is closed as “not justified.”

---

## Review validation baseline

The following evidence identifiers describe checks performed against `d68e78c`. They are references only until the procedures and artifacts are committed under the **Evidence-retention requirements**.

### Passed baseline checks

| Evidence ID | Check | Result |
|---|---|---|
| `EV-001` | `node --check` for `main.js` and the extracted inline script | Passed |
| `EV-002` | Duplicate HTML IDs and `getElementById` target resolution | No duplicate IDs; all referenced IDs resolved |
| `EV-003` | Headless Chromium smoke render across all nine transform modes | All modes completed without an uncaught page error |
| `EV-004` | Complex division guard | Division by zero is guarded in the reviewed implementation |
| `EV-005` | Baseline Electron renderer settings by code inspection | `nodeIntegration: false`; `contextIsolation: true` |

### Reproduced findings

| Evidence ID | Reproduction |
|---|---|
| `REP-001` | Viewport/document expansion to approximately 1,931 px at 1280×820 |
| `REP-002` | Invalid Print Gallery color selection (`selectedIndex = -1`) |
| `REP-003` | Pixel-identical Cartesian circle and square renders |
| `REP-004` | Header formula remains at `N = 256` after changing `N` |
| `REP-005` | Aspect ratio survives Reset |
| `REP-006` | Built-in generated-source edges are nonperiodic |
| `REP-007` | Bilinear sampling does not interpolate across periodic boundaries |
| `REP-008` | Angular-fold apex wraps exact `v = 1` to `v = 0` |
| `REP-009` | Standard alpha/gamma diagnostics remain visible for arbitrary `c = 0` |
| `REP-010` | Cut-slider stored value differs from the displayed special angle |
| `REP-011` | Equal numerical rotate and cut offsets produce pixel-identical output |

## Review limitations and unvalidated scope

This review did **not** establish:

- actual Electron 28 launch behavior, because the reviewed repository had no committed lockfile or installed dependency tree;
- Windows, macOS, or Linux packaged-app execution;
- installer generation, signing, notarization, or update behavior;
- Firefox or WebKit compatibility despite the standalone-browser claim;
- manual assistive-technology conformance;
- formal memory, allocation, or performance profiles;
- dependency vulnerability status;
- penetration testing or hostile-image decoder behavior;
- legal ownership or redistribution rights for bundled material.

Chromium 144 behavior is useful evidence, but it is not a substitute for testing the Chromium version embedded in the approved Electron runtime. The licensing finding is an engineering release gate, not a legal opinion.

## Controlled execution plan

| Phase | Work | Entry condition | Exit / success criterion | Rollback control |
|---:|---|---|---|---|
| **0** | Preserve baseline and contain distribution | Reviewed revision available | Tag or otherwise preserve `d68e78c`; commit this backlog/evidence plan; prevent unreviewed public packaging of third-party assets | Restore baseline tag and remove unpublished artifacts |
| **1** | Approve product and mathematical decisions | Assumptions A1–A6 reviewed | Approved dispositions for period semantics, `r2`, Cartesian boundaries, alpha, grid availability, browser support, and accessibility target | Revert decision record before dependent code merges |
| **2** | Establish quality and build controls | Decisions identified | Lockfile/runtime matrix, CI, test harness, fixtures, evidence retention, and one failing regression test per first-batch defect | Revert isolated tooling commits; retain baseline evidence |
| **3** | Implement canonical state and lifecycle | Phase 2 tests active | Deterministic state, presets/reset, load IDs, render IDs, cancellation, explicit render state, and safe Save gating | Small issue-linked commits; single-commit revert per behavior |
| **4** | Correct sampling and mathematical core | State/lifecycle stable | One production implementation of transforms and boundary policies; approved golden changes; diagnostics derived from active map | Revert by finding/workstream; restore prior approved goldens |
| **5** | Correct grid, layout, accessibility, and file policy | Core semantics stable | Viewport and responsive matrices pass; grid is correct or unavailable by design; input/resource and accessibility tests pass | Feature flags or scoped reverts for grid/input/UI changes |
| **6** | Update documentation and release controls | Functional acceptance complete | Documentation matches implementation; only approved assets package; intended artifacts build and smoke-test | Withdraw release artifacts and revert release-config commit |
| **7** | Optimize | Correctness baselines approved | Benchmarks meet declared thresholds without unapproved output changes | Revert optimization commit; preserve correctness baseline |

For every functional correction: add or identify the failing test, implement one scoped change, retain passing evidence, update the finding status, and preserve a direct rollback path. Mathematical changes that intentionally alter output require explicit golden-baseline approval rather than silent hash replacement.
