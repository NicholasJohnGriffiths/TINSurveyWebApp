# TIN Survey Web App (Azure + MailerLite)

Single-page web app that hosts an embedded MailerLite form for survey capture, intended to be opened from an email campaign link.

## 1) MailerLite form status

Your MailerLite embed code is already integrated in [index.html](index.html), including:

- Form container `mlb2-36596359`
- Submit endpoint `forms/178326180957521302/subscribe`
- MailerLite Universal script for account `1537579`

The form styles are extracted to [ml-embed.css](ml-embed.css) for easier maintenance.

If you update the form in MailerLite later, replace the embedded block in [index.html](index.html) with the newest embed code from `Forms -> Embedded forms -> Share -> Embed code`.

## 2) Run locally (optional)

From the project folder, run one of:

```powershell
python -m http.server 5500
```

Then open:

- http://localhost:5500

## 3) Deploy to Azure Static Web Apps

1. Create a GitHub repo and push this project to `main`.
2. In Azure Portal, create a **Static Web App** and connect it to this repo/branch.
3. In GitHub repo settings, add secret:
   - `AZURE_STATIC_WEB_APPS_API_TOKEN` (value from Azure Static Web Apps deployment token)
4. The workflow at [.github/workflows/azure-static-web-apps.yml](.github/workflows/azure-static-web-apps.yml) deploys automatically.

## 4) Use in email campaign

Use the deployed URL in your email CTA/button (for example, `https://<your-app>.azurestaticapps.net`).

### Prefill fields from MailerLite subscriber data

The page supports prefill values via query string and maps them to your MailerLite fields.

Supported parameters:

- `email`
- `name` (or `first_name`)
- `last_name` (or `lastname`)
- `company`
- `fye_current_year`
- `fye_year_1`
- `fye_year_2`

When `email` is provided in the link, the email input is automatically locked (`readonly`) so users cannot change identity accidentally.

Example URL format:

`https://<your-app>.azurestaticapps.net/?email=person@example.com&name=Jane&last_name=Doe&company=Acme&fye_current_year=2024&fye_year_1=2023&fye_year_2=2022`

In MailerLite campaign links, replace these sample values with your campaign personalization tokens for each subscriber.

## Notes

- This app is intentionally minimal: one page, one embedded form.
- If your MailerLite form redirects after submit, configure that in MailerLite form settings.
