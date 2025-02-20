# hugo-mock-landing-page-autodeployed

This repository was imported from the original **hugo-mock-landing-page** repository. Its purpose is to automatically build and deploy the Hugo website to GitHub Pages using GitHub Actions. This document outlines the setup process, configuration details, and debugging tips.

## 1. Repository Import and Basic Setup

1. **Importing the Repository**  
   - The original **hugo-mock-landing-page** repository was imported as an independent repository named **hugo-mock-landing-page-autodeployed** using the GitHub Importer.  
   - This import preserves the complete version history, allowing you to experiment and modify without affecting the original project.

2. **Updating the `baseURL` Configuration**  
   - In the imported repository, update the `baseURL` in the configuration file (`config.toml` or `config.yaml`) to point to the new repository URL. For example:
     ```toml
     baseURL = 'https://<GitHub username>.github.io/hugo-mock-landing-page-autodeployed/'
     ```
   - Commit and push this change.

3. **Repository Settings**  
   To ensure GitHub Actions can run and deploy the website, the following settings must be configured:
   - Set the default `GITHUB_TOKEN` permissions to **read and write**.
   - In GitHub Pages settings, set the publishing source to the `gh-pages` branch.
   - Allow all actions and reusable workflows by adjusting the GitHub Actions permissions.

## 2. GitHub Actions Workflow for Automated Deployment

A workflow file has been added at `.github/workflows/gh-pages-deployment.yaml` to automate the following tasks:

1. **Checkout the Repository**  
   Uses [actions/checkout](https://github.com/actions/checkout) to clone the repository, including submodules (e.g., Hugo themes).

2. **Initialize the Hugo Environment**  
   Uses [peaceiris/actions-hugo](https://github.com/peaceiris/actions-hugo) to set up the Hugo environment with the specified version (e.g., `0.123.4` for extended Hugo).

3. **Deploy to GitHub Pages**
    Uses peaceiris/actions-gh-pages to push the generated static files to the gh-pages branch, which serves as the publishing source.

## 3. Workflow Explanation and Debugging Tips

- **Automatic Trigger**  
  The workflow is triggered on every push to the `main` branch.  
  *Note: Ensure that the default branch in your repository matches the branch specified in the workflow trigger.*

- **Troubleshooting**  
  - **Workflow Not Triggering?**  
    Verify that the YAML file is placed in the `.github/workflows/` directory and that the branch name in the trigger is correct.
  - **Build Errors (e.g., Missing Theme Module):**  
    Check your theme management approach:
    - If using a custom `themesdir` (e.g., `node_modules/@filipecarneiro`), ensure the dependencies are correctly installed via npm and the directory structure is as expected.
    - Alternatively, consider using Hugo Modules to manage your theme by declaring it in your configuration file.
  - **Deployment Failures:**  
    Ensure the `GITHUB_TOKEN` has the proper permissions (read/write) as outlined in the GitHub Actions permissions documentation.

## 4. Validating Automatic Deployment

1. Make changes to the website content (for example, update `content/contact.md`).
2. Commit and push the changes to the `main` branch. This will trigger the GitHub Actions workflow again.
3. After the workflow completes, verify that the changes are reflected by visiting:

## 5. Acknowledgements and References

- [GitHub Importer and Actions Permissions](https://docs.github.com/en/actions/security-guides/automatic-token-authentication)
- [peaceiris/actions-hugo](https://github.com/peaceiris/actions-hugo)
- [peaceiris/actions-gh-pages](https://github.com/peaceiris/actions-gh-pages)
- Portions of this documentation were based on conversations with AI assistants (e.g., Claude/ChatGPT) and various official documentation sources.

---

This document outlines the overall process, workflow details, and debugging tips for automatically building and deploying the Hugo website. If you have any questions or suggestions for improvements, please open an Issue in the repository.
