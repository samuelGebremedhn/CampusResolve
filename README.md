# Utkal University — International Student Complaint & Support Portal

A Google Apps Script web application for international students to submit complaints and follow their status, with a separate office administration dashboard. The project uses a **Google Sheet** for records and **Google Drive** for evidence files.

## Project structure

| File | Purpose |
| --- | --- |
| `Code.gs` | Apps Script backend, Sheet integration, complaint workflows, notifications and evidence handling |
| `Index.html` | Student-facing portal |
| `Admin.html` | International Office dashboard |
| `Logo_IO.png` | University/office logo asset supplied with the project |
| `appsscript.json` | Apps Script manifest |
| `.gitignore` | Excludes local credentials and development files |

## Deployment (Google Apps Script)

> **This is not a static GitHub Pages site.** GitHub hosts the source code; Apps Script runs the backend and renders the HTML interfaces. Opening the HTML files directly will not make their Apps Script calls work.

1. Create a Google Sheet to hold complaint records.
2. In the Sheet, select **Extensions → Apps Script**. Create a script project bound to this Sheet.
3. Replace the default `Code.gs` contents with this repository's `Code.gs`.
4. Create two HTML files named **Index** and **Admin** (Apps Script adds `.html`) and paste the matching source files.
5. In **Project Settings**, enable showing the `appsscript.json` manifest and use the manifest in this repository if needed.
6. Run the **`setup`** function once in the Apps Script editor and authorize the requested permissions. It initializes/migrates the `Complaints` sheet and script properties.
7. **Before deployment**, open **Project Settings → Script Properties** and set `ADMIN_KEY` to a long, unique secret. The backend initializes it to the insecure placeholder `change-me-now` unless it already exists. Verify `OFFICE_EMAIL` is the intended office address. Do not commit either secret to GitHub.
8. Deploy via **Deploy → New deployment → Web app**. Choose the execution identity and access policy appropriate to your university's privacy requirements. The source header suggests **Execute as Me / Anyone**; review this carefully before allowing public access to a system that processes student information.
9. Open the web app URL for the student portal. Add `?view=admin` for the office dashboard; administrator functions require the configured key.

### Updating an existing deployment

Edit the bound Apps Script files, then use **Deploy → Manage deployments → Edit → New version → Deploy**. The GitHub repository and the Apps Script deployment do **not** synchronize automatically.

## Uploading to GitHub manually

From this folder in PowerShell or Terminal:

```bash
git init
git branch -M main
git add .
git commit -m "Prepare complaint portal for GitHub"
git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPOSITORY.git
git push -u origin main
```

If the GitHub repository **already exists**, clone it first and copy these project files into the clone; then use `git add -A`, `git commit`, and `git push origin main` instead of `git init`.

## Security and operational notes

- Student names, identifiers, complaints, and evidence may be sensitive. Never commit real student records, private evidence files, administrator keys, or spreadsheet credentials.
- The `Logo_IO.png` file is retained as supplied. Check that any references to it in the HTML/Apps Script are valid in your deployed project; an image in the GitHub repository is not automatically an Apps Script image resource.
- The existing backend explicitly sets `XFrameOptionsMode.ALLOWALL`. Assess clickjacking and embedding risks before institutional deployment.
- Test authentication, permissions, complaint submission, attachments, notification email, and admin actions using non-sensitive sample records before publishing.

## Technology

Google Apps Script (JavaScript), HTML, CSS, Google Sheets, Google Drive and Google Workspace services.
