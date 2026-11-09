# llaga.xyz

Chris Llaga's resume site, as plain HTML and CSS.

It is a static copy of the page that used to be published from Notion through
super.so (copied November 2026). The text, layout, fonts, colors and the
light/dark toggle match the original. There is no build step.

```
index.html          the page
style.css           super.so / Notion styles, trimmed to what the page uses
assets/logo.png     navbar logo and favicon
assets/fonts/       Inter (400, 500, 600, 700), the same files super.so served
resume/             /resume redirect to the home page (old super.so path)
resume-download/    /resume-download redirect to the Google Drive folder (old super.so path)
.nojekyll           tells GitHub Pages to serve the files as they are
```

The only JavaScript is the light/dark toggle, as on the original: the page
starts in dark mode and remembers the visitor's choice in `localStorage`
(`color-preference`).

Links on the page:

- Email: `mailto:chris@llaga.xyz`
- LinkedIn: <https://www.linkedin.com/in/chrisllaga/>
- Calendly: <https://calendly.com/chrisllaga/>
- Resume download: <https://drive.google.com/drive/folders/16ZAyMvKmDMugoUFdaOllo_Fq0D3QnHLW?usp=drive_link>
  (the original site linked here too, through its `/resume-download` redirect;
  the resume is not hosted on Notion or super.so)

## Preview locally

```sh
cd ~/Developer/llaga-site
python3 -m http.server 8000
```

Then open <http://localhost:8000/>. Use the server rather than opening the file
directly, so the `/resume` links and fonts resolve the same way they will online.

## Publish with GitHub Pages

1. Create a GitHub repository and push this folder to its `main` branch.
2. In the repository, go to **Settings > Pages**. Under **Build and deployment**,
   choose **Deploy from a branch**, branch `main`, folder `/ (root)`, and save.
3. Add a file named `CNAME` at the root containing one line, `llaga.xyz`, and push
   it (or type `llaga.xyz` under **Custom domain** in Settings > Pages, which
   commits the same file). This repository does not have it yet on purpose.
4. Check the site at `https://<username>.github.io/<repo>/` before changing DNS.
5. At Squarespace (Domains > llaga.xyz > DNS settings), point the website records
   at GitHub. Remove the existing records for `@` and `www` that point to super.so
   (in November 2026: `@` A `76.76.21.21` and `www` CNAME `cname.super.so`), then add:

   | Host  | Type  | Data                    |
   |-------|-------|-------------------------|
   | `@`   | A     | `185.199.108.153`       |
   | `@`   | A     | `185.199.109.153`       |
   | `@`   | A     | `185.199.110.153`       |
   | `@`   | A     | `185.199.111.153`       |
   | `@`   | AAAA  | `2606:50c0:8000::153`   |
   | `@`   | AAAA  | `2606:50c0:8001::153`   |
   | `@`   | AAAA  | `2606:50c0:8002::153`   |
   | `@`   | AAAA  | `2606:50c0:8003::153`   |
   | `www` | CNAME | `<username>.github.io.` |

   (The AAAA records are optional; they add IPv6.)
6. Once DNS has updated and GitHub shows the domain as verified, tick
   **Enforce HTTPS** in Settings > Pages.
7. Cancel the super.so site only after <https://llaga.xyz/> loads from GitHub.

> **Warning: do not touch the MX records** (or the TXT records for SPF, DKIM and
> domain verification). Email for chris@llaga.xyz (Google, `aspmx.l.google.com`)
> depends on them. Only the `@`
> A/AAAA records and the `www` record change.
