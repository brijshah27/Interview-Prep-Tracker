# Google L5 Preparation Tracker

An installable, local-first interview-preparation tracker. The PWA is served by GitHub Pages; `L5_Tracker.xlsx` remains on your computer and is the database.

## How it works

- The installed Chrome or Edge app remembers the workbook selected during the first connection.
- Every dashboard change saves to the workbook after a short delay.
- The app checks the workbook every five seconds for changes saved from Excel.
- When an Excel change and an unsaved dashboard change conflict, Excel wins and the dashboard reloads the Excel state.
- The workbook is ignored by Git, so GitHub Pages never publishes your progress.

## Publish to GitHub Pages

1. Create an empty GitHub repository. GitHub Free supports Pages from public repositories; private-repository Pages requires GitHub Pro, Team, or Enterprise. The Pages site itself is publicly reachable, but this project excludes the workbook and does not upload progress data.
2. From this folder, add the remote and publish the branch:

   ```bash
   git remote add origin https://github.com/YOUR_ACCOUNT/YOUR_REPOSITORY.git
   git add .
   git commit -m "Add installable L5 tracker PWA"
   git push -u origin main
   ```

   The workbook has already been removed from Git tracking and is ignored by `.gitignore`. Its staged deletion removes only the repository copy; the local `L5_Tracker.xlsx` file remains in this folder.

3. In the repository on GitHub, open **Settings > Pages**, set **Source** to **GitHub Actions**, and save. The included workflow deploys each push to `main`.
4. Open the Pages URL after the action completes, usually `https://YOUR_ACCOUNT.github.io/YOUR_REPOSITORY/`.

## Install and connect

1. Open the Pages URL in current Chrome or Edge.
2. Use the browser's **Install app** control in the address bar/menu.
3. Launch the installed app and select **Connect workbook**.
4. Choose the local `L5_Tracker.xlsx` file and allow editing. For the persistent-permission prompt, choose **Allow on every visit** when offered.

After that one-time connection, launch the installed app normally. It restores the workbook, fetches its current data, and saves changes without a file picker or download step. If browser permission is later revoked, select **Connect workbook** to renew it; the app remembers the same file and asks only for permission.

## Excel workflow

Save edits in Excel as usual. The PWA detects the changed file within five seconds and reloads it. Do not make simultaneous edits in Excel and the PWA: when a conflict is detected, the app intentionally discards its pending change and loads Excel.

The workbook may be unavailable for writing while Excel holds an exclusive lock. In that case, save or close the workbook in Excel, then select **Save now** in the tracker.

## Development preview

For a local preview only, run:

```bash
python3 -m http.server 4173
```

Then visit `http://localhost:4173/L5_Dashboard.html`. This is not needed for normal daily use after the GitHub Pages PWA is installed.
