# CyberTacticsForge

Static website for CyberTacticsForge, hosted with GitHub Pages. No build step or package installation is required.

For the everyday commands to update from GitHub, resolve conflicts, and publish to `main`, see [Git Push and Pull](GIT_PUSH_AND_PULL.md).

## Preview locally

From this directory:

```sh
python3 -m http.server 8765 --bind 127.0.0.1
```

Open http://127.0.0.1:8765. Stop the server with Ctrl+C.

## Review the redesign

The redesign is on `design/polished-nonprofit`, based on main commit `eb626b1`. It introduces a responsive, scrolling homepage, section navigation, expandable biographies, volunteer contact links, optimized competition artwork, and a support section linking to the existing Stripe-hosted donation checkout. Core navigation, biographies, and the donation link work without homepage JavaScript. Stripe handles the donation checkout on its own site.

- `index.html`: homepage content and semantic structure.
- `index.css`: colors, typography, layouts, and responsive styles.
- `index.js`: mobile navigation and current-section highlighting.
- `assets/competition-*.webp`: optimized versions of existing artwork.

The TRETC pages, 404 page, existing assets, and custom domain configuration remain available. The legacy particle scripts are no longer loaded by the homepage but remain in the repository.

## Push to a fork

A **branch** is a separate line of work within a repository. A **fork** is your own GitHub copy of a repository. Either can be the source of a pull request into the original repository's main branch.

1. Create a fork of `cybertacticsforge/cybertacticsforge.github.io` in your GitHub account.
2. Add your fork as a second remote (replace `YOUR-ACCOUNT`):

   ```sh
   git remote add fork https://github.com/YOUR-ACCOUNT/cybertacticsforge.github.io.git
   git push -u fork design/polished-nonprofit
   ```

3. To propose the redesign, open a pull request with the original repository's `main` as the base and your fork's `design/polished-nonprofit` as the head.

If you prefer to keep the branch in the original repository:

```sh
git push -u origin design/polished-nonprofit
```

Pushing this branch does not merge it into main. No remote push or production deployment is included in this local redesign.

## Optional fork preview with GitHub Pages

For a separate fork preview, select the redesign branch and `/ (root)` in the fork's Settings → Pages, and remove the `CNAME` file **on the fork preview branch** so the preview does not use the production custom domain. Use the preview URL shown by GitHub; homepage assets use relative paths and support a repository subpath.

Keep the production `CNAME` when proposing the final design to the original repository. A separate preview-only branch is useful if you want to publish the fork preview and also open a clean pull request.

## Before publishing

Review the page on desktop and mobile, expand biographies, open the volunteer PDF, and check the competition and contact links. Confirm the donation link opens the existing Stripe checkout. No payment is needed to review this design. The link was obtained from the public configuration of the existing Stripe buy button; the donation destination is unchanged.

## Redesign validation

Checked locally in Chromium on September 10, 2026:

- Layouts at 1440, 1024, 780, 768, 390, and 320 pixels: no horizontal overflow.
- Mobile menu: opens, closes after navigation, closes with Escape, and moves focus to the selected section.
- Biographies expand and collapse; navigation and biographies remain usable without JavaScript.
- Automated axe scans for WCAG 2 A/AA and WCAG 2.1 AA: no violations on desktop or mobile. Automated scans are not a complete accessibility audit.
- No browser JavaScript errors; local assets and anchor targets resolve.
- Desktop and mobile screenshots reviewed.

The embedded Stripe form was replaced with its existing hosted checkout URL after the embed produced contrast and form-label issues. Payment submission was not tested.


## Programs page

`programs/index.html` is the standalone ForgeOps program hub at `/programs/`, with the two tracks, four programs, VCR explanation, and expandable schedules. Edit its content directly; its isolated stylesheet is `programs/programs.css`. The foundation homepage links to it in the main navigation and retains the flagship ppsCTF feature. Technical classes remain at `https://jboyce1.github.io/ppsCTF/`.
