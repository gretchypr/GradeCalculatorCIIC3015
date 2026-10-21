# Course Grade Calculator

A student-friendly, static calculator for tracking course grades, remaining points, passing requirements, and the final exam score needed to reach 70%.

## Course weights

| Category | Weight | Items |
| --- | ---: | --- |
| Exams | 35% | 3 exams, 100 points each |
| Projects | 20% | PA0-PA3: 100 points each |
| Labs | 20% | 10 labs, 100 points each |
| Attendance | 5% | 100 points |
| Final exam | 20% | 100 points |
| **Total** | **100%** | |

Quizzes are not included in this version.

## Using the calculator

1. Choose a category tab and enter the points earned for each graded item.
2. Leave future or ungraded work blank. Enter `0` for a graded item that earned no points; zero counts as graded work.
3. Review the progress table below the grade-entry area. Expand **See totals by category** for a detailed breakdown.
4. Select **Grade needed on final** to see the final exam score needed to reach 70 course points.

Grades are saved automatically in the same browser on the same device when local storage is available. Nothing is submitted to your professor. **Clear all grades** removes saved scores after confirmation.

## Understanding the results

Each category converts raw scores to course points using its weight and the total raw points possible across all planned items:

`Category course points = category weight × raw points earned / total planned raw points`

Each category's contribution is capped at its course weight.

| Result | Meaning |
| --- | --- |
| Points offered | Course points available from the items with grades entered |
| Points left to earn | 100 minus points offered; points assigned to work still blank |
| Points accumulated | Total weighted course points earned so far, out of 100 |
| Current grade | Points accumulated divided by points offered, expressed as a percentage |
| Points needed to pass | Additional course points needed to reach 70, with a minimum of zero |

For example, all work except the final exam offers 80 course points. If you earn 56.59 of those points, your current grade is `56.59 / 80 × 100 = 70.74%`. You would need another 13.41 course points, equivalent to `13.41 / 20 × 100 = 67.05%` on the final.

The final exam calculation uses entered non-final grades and assumes no additional points from blank work. It does not use an existing final exam score. The estimate may change as you enter more grades.

## Bonus points and passing requirements

- Include bonus points in the score for the item that earned them. Exam, lab, and project scores may exceed the item's listed maximum.
- Bonus points stay within their category. Exams can contribute at most 35 course points; projects and labs can each contribute at most 20.
- Project bonus points above an item's maximum are pooled to cover deficits below the 50% minimum on other entered projects. PA0-PA3 require 50 points each.
- Passing requires at least 70 course points, a lab average of at least 50%, and the project minimums after applying project bonuses.
- The requirements check uses entered grades. Blank work is pending, so meeting the current requirements does not guarantee that all requirements will be met when the course ends.

## Local development

The site uses plain HTML, CSS, and JavaScript. No dependency installation or build step is required.

- `dist/index.html`: page structure
- `dist/styles.css`: styling and responsive layout
- `dist/app.js`: categories, weights, calculations, and browser storage

Open `dist/index.html` in a browser for a quick preview. For a local server, run `python -m http.server 8000 --directory dist` from the repository root and visit `http://localhost:8000`. Browser storage is specific to the origin used to open the calculator.

Check JavaScript syntax with `node --check dist/app.js` and whitespace errors with `git diff --check`.

## GitHub Pages deployment

The workflow in `.github/workflows/deploy-pages.yml` publishes the contents of `dist/` directly to GitHub Pages. It runs on pushes to `master` and can also be started manually from the repository's **Actions** tab using **Run workflow**.

Repository setup:

1. In **Settings > Pages > Build and deployment**, set **Source** to **GitHub Actions**.
2. Ensure GitHub Actions is enabled and the `github-pages` environment permits deployments from `master`. Complete any required environment approvals.
3. Push the changes to `master`, then check the **Deploy grade calculator** workflow run for the deployment result and site URL.

The workflow checks out the repository, configures Pages, uploads `dist/`, and deploys the uploaded artifact. Its permissions include `contents: read`, `pages: write`, and `id-token: write`. No separate build or dependency installation is needed. Asset links are relative, so the site supports a repository subpath on GitHub Pages.

If the deployment branch changes, update the workflow's `on.push.branches` setting and the environment's deployment rules accordingly.
