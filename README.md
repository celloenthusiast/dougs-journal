# Doug's Journal

Live site: https://celloenthusiast.github.io/dougs-journal/

This repository is the GitHub Pages front door for Doug's private journal.

## Architecture

- GitHub Pages provides the stable cross-platform URL.
- Google Apps Script runs the journal and stores data in Google Sheets / Drive.
- The GitHub wrapper uses the account-neutral Apps Script /exec URL.
- The journal's own PIN/session system protects access.
- No PIN or journal content belongs in this public repository.

## One required Apps Script change

In Code.gs, the doGet() function must be:

```javascript
function doGet() {
  return HtmlService.createTemplateFromFile('Index')
    .evaluate()
    .setTitle('Wiseman Journal')
    .setXFrameOptionsMode(HtmlService.XFrameOptionsMode.ALLOWALL)
    .addMetaTag('viewport', 'width=device-width, initial-scale=1, viewport-fit=cover');
}
```

Then deploy a NEW Apps Script web-app version:

- Execute as: Me
- Who has access: Anyone

Keep using the same /exec deployment URL. The GitHub wrapper is already pointed at it.


## 2026-09-25 startup fix

If the live site shows "Journal startup did not finish" before a PIN screen appears,
the Apps Script Index/Script files are out of sync. Replace the Apps Script
Script.html with the matched v1.3 Script.html, save, and deploy a new web-app
version. The GitHub wrapper itself is already functioning when this message is
visible.
