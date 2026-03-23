# Static Site

Minimal static site scaffold with SPA routing support.

## Structure

```
index.html    — HTML5 entry point
styles.css    — Stylesheet
main.js       — JavaScript entry point
vercel.json   — Vercel deployment config (SPA rewrites)
```

## Deploy to Vercel

1. Push this repo to GitHub.
2. Go to [vercel.com](https://vercel.com), import the repository.
3. Vercel auto-detects the static site. Click **Deploy**.

All routes will resolve to `index.html` via the rewrite rule in `vercel.json`.

## Deploy to GitHub Pages

1. Push this repo to GitHub.
2. Go to **Settings > Pages**.
3. Set source to the branch and folder containing these files.
4. Save — the site will be live at `https://<user>.github.io/<repo>/`.

For SPA routing on GitHub Pages, add a `404.html` that redirects to `index.html`:

```html
<!DOCTYPE html>
<html>
<head>
  <script>
    sessionStorage.setItem('redirect', location.pathname);
    location.replace('/');
  </script>
</head>
</html>
```

Then in `main.js`, handle the redirect:

```js
const redirect = sessionStorage.getItem('redirect');
if (redirect) {
  sessionStorage.removeItem('redirect');
  history.replaceState(null, '', redirect);
}
```
