# Society Edition Wedding Album: Folder-Aware pCloud Proof of Concept

This is a **public technical experiment**, not a finished customer product. Its purpose is to demonstrate that a single shared folder in a buyer-owned **free pCloud account** can drive a wedding album cover and chapter galleries without Society Edition hosting photographs.

## Live page

https://dallylee.github.io/society-edition-wedding-album-poc/

## Current album folder convention

In the already-shared pCloud parent folder (`etsy test`):

```text
etsy test/
├── 00 - Cover/        # Exactly one selected cover photograph
├── 01 - Ceremony/     # Two or more ceremony photographs
├── other-file-1.jpg   # Still visible in the original root-gallery test
└── other-file-2.jpg

Wedding Guest Uploads/  # Private, separate pCloud file-request destination
```

The folder names must match exactly, except for case/outer whitespace. Use ordinary shared-folder links, not pCloud Premium's paid Public Folder hosting.

### How it works

- **Test C (first on the page):** Reads the existing parent-folder public link with pCloud `showpublink`, finds `00 - Cover` and `01 - Ceremony`, picks the first cover photograph by filename, and displays Ceremony photos in a chapter. Runs automatically at page load or on **Refresh album from pCloud**. Handles missing folders and failed thumbnails visibly.
- **Test A:** Preserves the previously verified static external-thumbnail embedding check.
- **Test B:** Preserves the previously verified manually refreshed gallery of photos placed directly at the parent-folder root.

The display uses pCloud `getpubthumb`; new photos or changes to the cover are discovered on the next refresh. No OAuth tokens, app-managed photograph storage, build tooling or database are required for this proof of concept.

## Manual end-to-end test

1. Confirm the two named subfolders exist inside the already-shared parent folder.
2. Add one photograph to `00 - Cover` and two or more to `01 - Ceremony`.
3. Open the live GitHub Pages site on desktop and mobile. Confirm the album shows the correct cover and ceremony images.
4. Replace the cover photograph in pCloud, return to the page, press **Refresh album from pCloud** and confirm the new cover appears.
5. Add a new Ceremony photograph, refresh, and confirm its appearance.
6. Press **Load / Refresh Album** under Test B and confirm the original root-level photos still appear.
7. For the already-tested guest upload workflow, submit via the private pCloud File Request, then copy approved photos into the public album's desired folder and refresh the site.

## Verification and limitations

The folder-aware code was checked with `node --check` and automated Chromium/Playwright browser tests using **mocked** pCloud metadata and image responses, including mobile layout and missing-folder handling. The real nested-folder response and nested thumbnail access still need verification in the live browser.

The shared pCloud folder link and every included photograph are **publicly accessible**. The `noindex` meta tag only asks search engines not to index the page and **does not provide access control**. Use non-sensitive test photos only. The guest-upload folder must remain separate from the publicly shared album.

The prototype has no automatic approval, owner login, interactive customisation dashboard, full-resolution photo-download capability, continuous background updates, buyer self-onboarding, or guaranteed provider service levels. pCloud commercial API usage and traffic terms must be reviewed before selling this as an Etsy product.

## Publishing

A static `index.html` publishes from the default branch root through GitHub Pages. The `.nojekyll` marker disables Jekyll processing. No build step or GitHub Actions required.