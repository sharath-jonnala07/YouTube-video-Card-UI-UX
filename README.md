# YouTube Video Card UI/UX

A compact mobile-feed prototype for comparing three YouTube-style video-card treatments. The same two video previews stay in view while card radius, horizontal inset, and screen theme can be changed interactively.

> This is a visual prototype, not a YouTube client. The video images are static previews; playback, navigation, accounts, and network data are not implemented.

## The design question

Rounded corners on a full-bleed thumbnail can read as clipped when the card touches both screen edges. This prototype makes that choice easy to compare against a card with side gutters and a square-corner treatment.

| Option | Card edges | Horizontal inset |
| --- | --- | --- |
| **Original** | Rounded | None; remains edge-to-edge |
| **Radius + padding** | Rounded | 12px on both sides |
| **No radius** | Square | None; remains edge-to-edge |

All three options keep the same 12px vertical spacing above the first card, between cards, and below the last card. That keeps the comparison focused on corner shape and side inset instead of changing several spacing cues at once.

## Try the prototype

- Select a card style to compare the feed treatments.
- Switch between dark and light screen themes. The outer canvas follows the theme with a charcoal treatment in dark mode and a pale textured treatment in light mode; a rounded outline keeps the preview distinct from its surroundings.
- On first load, a short animated cue highlights both control groups. The cue is disabled for people who request reduced motion.

The layout is sized to show both complete video cards and the bottom navigation together in the mobile preview. The video areas remain previews inside the feed; they do not open as a full-screen player.

## Design rationale

The prototype treats this as a comparison, not a claim that one radius or inset is universally better. Research on perceptual grouping supports using spacing and similarity as cues for how interface elements relate; therefore the vertical rhythm is held constant while the horizontal card treatment changes. A study of shape expectations in dialog interfaces suggests shape can carry meaning, but it does not establish an optimal radius for video cards. The options should ultimately be judged with viewers in the intended feed context.

### Research references

- Xie, M., Xing, Z., Feng, S., Xu, X., Zhu, L., & Chen, C. (2022). [Psychologically-Inspired, Unsupervised Inference of Perceptual Groups of GUI Widgets from GUI Images](https://doi.org/10.1145/3540250.3549138). *ESEC/FSE 2022*. The work models grouping cues including proximity and similarity in GUI layouts; it motivates keeping list spacing consistent across these treatments.
- Wagemans, J., Elder, J. H., Kubovy, M., Palmer, S. E., Peterson, M. A., Singh, M., & von der Heydt, R. (2012). [A Century of Gestalt Psychology in Visual Perception: I. Perceptual Grouping and Figure–Ground Organization](https://doi.org/10.1037/a0029333). *Psychological Bulletin, 138*(6), 1172–1217. A broad review of visual grouping and figure–ground organization.
- Yan, X. E., Feldman, J., Bentley, F., Khwaja, M., & Gilbert, M. (2023). [A Case Study Exploring Users' Perceptions and Expectations of Shapes for Dialog Designs](https://doi.org/10.1145/3544549.3573845). *CHI Conference on Human Factors in Computing Systems Extended Abstracts*. This is adjacent evidence about interface shape expectations, not a direct test of video-card corners.

## Implementation

- Single-file static app: `index.html` contains the markup, inline CSS, and small interaction script.
- The supplied screenshot's thumbnail and avatar crops are embedded in the HTML, so there are no separate image assets to manage.
- Roboto and Material Symbols are loaded from Google Fonts. The page has no package dependencies, build step, API, or backend.
- Theme and card-style controls are native buttons with accessible labels and pressed states. The animated onboarding cue respects `prefers-reduced-motion`.

## Run locally

Open `index.html` directly in a browser, or serve the repository root:

```bash
python -m http.server 8080
```

Then visit `http://localhost:8080`.

## Deploy to Vercel

The repository is static HTML/CSS/JavaScript and is ready to deploy from its root. No Vercel configuration file or build tooling is required.

1. Import this GitHub repository in Vercel.
2. Set **Framework Preset** to **Other**.
3. Keep the **Root Directory** at the repository root.
4. Leave the build command empty (enable the build-command override and leave its value blank if Vercel asks for one).
5. Serve the repository root as the output directory (`.`); if there is no `public` directory, Vercel can serve the root directly.

See Vercel's guide to [configuring a build and skipping the build step](https://vercel.com/docs/builds/configure-a-build).
