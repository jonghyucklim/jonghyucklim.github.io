# Jonghyuck Lim — academic website

A minimal Quarto website with Home, Research, CV, and Teaching pages. White background, navy links, system body fonts, and serif headings. Quarto supplies the responsive navigation; all custom styling is in `styles.css`.

## Preview and render

Install [Quarto](https://quarto.org/docs/get-started/) (tested with 1.10.18), open a terminal in this folder, and run:

```sh
quarto preview
```

For a complete static build:

```sh
quarto render
```

The result is in `_site/`. Edit the source files, not the generated HTML. No R, Python, Node packages, or database are needed to render this site.

This workspace also contains an untracked project-local Quarto installation. In PowerShell, you can use it immediately:

```powershell
& '.\.tools\quarto\bin\quarto.exe' preview
& '.\.tools\quarto\bin\quarto.exe' render
```

The `.tools/` directory is excluded from Git and site resources. It is only a local convenience; the GitHub workflow installs Quarto independently.

## Files

```text
_quarto.yml                    Site settings and navigation
index.qmd                      Home and short biography
research.qmd                   Research
cv.qmd                         CV link and education
teaching.qmd                   Teaching experience and materials
_includes/job-market-paper.qmd  Shared paper title, abstract, and link
styles.css                     Custom styling
pdfs/                          Public PDF files
  teaching/                    Syllabi and teaching materials
images/                        Images and favicon
.github/workflows/publish.yml   Manual GitHub Pages deployment
```

## Update the content

1. The job-market paper is *Reverse Engineering a Soft Landing*, copied from the supplied October 29, 2026 draft to `pdfs/job-market-paper.pdf`. Its title, coauthors, abstract control, and link are shared by Home and Research through `_includes/job-market-paper.qmd`. The supplied draft has an empty abstract section, so the website abstract remains marked forthcoming. Replace that placeholder when the abstract is ready.
2. The current CV is `pdfs/jonghyuck-lim-cv.pdf`, refreshed from the supplied `Jonghyuck_Lim_CV_2026.pdf` on October 31, 2026 and linked in `cv.qmd`. Replace that file when updating your CV; keep the short education and research-field summary on the CV page consistent with it.
3. The homepage contact link is `jlim@unc.edu`. Update the address and its `mailto:` target in `index.qmd` if your public email changes.
4. Fill in course, role, institution, and semester details in `teaching.qmd`. Add public teaching PDFs to `pdfs/teaching/`, then update the syllabus link and remove its availability notice.
5. The homepage portrait is `images/headshot_f.png`. To replace it, update the image and, if its dimensions change, the width and height attributes in `index.qmd`. Its responsive size is controlled by `styles.css`.

Remaining forthcoming notices identify unavailable content. The job-market abstract and teaching details have not been inferred.

The Research page also lists *Understanding the Distribution of Inflation Expectations*, linked to the St. Louis Fed's article and official PDF. The older *Soft Landing Engineering* working-paper entry has been replaced by the revised job-market paper above. Previous PDFs, the older abstract, and update provenance are preserved under the ignored `.qa/asset-update-2026-10-31/` directory, outside the public site.

Each paper has an **Abstract** control that expands its text on the page. Full-paper PDF links are separate. The publication's abstract is in `_includes/abstracts/inflation-expectations.qmd`; the job-market paper's abstract is still marked forthcoming in its shared include. These controls use native HTML `details` and `summary` elements and require no custom JavaScript.

## Publish to GitHub Pages when ready

The site is configured for the user-site address **https://jonghyucklim.github.io/**. The workflow below builds and publishes the site from the source files in this repository.

1. Create a public GitHub repository named **`jonghyucklim.github.io`** under **`jonghyucklim`**, or use that repository if you already own it. Add these source files to its default branch. Generated output and project-local tools are ignored by Git.
2. In the repository, open **Settings → Pages**, and choose **GitHub Actions** as the source.
3. Open **Actions → Publish Quarto website → Run workflow** on the default branch. The workflow installs the pinned Quarto version, renders the four pages, and deploys `_site/` using GitHub's Pages artifact workflow.
4. Once deployed, future manual runs update the same site. If you prefer automatic publishing, add `push: { branches: [main] }` beneath `on:` in the workflow, using your actual default branch name.

The workflow is manual so uploading the source alone does not trigger publication. It uses GitHub's built-in token; no personal access token is required. To use a different repository name or domain, update `website.site-url` in `_quarto.yml` to the final public address.

References: [Quarto websites](https://quarto.org/docs/websites/), [Quarto and GitHub Pages](https://quarto.org/docs/publishing/github-pages.html), and [GitHub's custom Pages workflows](https://docs.github.com/en/pages/getting-started-with-github-pages/using-custom-workflows-with-github-pages).
