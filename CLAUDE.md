# Notes for Claude working on andreaduqueauthor.com

Static site on GitHub Pages: no build step and no server. `index.html` is the whole homepage (styles and scripts inline), and `privacy.html` is the privacy policy. Every push to `main` goes live within about a minute. The repo is **public**.

Two people edit this repo: Andrea (`duqueandreina1406`) and Amirali (`ashankaei`). Both mostly touch `index.html`.

## How to work
- Pull `main` before starting. Make changes on a branch and merge with a small PR. Keep each PR to one topic so the two of you don't conflict.
- After a change, open the page in a browser and check the console for errors. A Content-Security-Policy error means a resource is blocked (see below).

## Security rules (please keep these)
- **Keep the `Content-Security-Policy` meta tag** at the top of both pages. When you add something from another site, allow only that exact origin in the matching directive (`img-src`, `font-src`, `form-action`, `script-src`…). Never loosen it to `*` or `https:`.
- **Don't add third-party scripts without asking Andrea and Amirali first.** That includes Mailchimp's "connected site" script (`<script id="mcjs">` from chimpstatic.com), analytics, chat widgets and pixels. They run with full access to the page and can set tracking cookies, which would need a cookie banner and Privacy Policy updates.
- Host images in the repo (as `andrea-duque.jpg` and `detours-banner.jpg` are), compress them, and give them real `alt` text.
- External links: `target="_blank" rel="noopener noreferrer"`.
- Never commit secrets, API keys, passwords or subscriber lists. Mailchimp's form `u`/`id` values are fine; they're public by design.
- Don't touch `CNAME`. It holds the custom domain.

## To do: newsletter signup may be broken (found 2026-10-12)
The "Be the first to know" form (`#signupForm`, added in PR #7) submits through Mailchimp's JSONP endpoint `/subscribe/post-json`. Two problems:

1. **Missing consent field.** The Mailchimp audience (`516c0ebd91`) has a *required* "Email Updates" GDPR permission, field `gdpr[241265]` with value `Y`. The form never sends it, so Mailchimp will probably reject every signup.
2. **The JSONP endpoint returned 404** in a test (empty email, nothing subscribed), while the regular `/subscribe/post` endpoint answered normally. It may not be enabled for this account.

Suggested fix:
- Add a required checkbox to the form: `<input type="checkbox" name="gdpr[241265]" value="Y" required>` with a label like "Yes, I'd like to receive book updates and news from Andrea Duque by email." Send `&gdpr[241265]=Y` in the JSONP URL too, and block submitting until it's ticked.
- Optionally add a first-name field, `FNAME` (the audience has one).
- If `post-json` still fails, fall back to a normal form post (remove `e.preventDefault()` in that case, or drop the JS). The `action`, `method="post"` and `target="_blank"` already in the form handle that, and `form-action` in the CSP already allows the Mailchimp host.
- **Test with a real email address** on the live site, check that it shows up in Mailchimp → Audience, then unsubscribe it. An empty or fake address doesn't prove anything.
- Delete this section once it's fixed and tested.
