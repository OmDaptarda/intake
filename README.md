# Coach Om Intake

Client assessment for Om Daptardar's powerlifting and fitness coaching.
Clients fill in basics, lifestyle, a PAR-Q style health check, injuries, goals, lifts and
training setup. Each finished assessment is saved as one row in a Google Sheet
(download it as Excel any time: File > Download > Microsoft Excel).

```
index.html            the whole site (HTML, CSS, JS, no build step)
apps-script/Code.gs   the Google Sheet script that receives submissions
```

## 1. Connect the Google Sheet (about 5 minutes)

1. Go to **sheets.new** and name the sheet something like `Coach Om clients`.
2. In the sheet: **Extensions > Apps Script**.
3. Delete what's in `Code.gs`, paste in everything from `apps-script/Code.gs`, click **Save**.
   (Optional: put your email in `NOTIFY_EMAIL` to get an email for each new client.)
4. **Deploy > New deployment**. Click the gear next to "Select type" and pick **Web app**.
   - Execute as: **Me**
   - Who has access: **Anyone**
   - Click **Deploy**, then **Authorize access**. Google warns that the app isn't verified because
     it's your own script: click **Advanced > Go to (project name) > Allow**.
5. Copy the **Web app URL** (it ends in `/exec`). Open it in a browser once: you should see
   `{"ok":true,...}`.
6. In `index.html`, find `const SHEET_URL='';` near the top of the script and paste the URL
   between the quotes.

The first submission creates a `Submissions` tab with the header row. Repeats of the same
submission are ignored, so a client retrying on bad internet never creates a double row.

## 2. Put it online with GitHub Pages

1. Create a **public** repo (for example `coach-om-intake`) and upload `index.html`,
   `README.md` and `.nojekyll` (the `apps-script` folder is optional).
2. Repo **Settings > Pages**: Source = Deploy from a branch, Branch = `main`, folder = `/ (root)`, Save.
3. About a minute later the link is live at `https://<your-username>.github.io/coach-om-intake/`.
   Send that link to clients.

Do one test run yourself and check that the row shows up in the sheet.

## Notes

- Keep the Google Sheet private. It holds clients' health and injury answers.
- Each row also has a `Full profile (JSON)` column: the complete structured profile for a
  program generator.
- To change questions, edit the `STEPS` config near the top of the script in `index.html`.
  New fields show up as new sheet columns automatically.
- If you edit `Code.gs` later: Deploy > Manage deployments > Edit (pencil) > Version: New version
  > Deploy. The URL stays the same.
