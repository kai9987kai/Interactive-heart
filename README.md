# Dr. Cardio Pro Evolved v4.0 — Offline Cardiovascular Simulation Laboratory

**Release date:** 22 November 2026  
**Package:** one self-contained HTML application, with optional inspectable build sources and regression checks.

## Quick start

1. Open `Dr_Cardio_Pro_Evolved_v4_OFFLINE.html` in a current version of Chrome, Edge or Firefox. **Do not extract or install any dependencies.**
2. Select **Animations On**, then **Start Heart** and **Show Flow** to watch the pulsating heart, moving red/blue circulation particles and ECG signal.
3. Choose any of the 21 learning modes from the menu. On mobile, scroll past the heart to the menu and learning panels.
4. Select **PV Loop** to explore the pressure–volume model or **Pulse** to explore the arterial Windkessel model.
5. In **Data**, export your backup before clearing browser storage or moving to another device. Browser storage may be scoped differently depending on how the HTML file is opened.

This product is **educational software, not a medical device**, and does not interpret patient data or provide clinical advice. In the UK, for a suspected emergency call **999**.

## Functional changes since v3.1

- **All 19 existing learning modes are retained.** They are Explore, Flow, ECG, Cycle, Vitals, Sounds, Labels, CPR, LE8, Risk, Meds, Cases, Quiz, Notes, 999, Research, Dynamics, Conduction and Data.
- **Two new modes**: an animated pressure–volume loop laboratory and a dynamic arterial-pulse laboratory, making **21 modes** in total.
- **The entire interface is bundled offline**: core UI, styles, icons, the heart animation, the ECG monitor, the existing quizzes and study features, and the new mathematical models can load without external script requests. This is a genuine improvement over v3.1, whose full React UI depended on online CDNs and only had an offline heartbeat fallback.
- **Preserved heart animation** including start/stop, animated red/blue SVG path-following blood particles, 40–180 BPM adjustment, coronary/electrical overlays, SVG structure selection and high-contrast controls.
- **Updated icon pack**: the former Lucide CDN icons have been substituted by bundled Font Awesome Free SVG assets for offline reliability. Some icon shapes therefore differ from v3.1.
- **Compatibility with prior progress**: the existing storage keys remain; new models introduce two additional keys, `dr-cardio-v4-pv` and `dr-cardio-v4-arterial`. Data backup includes these. A compatibility fix evaluates function-valued defaults correctly.
- **Mobile layout tested**, without horizontal document overflow at a 390px viewport.

### Offline boundaries

Core app: no network calls on startup. The **optional Google Gemini tutor and remote text-to-speech still require internet connectivity, a valid API key and currently supported Google model access**. The built-in browser speech synthesizer is retained as a fallback. Clicking external research links also requires a connection.

The previously available Gemini key persistence mechanism remains for backward compatibility. It stores the credential in browser `localStorage`, which is not a secure credential vault; do not enter secrets on untrusted or shared devices. Data backups exclude the key unless you explicitly opt in.

## New physiology models

### 1. Pressure–volume loop (PV Loop)

This **synthetic, lumped-parameter teaching model** varies end-diastolic volume (EDV), end-systolic elastance (Ees), effective arterial elastance (Ea), heart rate and vascular resistance/compliance. It derives end-systolic volume (ESV) from an intentionally simplified ventricular–arterial coupling:

`ESV = (Ea * EDV + Ees * V0) / (Ees + Ea)` with `V0 = 10 mL`.

`SV = EDV - ESV`; `EF = 100 * SV / EDV`; `CO = BPM * SV / 1000` L/min.

The phased loop approximates isovolumic contraction, ejection, isovolumic relaxation and filling. The graph uses auto-scaled axes. Controls provide baseline/exercise/low-filling/high-afterload scenarios, A/B comparisons, animated cardiac phase and CSV export. **This is not an identified patient model or validated pressure–volume solver.** In particular, its chamber-pressure trajectory is imposed phenomenologically and it omits valve mechanics, reflex regulation, right-heart coupling and oxygen transport.

### 2. Windkessel arterial pulse (Pulse)

An explicit, two-element RC model integrates a synthetic inflow pulse:

`dP/dt = (Q_in - (P - P_venous)/R) / C` with `P_venous = 5 mmHg`.

The simulation uses 240 time steps per beat and 15 warm-up cycles. It displays arterial pressure and aortic inflow over one beat and synthetic systolic/diastolic/mean pressures. It does not include reflected pressure waves, wave travel, viscoelastic walls, baroreflexes, or measured blood pressure. **R, C and Ea are simplified independent teaching inputs**, not a calibrated vascular model.

Both laboratories show an explicit **model validity warning** when extreme combinations produce nonphysiological or implausible outputs. Results are solely *illustrative* and must never be used for clinical decisions.

For the default settings (70 bpm, EDV 120 mL, Ees 2.5 mmHg/mL, Ea 1.45 mmHg/mL, R 1.02 mmHg·s/mL, C 1.6 mL/mmHg), the current implementation calculates approximately:

