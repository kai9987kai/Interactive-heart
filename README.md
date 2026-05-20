# Dr. Cardio Pro — Interactive Heart Learning Lab

**Dr. Cardio Pro** is a single-file, browser-based cardiovascular education app for exploring heart anatomy, blood flow, ECG concepts, CPR practice timing, prevention habits, and clinical reasoning prompts.

It keeps the original **Dr. Cardio** experience — animated heart diagram, clickable anatomy, heartbeat controls, blood-flow particles, BPM slider, ECG canvas, AI pathology explanations, quiz mode, and speech/TTS support — while expanding it into a more advanced learning lab with additional overlays, guided tools, practice challenges, and safety education.

> Educational use only. This project does **not** diagnose, treat, or replace medical advice. For urgent symptoms such as severe chest pain, collapse, severe breathing difficulty, or blue/grey lips or skin, seek emergency help immediately.

---

## Preview

Open the HTML file directly in a modern browser:

```text
dr-cardio-pro-ultra-fixed.html
```

No build step is required.

---

## Core Features Preserved from the Original

- **Single-file HTML app** using React, Tailwind CSS, Babel, and CDN imports
- **Interactive SVG heart diagram** with clickable anatomical structures
- **Start/Stop Heart** heartbeat animation
- **Show/Hide Flow** animated oxygenated/deoxygenated blood-flow particles
- **BPM slider** from slow to fast heart-rate simulation
- **Live ECG canvas monitor** with animated waveform output
- **Explore mode** with anatomy descriptions and circulation details
- **AI pathology explainer** for selected heart structures
- **Quiz mode** with AI-generated or fallback anatomy questions
- **Speech/TTS support** for reading descriptions and explanations aloud
- **Dark medical-dashboard interface** with responsive layout

---

## New Advanced Tools and Panels

### 1. Expanded Anatomy Model

The app now includes more than the original chambers and major vessels:

- Superior vena cava
- Inferior vena cava
- Right atrium
- Tricuspid valve
- Right ventricle
- Pulmonary valve
- Pulmonary artery
- Pulmonary veins
- Left atrium
- Mitral valve
- Left ventricle
- Aortic valve
- Aorta
- Coronary arteries
- SA node
- AV node
- Bundle branches

Each structure includes:

- Plain-English name
- Anatomical description
- Blood oxygenation state
- Structure type
- Learning check prompt
- Built-in fallback pathology notes

### 2. Visual Overlays

Toggle extra learning layers on the diagram:

- **Coronary artery overlay**
- **Electrical conduction overlay**
- **High-contrast accessibility mode**
- **Reduced-motion friendly styling support**

### 3. Guided Blood-Flow Journey

A step-by-step flow trainer walks learners through the route:

```text
Body → vena cava → right atrium → right ventricle → pulmonary artery → lungs → pulmonary veins → left atrium → left ventricle → aorta → body
```

Useful for revision, classroom demonstrations, and active recall.

### 4. ECG Rhythm Explorer

The ECG panel supports demo rhythm presets:

- Normal sinus rhythm
- Bradycardia demo
- Tachycardia demo
- Irregular rhythm demo

These are synthetic educational waveforms, not diagnostic ECG traces.

### 5. Cardiac Cycle Timeline

Explains the mechanical sequence of the heartbeat:

- Atrial filling
- Atrial contraction
- Ventricular filling
- Isovolumetric contraction
- Ventricular ejection
- Isovolumetric relaxation

### 6. Vitals Response Lab

Scenario-based explanations show how heart rate, blood pressure, oxygen demand, and workload can shift during common situations such as:

- Rest
- Exercise
- Stress
- Dehydration
- Blood loss concept demo
- Fever concept demo

### 7. Heart Sound Lab

Synthetic audio demos help learners connect timing and valve events:

- Normal S1/S2 concept
- Faster rhythm concept
- Murmur concept demo

These are simple educational tones, not real diagnostic auscultation recordings.

### 8. CPR Metronome Trainer

A practice tool for timing compressions:

- 100–120 compressions/minute practice target
- Tap/beat feedback
- 2-minute rescuer-rotation reminder concept
- AED/emergency action reminders

### 9. Life's Essential 8 Prevention Lab

A non-diagnostic prevention checklist based on major cardiovascular health categories:

- Eat better
- Be active
- Avoid nicotine
- Healthy sleep
- Healthy weight
- Blood lipids
- Blood glucose
- Blood pressure

### 10. Risk Factor Mapper

A simple, non-diagnostic teaching map for common cardiovascular risk levers:

- High blood pressure
- High LDL / unhealthy lipids
- Diabetes or high glucose
- Smoking or nicotine exposure
- Poor sleep
- Low physical activity
- Family history
- Older age

This is **not** QRISK, SCORE2, or a personal risk calculator.

### 11. Medication Mechanism Cards

Plain-English mechanism cards for common cardiovascular medicine groups:

- Statins
- ACE inhibitors / ARBs
- Beta blockers
- Diuretics
- Antiplatelets / anticoagulants

Includes monitoring considerations and “not for” cautions.

### 12. Triage Case Cards

Scenario cards encourage safe reasoning about symptoms and urgency, including:

- Chest pressure after exertion
- Palpitations after stimulants
- Breathlessness lying flat with swollen ankles
- Collapse with abnormal breathing

### 13. Label Challenge

A quick identification game that lets learners select the matching structure on the diagram and practise active recall.

### 14. Notes, Flashcards, Import, and Export

Learners can build their own revision notes and export/import progress using JSON.

---

## AI Features

