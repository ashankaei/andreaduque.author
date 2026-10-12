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

## Newsletter signup (how it works)
The "Be the first to know" form (`#signupForm`) is a plain form post to Mailchimp's `/subscribe/post` endpoint and opens Mailchimp's confirmation in a new tab. Don't switch it back to the JSONP endpoint (`/subscribe/post-json`): it returned 404 for this account.
- `EMAIL` is required, `FNAME` is optional, and `gdpr[241265]=Y` is the audience's required "Email Updates" permission. Keep that checkbox, or Mailchimp rejects the signup.
- The hidden `b_3a95c0c832f0a184601cef622_516c0ebd91` input is Mailchimp's bot trap. Leave it empty and hidden.
- To test, sign up with a real address on the live site, check Mailchimp → Audience, then unsubscribe it.
