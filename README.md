# Society Edition Wedding Album: pCloud Proof of Concept

This is a **public technical experiment**, not a finished wedding album product.

## Purpose

Test whether an independently hosted website can:

1. Display a photograph stored in a **free pCloud account** through `getpubthumb`.
2. Read a public, shared pCloud folder using `showpublink`.
3. Rebuild the gallery when the owner adds a new photo and the visitor clicks **Load / Refresh Album**.

The page is a self-contained `index.html`, with no build dependencies, passwords, OAuth tokens or Society Edition-managed photo storage.

## Test workflow

- Open the deployed GitHub Pages URL in a standard browser and on a phone.
- Confirm Test A loads a photograph.
- Click **Load / Refresh Album** and confirm Test B shows the current image count.
- Add a test photo to the approved shared folder in pCloud, refresh Test B and confirm the image count rises.
- Test an anonymous guest upload using a separate pCloud **File Request** folder, then copy an approved photo into the publicly shared folder and refresh again.

## Privacy and limitations

**The pCloud shared link and its photographs are public.** The sharing code is present in `index.html` because this is an intentionally public integration test. Use only non-sensitive sample images. The `noindex` meta tag requests that search engines not index the page; it is not an access restriction.

The prototype does not provide real-time push updates, automatic background refresh, guest upload UI, automatic approval or album-level access control. It relies on pCloud APIs and policies that must be reviewed before commercial deployment. GitHub Pages serves only the webpage code, not the photos.

## Publishing

This is a static site. GitHub Pages can publish directly from the default branch `/ (root)`. No GitHub Actions or external build required.