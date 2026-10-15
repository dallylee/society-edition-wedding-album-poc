# Society Edition | Canva Code + pCloud proof of concept

**Status:** Test specification and copy-paste prompt, not a completed Canva Code website.

## Objective

Discover whether a *published Canva Code website* can (A) load the existing buyer-owned public pCloud gallery and (B) use user-authorised OAuth to create buyer-owned folders and upload links. These are two different technical gates.

**What is already proven elsewhere:** Static GitHub Pages can load the existing public pCloud folder and thumbnails, detect its Cover/Ceremony subfolders, and refresh after photo changes.

**What is NOT yet proven:** Canva Code network access, published runtime limitations, pCloud OAuth callbacks, authenticated write requests from Canva Code, and whether an independent buyer on a free Canva account can clone and publish their own copy.

## Prompt for Canva Code

```text
Create a deliberately crude, mobile-friendly INTERACTIVE CANVA CODE WEBSITE called “Society Edition | Canva Code and pCloud Feasibility Test”. This is a technical experiment, NOT a wedding design. It must work when published as a Canva Code website, not merely in the Canva preview.

CRITICAL: Never simulate successful API calls, invent photographs or fake successful OAuth/folder creation. Show accurate error states. No paid backend, database, proxy, third-party upload service or Canva-specific data storage. Never ask users for their pCloud password. No analytics. No logging of credentials or access tokens.

TEST A: PUBLIC PCLOUD FOLDER READ (must work without OAuth)
Use pCloud's European public API https://eapi.pcloud.com
Existing test folder share code: kZleOk7Zng7XFQVbL0zqJ3BCNdL98zYp0kJk
On “Load test album” button press, GET /showpublink?code=<share code>. The response's metadata.contents contains root files plus subfolders, with subfolder contents. Identify Cover using “Cover” or “00 - Cover”; identify Ceremony using “Ceremony” or “01 - Ceremony”, ignoring case and numeric prefixes. Display the first cover image prominently and all Ceremony photos in a simple grid. Use ordinary image elements with GET /getpubthumb?code=<share code>&fileid=<id>&size=1200x800. Show exact counts and a PASS message only after metadata fetch and image load; distinguish metadata failures from image failures. Also show folder names returned by the API in a small diagnostics area. Keep filenames as captions; do not inject them as HTML.

TEST B: ACTUAL PCLOUD AUTHORISATION AND ONE-TIME FOLDER SETUP
Show a text field for a PUBLIC pCloud Developer app client ID (blank by default, not a secret). If blank, show “OAuth not configured yet”; never imply setup worked.
When a valid client ID is entered and the user explicitly clicks “Connect pCloud”, use pCloud's official OAuth2 authorization page (https://my.pcloud.com/oauth2/authorize) with response_type=token, client_id, redirect_uri set to the published Canva Code website URL, and a random state parameter. The pCloud app must have this redirect URI registered by the tester. If the Canva runtime prevents redirect handling or URL fragments, show “Canva Code OAuth limitation” rather than fabricating success.
On return verify state; extract access_token and hostname from URL fragment; immediately remove the sensitive fragment from browser history, never save the token in localStorage/sessionStorage/URL/query string or UI and never log it. Hold token in memory only during this single session. Use pCloud's returned hostname to choose EU vs US API. For API calls send Authorization: Bearer <token> (never append the token to URLs).
After sign-in, show a separate, explicit “Create test folders and links” button and confirmation so nothing is created during page load.
Use createfolderifnotexists, starting at folderid=0, to create:
- Society Edition Canva POC (parent)
- Published Album (inside parent)
- Cover (inside Published Album)
- Ceremony (inside Published Album)
- Private Guest Uploads (inside parent, NOT inside Published Album)
Then use getfolderpublink on Published Album and createuploadlink on Private Guest Uploads, including a helpful wedding photo upload comment. Show each result and the resulting public folder link and guest upload link; show PASS only after pCloud actually confirms success for every step (result 0).
Do not publish the guest folder. Do not delete anything or modify any existing folder. If the API forbids a step from the Canva Code environment, show endpoint, error type and a concise explanation without leaking credentials. Offer a “Forget connection” action that clears the token held in memory (do not falsely claim revocation at pCloud).

For Test A and Test B, clearly label actual statuses: Not tested, In progress, Passed, Failed, or Blocked. Use simple styling, large usable phone buttons, readable messages. No animations, branding polish, payment screens, user accounts or Etsy integration. Prioritise real third-party API compatibility and a publishable Canva Code website.

At the end, provide a short plain-language summary of which APIs actually succeeded in the published website. Do not claim the whole customer workflow is complete until BOTH tests pass.
```

## How to run

1. In Canva, create a **Code** design (not an ordinary Canva Website), paste the complete prompt, and generate.
2. Publish directly from the Canva Code thread and save the live URL.
3. Run **Test A** on the published URL using the known public test photos. Record status and actual images.
4. Register a pCloud Developer application in the pCloud My Apps console, set its allowed redirect URI to the exact published Canva Code URL, and note the public **client ID**. Do not share the client secret or OAuth access token.
5. Return to the *published* Canva Code test, enter the app client ID, and run **Test B**. Test authentic login, folder creation, public share link and guest file request. Use only your test account.
6. Confirm that a second separate free Canva account can make its own independently publishable copy, rather than editing the author's original Canva Code thread.

## Security and policy constraints

- Public image link code is intentionally test data and already used in the public GitHub proof of concept.
- pCloud OAuth access tokens are highly sensitive and can be long-lived; never print or share them.
- Do not treat OAuth support, storage setup, Canva template copying or commercial/API permissions as proven before live checks.
- Etsy policy: sell an original downloadable design/template, not third-party subscription or access to a hosted membership service. Independently validate the final Etsy delivery model.
- All actual buyer photos remain in buyer-controlled storage; public share links still allow viewing by whoever has access.

## Official reference links

- Canva Code: https://www.canva.com/help/canva-code/
- Canva Code publishing: https://www.canva.com/help/publish-canva-code/
- pCloud API: https://docs.pcloud.com/
- pCloud app management: https://docs.pcloud.com/my_apps/
- pCloud OAuth: https://docs.pcloud.com/methods/oauth_2.0/authorize.html
- Etsy Services: https://www.etsy.com/legal/policy/services/242665313101
- Etsy Creativity Standards: https://www.etsy.com/legal/creativity/
