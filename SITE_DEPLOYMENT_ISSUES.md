# Site deployment investigation

## Findings
- The working copy is on a branch named `work`. GitHub Pages normally builds from the default branch (often `main`) or a configured `gh-pages` branch, so pushing updates only to `work` would prevent the public site from updating.
- The only GitHub Actions workflow in the repo is `scrape_talks.yml`, which automates talk map updates. There is no explicit Pages deployment workflow here, so publishing depends on the branch configured in the repository settings.
- `_config.yml` already declares the production URL `https://cv.q1x.xyz`, but there is no `CNAME` file in the repo. If the custom domain is not set in the repository Pages settings, GitHub will not provision the domain even if DNS points to it.
- `cv.q1x.xyz` should be published from the `gh-pages` branch. A local branch named `gh-pages` now tracks the same commit as `work` so the publishing branch can be pushed without losing the recent edits.
- Cloudflare Pages (`marc-levy-cv-site.pages.dev`) can also point at `gh-pages` to keep both deployments in sync.

## Next steps
1. Verify which branch GitHub Pages is configured to build from. Merge or cherry-pick the latest changes from `work` into that branch so the site rebuilds.
2. In repository settings, confirm the custom domain is set to `cv.q1x.xyz` and add a `CNAME` file with that hostname if you want it tracked in version control.
3. After merging to the publishing branch, trigger a Pages build (e.g., by pushing a commit) and confirm the site updates.
