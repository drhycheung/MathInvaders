# Reproducing Math Invaders with vibe coding

Companion guide to the [main README](../README.md). This is a teaching resource for demonstrating how design thinking and AI-assisted "vibe coding" can be used to address an educational problem: students lack motivation for practising arithmetic.

**Target audience:** Pre-service/in-service teachers exploring EdTech, game-based learning and AI coding tools.

---

## 1. Design thinking: from problem to solution

The project follows the Stanford d.school design thinking model: empathise, define, ideate, prototype, test.

| Stage | Application to Math Invaders |
|---|---|
| **1. Empathise 同理心** | Many students find repetitive arithmetic drills boring and demotivating. They may disengage, rush through exercises, or avoid practice entirely. Observation: games often hold their attention far longer than worksheets. |
| **2. Define 定義** | **Problem statement:** *Students lack motivation to practise arithmetic regularly.* **Design goal:** Create an engaging, low-barrier experience that encourages repeated practice of arithmetic without feeling like a drill. Success criterion: students willingly return for "one more round". |
| **3. Ideate 構思** | Considered approaches: digital flashcards, quizzes with badges, timed challenges, role-playing games. Chose a Space Invaders clone because it's instantly recognisable, has a clear goal (shoot target), creates gentle time pressure, and maps naturally to "select the correct answer". |
| **4. Prototype 原型** | Built a single-file HTML5 Canvas game with: math problem generator, descending aliens with answer choices, collision detection, scoring/lives, level progression, keyboard/touch controls, and hand-gesture mode via MediaPipe Hands. Kept it self-contained for easy sharing. |
| **5. Test 測試** | Tested locally and on mobile. Iterated on: difficulty curve, UI readability, mobile controls layout, and feedback clarity. Hand-tracking mode was added to spark discussion about accessibility/alternative inputs. |

### Pedagogical rationale

- **Game-based learning:** Leverages the motivational pull of games (challenge, autonomy, feedback, progression).
- **Cognitive load:** Embeds arithmetic practice in a task where math is necessary to progress, not an isolated worksheet item.
- **Immediate feedback:** Players know instantly if they shot the right alien, reinforcing correct reasoning.
- **Low stakes, high repetition:** Failure is part of gameplay, reducing anxiety compared to graded drills.
- **Transferable design:** The "problem + multiple choices + timed action" pattern can be adapted to other subjects (vocabulary, science facts, etc.).

---

## 2. What is "vibe coding"?

"Vibe coding" refers to using AI coding assistants to build software by describing intent in natural language, iterating conversationally, and accepting/rejecting suggestions. It emphasises:
- **Idea-first:** Focus on the user/problem and desired experience, not syntax details.
- **Rapid prototyping:** Go from concept to playable demo quickly.
- **Iterative refinement:** Test, spot issues, prompt adjustments.
- **Learning by doing:** Inspect generated code to understand how it works.

For educational contexts, vibe coding democratises creation: teachers and students can prototype EdTech tools without deep programming expertise, then critique and extend the code.

---

## 3. How this project was built with AI

This demo was created by describing the desired experience to an AI coding tool and iterating. The process mirrors design thinking:

1. **Problem statement first:** "Build a Space Invaders-style game where students shoot the alien with the correct math answer."
2. **Core mechanics:** Specified canvas, sprites, descending aliens, math problem display, collision detection, scoring, lives, levels.
3. **Input modes:** Requested keyboard, touch (mobile), and hand-gesture control (MediaPipe Hands).
4. **UX polish:** Added pixel-art style, HUD, final screen, difficulty progression.
5. **Single-file constraint:** Requested everything inline (HTML/CSS/JS) for GitHub Pages deployment.
6. **Testing & refinement:** Ran in browser, identified issues (e.g. scaling on mobile, gesture responsiveness), prompted fixes.
7. **Documentation:** Generated README and this guide to make it classroom-ready.

Key lesson: **The quality of output depends on the quality of the prompt.** Being explicit about constraints (single file, no build, CDN libraries, gameplay rules) prevents common pitfalls.

---

## 4. Reproduction prompt

Copy and paste this entire prompt into your preferred AI coding assistant (e.g. Claude, Gemini, OpenCode, ChatGPT). It encodes the design rationale, constraints and requirements to reproduce Math Invaders.

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