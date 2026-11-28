# AGENTS.md — sweet-swap-adventure

## Required Flowbeacon Arcade Quality Rules

This game belongs to Flowbeacon Arcade but is developed in an **independent** GitHub repository. **Read and follow the shared standard** before implementing or declaring any update complete:
https://github.com/flowbeacon-labs/flowbeacon-arcade/blob/main/docs/GAME_QUALITY_STANDARD.md

### iPhone Safari interaction — release blocker

- **No context menu, text-selection callouts, copy/share links, hover-only controls or unwanted page scrolling** when a player holds or uses any movement, joystick, jump, fire, throttle, pause, camera, menu or other game-control surface.
- Apply scoped `-webkit-touch-callout:none`, `-webkit-user-select:none`, `user-select:none`, and `-webkit-tap-highlight-color:transparent` to the control subtree; use `touch-action:none` on held/drag controls and `touch-action:manipulation` on ordinary tap controls. **Do not apply global blocks to body or form/navigation controls.**
- Use Pointer Events and `preventDefault` for game gestures; prevent `contextmenu` and `selectstart` on game controls only. Release state on `pointerup`, `pointercancel`, `lostpointercapture`, `blur`, and visibility changes. Support simultaneous touch controls.
- Holding actions must remain active until released without repeatedly toggling single-action buttons. Keep working desktop keyboard/mouse controls.
- Icon-only buttons need `aria-label`, >=44x44 CSS px touch targets where practical, visible focus and a Help/tooltip legend. Update ARIA/state rather than replacing SVG icons with text.

### Rendering, layout and gameplay integrity

- Test phone portrait and landscape plus desktop widths of 375, 590, 768 and 1280 px. HUD/buttons must not overlap, clip or obscure the central game area; respect iPhone safe-area insets.
- Preserve existing gameplay, levels, scores, saved data, sounds, navigation, responsive layout and startup when extending the game.
- Browser game must launch and remain playable, not just pass syntax; report errors visibly.
- For WebGL/canvas games, validate shader compilation/linking, finite camera transforms, visible player/terrain and context loss. Do not assume mock GPU tests prove real rendering.
- Be cost-conscious; prefer static GitHub Pages, vanilla web tech and no mandatory paid dependencies.

### Test-and-release requirements

1. Read existing code, README and tests; create a minimal change with a regression test that reproduces the user's issue.
2. Verify hold + release + canceled touch and long-press (>1.5 s) without Safari callouts; test multitouch and background/resume.
3. Validate start/play/pause/resume/restart/navigation and look for JavaScript errors.
4. Inspect responsive bounds and overlap at 375/590/768/1280 px.
5. Execute actual browser tests when available, not only mocked DOM/WebGL. Use real iPhone Safari before claiming iPhone tested. If not available say **physical iPhone Safari QA pending**.
6. Confirm GitHub Actions result and actual GitHub Pages deployment; report exact test results and untested cases.

### Never repeat these known defects

- iPhone long-press popup on game controls
- Lost or stuck touch input after finger release or interruptions
- Overlapping controls, mission text, HUD or buttons on mobile/desktop
- Broken Start Game button, invisible scene/player/airfield after a graphics change
- SVG icons disappearing when sound, camera or stats are toggled
- Silent failures masked by simulated tests or claimed deployment before verification

Central policy changes do **not automatically propagate** to this repository. Review/update this file when the shared standard changes.
