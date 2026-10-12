# Andrea Duque, Author Website

Static one-page site for *Detours* (no build step, no server). Everything lives in `index.html` (styles and scripts are inline).

## Editing
- Text: open `index.html` on GitHub and click the pencil icon. Search for the section you want (`id="story"`, `id="book"`, `id="cast"`, `id="quiz"`, `id="join"`, `id="follow"`).
- Each save to `main` republishes the site automatically (usually within a minute).

## Hosting
GitHub Pages, branch `main`, folder `/ (root)`. Custom domain is set by the `CNAME` file (`andreaduqueauthor.com`). DNS: four `A` records for `@` (185.199.108-111.153) and a `CNAME` for `www` pointing to `ashankaei.github.io`.

## Newsletter signup
The form on the page does **not** send emails anywhere yet. To collect real signups, replace the `<form id="signupForm">` block with the embed code from a service such as MailerLite, Buttondown or Mailchimp. Never commit subscriber lists or API keys to this repo.