| Synthetic model value | Result |
|---|---:|
| Stroke volume | 69.62 mL |
| Cardiac output | 4.87 L/min |
| Ejection fraction | 58.02% |
| End-systolic pressure | 100.95 mmHg |
| Windkessel peak pressure | 103.70 mmHg |
| Windkessel minimum pressure | 72.69 mmHg |
| Windkessel mean pressure | 87.51 mmHg |

These are calculated *model outputs*, **not reference human measurements**.

## Engineering implementation

The distributable HTML file bundles React 16.0.0, ReactDOM 16.0.1, a lightweight wrapper that adapts React Hook calls to the available local class-component runtime, pre-generated Tailwind CSS 4.1.10 styles, and a local Font Awesome icon set. The JSX source is precompiled, removing Babel-on-load. The resulting HTML is under 400 KB uncompressed.

The compatibility hook adapter deliberately supports the hooks used by this app: `useState`, `useEffect`, `useMemo`, and `useRef`. It is not intended to reproduce every behaviour of modern React. A future migration to a bundled modern React release, with a reproducible package-lock and continuous browser tests, would be preferable for long-term maintenance. **No claim is made that replacing the original React 18 CDN runtime with this bundled React 16-based compatibility layer is risk-free.**

### In the optional source package

- `cardio_v4_source.jsx`: all the application mode implementations in JSX form after conversion, including the new model.
- `cardio_v4_components.txt`: the new model components and formulae, in isolation.
- `cardio_hooks_compat.js`: the offline React Hook compatibility adapter.
- `test_cardio_v4_extended.py`: a Playwright-based regression script.
- `Dr_Cardio_Pro_Evolved_v3_1_FIXED.html`: the preceding version, retained for reference.

The supplied developer build script is specific to the preinstalled build environment and may require editing and npm dependencies when run elsewhere. For end users, **the HTML itself requires no build step**.

## Validation performed

Executed in headless Chromium on 22 November 2026 with all external requests blocked. The isolated testing environment blocks `file://`/HTTP navigation, so the test uses `page.set_content()` with a small `localStorage` test stand-in to verify saved-state compatibility. This is a **real browser DOM/animation test**, but not a substitute for a device acceptance test of persistent storage on your own Windows browser.

- JSX transpilation: **zero diagnostics**; application script and injected assets compile and run.
- All **21 modes** successfully open without JavaScript exceptions, including the 19 carried over from v3.1.
- Offline app startup: **no external HTTP requests**; full UI mounted, no fallback required.
- Live blood-flow `animateMotion` particles: **eight in full UI, verified visibly moving** in Chromium.
- BPM changes alter animation duration; toggling flow removes/restores particle components.
- Heart start/stop toggles ECG playback status.
- Reduced-motion initially disables animation when appropriate, while **explicit user opt-in enables playback**; verified by particle position change.
- Existing saved BPM and rhythm values restored using simulated prior-version localStorage entries.
- Both new simulation modes render and respond to their sliders; model consistency checks pass; comparison overlay renders.
- Parameter extremes are finite and model validity warnings appear for extreme settings; graphs auto-scale.
- Existing Data diagnostics still report internally passing checks; Quiz controls still render and are interactive.
- At 390px viewport, no overall horizontal overflow. Desktop screenshots were manually inspected.

**Not fully covered:** all per-control interactions in every legacy mode, actual persistent `file://` storage on a user device, all browser engines, Google API key/model availability, offline voices, heavy memory/performance benchmarking, clinical validity, and long-duration testing. Therefore this release is a major tested improvement, **not a mathematical guarantee of zero regressions**.

## Primary technical and medical references

- Resuscitation Council UK (2025), [Adult Basic Life Support Guidelines](https://www.resus.org.uk/professional-library/2025-resuscitation-guidelines/adult-basic-life-support-guidelines). Rate recommendation for adult CPR: 100–120 compressions/min.
- [Clinical Applications of Patient-Specific Models: The Case for a Simple Approach](https://pmc.ncbi.nlm.nih.gov/articles/PMC5910244/) — time-varying elastance and pressure–volume models. The application **does not implement this paper's validated patient-specific methods**.
- [Dynamic Estimation of Cardiovascular State From Arterial Blood Pressure Recordings](https://pmc.ncbi.nlm.nih.gov/articles/PMC11771135/) — Windkessel modelling. The app implements a deliberately simplified teaching version.
- [American Heart Association — Life's Essential 8](https://www.heart.org/en/healthy-living/healthy-lifestyle/lifes-essential-8).
- [NHS — Heart attack](https://www.nhs.uk/conditions/heart-attack/).

## Attributions and licences

- **Font Awesome Free icons**, © Fonticons, Inc., licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). Source: [Font Awesome](https://fontawesome.com/license/free). The packaged SVG data is extracted from the freely distributed icon assets; shapes are unchanged but the packaging differs.
- **Tailwind CSS 4.1.10** by Tailwind Labs, MIT licence. Utility CSS is pre-generated and embedded.
- **React 16.0.0 / ReactDOM 16.0.1** by Meta/Facebook and contributors, open-source React licence. These are bundled from the build environment to make the app standalone.

No fonts are distributed separately.
