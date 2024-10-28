# static-website-cicd
Static website deployment onto github pages using github actions for the cicd

- Here's a step-by-step guide to deploying a static website on GitHub Pages with GitHub Actions. 
- The is the link to the repo that already has the codes with a sample html for the deployment https://github.com/Asiwomex/static-website-cicd
- You can clone this repo and use the index.html

---

## Step 1: Set Up the GitHub Repository

1. **Create a new repository** on GitHub (or use an existing one) and name it something like `static-website`.
2. **Add your static site files** (e.g., `index.html`, `style.css`, `script.js`).
3. **Commit and push** the static site files to the `main` branch.

## Step 2: Enable GitHub Pages for the Repository

1. Go to **Settings > Pages** in your repository.
2. Under **Source**, select `Deploy from a branch`.
3. Choose the `main` branch and the root directory for a simple setup.
4. Click **Save**. GitHub Pages will provide a link where your site will be hosted.
5. You can visit the link to view the already hosted website.

## Step 3: Create a GitHub Actions Workflow for Deployment

- This step comes in 2 folds
- create **".github/workflows"** directory in your main working directory
---

### Step 3b: Generating the github workflow from github

1. Go to **Settings > Pages** in your repository.
2. Under **Source**, select `Github Actions`.
3. Click on **Configure** under **Static HTML by github actions**
4. Wait for github generate the workflow for you
5. Save and commit changes to the main branch, it will be provided by github
6. Go to the actions tab to watch the workflow run
7. You can visit the link to view the already hosted website.

### Step 3b: Manually creating the github workflow

1. In your repository, navigate to the `.github/workflows/` folder.
   - If this folder doesn’t exist, create it.
2. Create a file named `static.yml` inside `.github/workflows/`.

3. **Add the following code** to `static.yml` to define the deployment and validation steps:

   ```yaml
    # Simple workflow for deploying static content to GitHub Pages
    name: Deploy static content to Pages

    on:
    # Runs on pushes targeting the default branch
    push:
        branches: ["main"]

    # Allows you to run this workflow manually from the Actions tab
    workflow_dispatch:

    # Sets permissions of the GITHUB_TOKEN to allow deployment to GitHub Pages
    permissions:
    contents: read
    pages: write
    id-token: write

    # Allow only one concurrent deployment, skipping runs queued between the run in-progress and latest queued.
    # However, do NOT cancel in-progress runs as we want to allow these production deployments to complete.
    concurrency:
    group: "pages"
    cancel-in-progress: false

    jobs:
    # Single deploy job since we're just deploying
    deploy:
        environment:
        name: github-pages
        url: ${{ steps.deployment.outputs.page_url }}
        runs-on: ubuntu-latest
        steps:
        - name: Checkout
            uses: actions/checkout@v4
        - name: Setup Pages
            uses: actions/configure-pages@v5
        - name: Upload artifact
            uses: actions/upload-pages-artifact@v3
            with:
            # Upload entire repository
            path: '.'
        - name: Deploy to GitHub Pages
            id: deployment
            uses: actions/deploy-pages@v4
       
   ```


### Step 4: Commit and Push the Workflow File

**Add, commit, and push** the workflow file to your repository:

   ```bash
   git add .github/workflows/deploy.yml
   git commit -m "Add GitHub Actions workflow for Pages deployment"
   git push origin main
   ```

### Step 5: Verify the Workflow

1. After pushing the workflow file, go to the **Actions** tab in your GitHub repository. You should see the workflow running.
2. If the workflow completes successfully, GitHub Pages will deploy your site.
3. You can check the **Settings > Pages** section for the URL where your static website is live.

---

