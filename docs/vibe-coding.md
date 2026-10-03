# Reproducing the game with vibe coding

Companion guide to the [main README](../README.md). This is the teaching pack for the lesson:
why the game is designed the way it is, how it was actually built with an AI coding tool, and the
complete prompt to hand to one.

The guide assumes "vibe coding" — building software by describing intent in natural language,
iterating conversationally, and inspecting what comes back. For an education audience this is the
point: a teacher or student can prototype a usable learning tool without deep programming
expertise, then read, critique and extend the generated code.

**Last verified: 3 October 2026** using OpenCode, and against the deployed page at
<https://drhycheung.github.io/MathInvaders/>.

## Contents

1. [Design thinking: from an arithmetic drill to a game students return to](#1-design-thinking-from-an-arithmetic-drill-to-a-game-students-return-to)
2. [How the game was built](#2-how-the-game-was-built)
3. [Further work for students](#3-further-work-for-students)
4. [The reproduction prompt](#4-the-reproduction-prompt) ← jump here if you just want to build it

---

## 1. Design thinking: from an arithmetic drill to a game students return to

The project follows the Stanford d.school design-thinking model — empathise, define, ideate,
prototype, test — applied to one problem: students do not practise arithmetic enough, because
drilling feels like a chore.

| Stage | This project's arc |
|---|---|
| **1. Empathise 同理心** | Many students find repetitive arithmetic drills boring and demotivating. They may disengage, rush through exercises, or avoid practice entirely. Observation: games often hold their attention far longer than worksheets. |
| **2. Define 定義** | **Problem statement:** *students lack motivation to practise arithmetic regularly.* **Design goal:** create an engaging, low-barrier experience that encourages repeated practice without it feeling like a drill. Success criterion: students willingly return for "one more round". |
| **3. Ideate 構思** | Options considered: digital flashcards, quizzes with badges, timed challenges, role-playing games. The Space Invaders format was chosen because it is instantly recognisable, has a clear goal (shoot the target), creates gentle time pressure, and maps naturally onto "select the correct answer". |
| **4. Prototype 原型** | A single-file HTML5 Canvas game: a math-problem generator, descending aliens carrying answer choices, collision detection, scoring and lives, level progression, keyboard and touch controls, and a hand-gesture mode via MediaPipe Hands. Kept self-contained for easy sharing. |
| **5. Test 測試** | Tested locally and on mobile. Iterated on the difficulty curve, UI readability, mobile control layout and feedback clarity. Hand-tracking mode was added to spark discussion about accessibility and alternative inputs. |

The measurable outcome was **repeated voluntary practice**: a student should be able to start a
round within seconds, see immediately whether an answer was right, and want to play again.
Motivation is treated as the outcome to be designed for, not as an assumption about students.

### Context: why gamification, and where this project fits

- **Game-based learning** leverages the motivational pull of games — challenge, autonomy, feedback
  and progression.
- **Cognitive load:** arithmetic practice is embedded in a task where maths is necessary to
  progress, rather than being an isolated worksheet item.
- **Immediate feedback:** players know instantly whether they shot the right alien, which
  reinforces correct reasoning.
- **Low stakes, high repetition:** failure is part of the game, which reduces anxiety compared with
  graded drills.
- **Transferable design:** the "problem + multiple choices + timed action" pattern can be adapted
  to other subjects (vocabulary, science facts, and so on).

---

## 2. How the game was built

The game was built with an AI coding tool and iterated in the browser, with each claim checked
before it was accepted. The prompt in [Part 4](#4-the-reproduction-prompt) encodes the findings
below, so that a working game should be produced on the first attempt.

1. **Problem statement first:** "Build a Space Invaders-style game where students shoot the alien
   with the correct math answer."
2. **Core mechanics:** specified the canvas, sprites, descending aliens, math-problem display,
   collision detection, scoring, lives and levels.
3. **Input modes:** requested keyboard, touch (mobile) and hand-gesture control (MediaPipe Hands).
4. **UX polish:** added the pixel-art style, HUD, final screen and difficulty progression.
5. **Single-file constraint:** requested everything inline (HTML/CSS/JS) for GitHub Pages
   deployment.
6. **Testing and refinement:** ran the game in a browser, then identified and fixed issues such as
   mobile scaling and gesture responsiveness.
7. **Documentation:** generated the README and this guide to make the game classroom-ready.

The central lesson is that **the quality of the output depends on the quality of the prompt**.
Being explicit about the constraints — single file, no build step, CDN libraries, gameplay rules —
prevents most common pitfalls.

### Bugs that measurement caught and looking did not

- **The game looked finished only because the machine was online.** Unlike the other teaching
  demos in this series, which snapshot their stylesheet into the file, MathInvaders loads
  everything from a CDN: Tailwind from `cdn.tailwindcss.com`, four MediaPipe scripts from
  jsDelivr, and the Press Start 2P font from Google Fonts (see `index.html`, `<head>`). On a
  connected machine the game renders and plays correctly, so nothing appears wrong. Opened offline
  or on a filtered network, the HUD loses its styling and hand-tracking never initialises, while
  the game loop still starts — the failure is partial, not a crash, which is what makes it easy to
  miss. Confirm it by loading the page with all non-document requests blocked: the canvas appears,
  the overlays are unstyled, and camera mode stays at `CAMERA: ERROR/DENIED`.

> [!IMPORTANT]
> This is the pedagogical heart of the lesson. The fault produces no error message and a page that
> looks complete; only someone who tests under a different network condition will find it. The same
> trap applies to camera permission — the gesture path can be denied silently, so the code must
> surface the state (as this game does in its camera-status readout) rather than assume success.

---

## 3. Further work for students

This project is deliberately **not** a research contribution. Gamified arithmetic practice is a
well-established area, and it is presented here as a teaching baseline, not as an evaluation of
learning gains.

Students are encouraged to extend it, or to build something adjacent — a different subject,
age group or interaction mode — so that their work addresses a question that is genuinely not yet
answered. The limitations in the [main README](../README.md#5-known-limitations) suggest several
directions; the most direct are to calibrate the difficulty curve against real student performance,
to add an adaptive problem generator, and to add accessibility alternatives for the purely visual
game state.

---

## 4. The reproduction prompt

Copy and paste this entire prompt into your preferred AI coding assistant (e.g. Claude, Gemini,
OpenCode, ChatGPT). It encodes the design rationale, constraints and requirements to reproduce
Math Invaders.

```text
Build a complete, standalone, single-file HTML page (all CSS/JS inline, native ES6 only, no frameworks, no build step) for "Math Invaders", a gamified arithmetic practice game deployable on GitHub Pages.

## Problem statement (context)
The goal is to address students' lack of motivation for practising arithmetic. Turn repetitive drills into an engaging arcade experience.

## Core gameplay
- Retro Space Invaders style: player controls a cannon at bottom; aliens descend in waves.
- A math problem appears at the bottom of the screen (e.g. "5 + 3 = ?" or "12 ÷ 4 = ?"). 
- Each alien carries a different answer value.
- Player must shoot the alien carrying the CORRECT answer to score points and progress.
- Shooting wrong alien or letting aliens pass reduces health/score.
- Difficulty increases across levels (faster movement, more aliens, adjusted spawn rates).
- Track score, level, lives/health. Show final result screen when game ends.
- Include a "Start", "Restart", and clear HUD showing current problem, score, level, health.

## Visual/style
- Pixel-art look, classic arcade feel.
- Use HTML5 Canvas for rendering.
- Readable HUD text with text shadow.
- Clean layout that works on desktop and mobile.

## Input controls
1. Keyboard: Arrow keys to move left/right, Space to shoot.
2. Touch: On-screen left/right/shoot buttons for mobile devices.
3. Hand gesture (webcam): Use MediaPipe Hands (load from CDN: https://cdn.jsdelivr.net/npm/@mediapipe/hands). 
   - Move cannon horizontally by tracking hand position (e.g. index finger tip x mapped to canvas).
   - Shoot by raising/gesturing (e.g. extend index finger or quick upward motion). Keep it intuitive and responsive.
   - Include UI toggle to enable/disable hand tracking; request camera permission only when enabled.
   - Gracefully handle permission denial/camera errors.

## Technical constraints
- Single file: index.html with inline <style> and <script>.
- Vanilla JavaScript (ES6), no npm, no bundlers, no TypeScript.
- Tailwind CSS via CDN for UI overlays/buttons (optional but fine): https://cdn.tailwindcss.com.
- MediaPipe Hands via CDN as above.
- Must work when opened directly (file://) and when served over http(s).
- Mobile responsive: scale touch controls and text appropriately.
- No external image files required; use simple drawn shapes or minimal inline assets if any.
- Include clear comments in code explaining key logic (game loop, collision, math generation).

## Math generation
- Generate random arithmetic problems appropriate for basic practice (addition/subtraction/multiplication/division). 
- Avoid negative answers where confusing; for division, prefer integer results.
- Generate plausible wrong answers (close but incorrect) to avoid trivial guessing.
- Show the expression clearly in the HUD (e.g. "Solve: 7 × 8 = ?").

## Implementation details
- Game loop using requestAnimationFrame.
- Collision detection between bullets and aliens.
- Wave management: spawn aliens with random x positions, descend.
- State management: start/menu, playing, game over.
- Prevent default on arrow/space keys.
- Ensure touch controls don't interfere with canvas.

## Deliverables
Return the complete, final code for index.html ready to run and deploy to GitHub Pages. Include the full file content.
```

---

Back to the [main README](../README.md).
