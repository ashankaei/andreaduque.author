# Book Website

A simple static site (no build step, no server).

## Files
- `index.html` : all the text. Search for "Author Name", "hello@example.com", and the blurb placeholders.
- `style.css` : colors and layout. Colors are at the top under `:root`.
- `images/` : put cover images here (create the folder), then replace the `<div class="cover">` in `index.html` with `<div class="cover"><img src="images/detours.jpg" alt="Detours cover"></div>`.

## Publish with GitHub Pages
1. Create a **public** repo on GitHub (free Pages needs public).
2. Upload these files (or push with Git).
3. Repo Settings > Pages > Source: "Deploy from a branch", branch `main`, folder `/ (root)`.
4. The site goes live at `https://USERNAME.github.io/REPO/` within a minute or two.

## Share with someone
Repo Settings > Collaborators > Add people. They can edit `index.html` directly in the browser (pencil icon), and each save updates the live site.

## Custom domain
Settings > Pages > Custom domain, then add the DNS records your domain registrar shows.