The app can work with or without an API key.

### Without an API key

The app uses built-in local fallback content for:

- Anatomy descriptions
- Pathology notes
- Quiz-style prompts
- Learning checks
- Speech via browser speech synthesis where available

### With a Gemini API key

Add a Gemini API key inside the app settings field to enable:

- AI-generated pathology explanations
- AI answers to heart-anatomy questions
- AI-generated quiz questions
- Gemini TTS audio where supported

The app currently references:

```js
const MODEL_TEXT = "gemini-2.5-flash";
const MODEL_TTS = "gemini-2.5-flash-preview-tts";
```

Do not commit private API keys to a public repository.

---

## Tech Stack

- **HTML5**
- **React 18.2.0** via CDN
- **ReactDOM 18.2.0** via CDN
- **Tailwind CSS** via CDN
- **Babel Standalone** for in-browser JSX
- **Lucide React** icons pinned to React 18 dependencies
- **SVG** for the anatomy diagram
- **Canvas API** for ECG rendering
- **Web Audio API** for synthetic heart sounds and metronome tones
- **SpeechSynthesis API** fallback for spoken explanations
- **LocalStorage** for settings/progress persistence

---

## Important React CDN Fix

The upgraded file pins React-dependent packages to React 18.2.0 to avoid the runtime issue:

```text
Minified React error #31
```

The import pattern is:

```js
import React, { useEffect, useMemo, useRef, useState } from 'https://esm.sh/react@18.2.0?dev';
import ReactDOM from 'https://esm.sh/react-dom@18.2.0/client?deps=react@18.2.0&dev';
import { Heart, Activity } from 'https://esm.sh/lucide-react@0.468.0?deps=react@18.2.0';
```

This prevents mixed React 18/19 element-symbol conflicts from CDN dependency resolution.

---

## Getting Started

### Option 1 — Open Locally

Download the HTML file and open it in a browser:

```bash
open dr-cardio-pro-ultra-fixed.html
```

Or double-click the file.

### Option 2 — Run with a Local Static Server

This is recommended when testing API calls or browser permissions:

```bash
python3 -m http.server 8080
```

Then visit:

```text
http://localhost:8080/dr-cardio-pro-ultra-fixed.html
```

### Option 3 — Deploy to GitHub Pages

1. Add the HTML file to your repository.
2. Rename it to `index.html` if you want it to be the homepage.
3. Commit and push.
4. Enable GitHub Pages in repository settings.

---

## Suggested Repository Structure

```text
.
├── index.html
├── README.md
└── LICENSE
```

For a larger version later:

```text
.
├── index.html
├── README.md
├── LICENSE
├── assets/
│   ├── screenshots/
│   └── icons/
└── docs/
    ├── education-notes.md
    ├── safety-disclaimer.md
    └── roadmap.md
```

---

## Accessibility

Current accessibility improvements include:

- Keyboard-visible focus rings
- High-contrast mode
- Responsive layout
- Reduced-motion support in CSS
- Clearer button labels
- Plain-language educational copy
- Speech/TTS support where available

Planned accessibility upgrades:

- ARIA-labelled SVG regions
- Full keyboard diagram navigation
- Captions/transcripts for sound demos
- Colour-blind-safe palette toggle
- Larger text mode

---

## Safety and Medical Disclaimer

This project is for **education, revision, and demonstration only**.

It does not provide:

- Diagnosis
- Personal risk scoring
- Emergency triage decisions
- Treatment instructions
- Medication advice for an individual
- Replacement for a clinician, NHS 111, 999, GP, pharmacist, or emergency service

Emergency symptoms should be handled through appropriate local emergency services.

---

## Browser Support

Recommended:

- Chrome / Chromium
- Edge
- Safari
- Firefox

Some features depend on browser support:

- Speech synthesis availability varies by browser/device.
- Web Audio may require a user gesture before playing sounds.
- External CDN imports require internet access.
- Gemini API tools require a valid API key and network access.

---

## Roadmap

Planned improvements:

- More accurate SVG anatomy proportions
- ARIA-labelled anatomical regions
- Teacher/classroom mode
- Student progress export bundle
- Printable worksheet generator
- More quiz categories by difficulty
- Multi-language mode
- Offline-first service worker
- IndexedDB note storage
- Screenshot/export-to-PNG tool
- PWA install support
- Optional real citation panel for educational claims
- More rhythm concepts with clearer safety warnings
- Modular version using Vite/React for maintainability

---

## Development Notes

This is intentionally a **single-file prototype** for easy sharing and deployment.

For long-term maintenance, consider migrating to:

- Vite
- TypeScript
- Component-based file structure
- Unit tests
- ESLint/Prettier
- Playwright browser smoke tests
- Versioned educational content files

---

## Contributing Ideas

Good contribution areas:

- Better SVG anatomy labels
- Accessibility improvements
- Additional learning activities
- More accurate heart sound education
- Safer clinical wording
- Classroom worksheet exports
- Mobile layout refinements
- Offline/PWA support

Please keep all medical content educational, cautious, and non-diagnostic.

---

## License

Add your preferred license here.

Suggested options:

- MIT for open-source reuse
- CC BY-NC for educational content reuse with attribution
- Custom license if you want to restrict clinical/commercial use

---

## Credits

Built as an advanced educational upgrade to the original **Dr. Cardio** interactive heart diagram.

Uses:

- React
- Tailwind CSS
- Lucide icons
- Browser Canvas API
- Browser Web Audio API
- Browser SpeechSynthesis API
- Optional Gemini API integration
