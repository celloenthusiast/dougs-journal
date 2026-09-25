# Doug's Journal

Live site: https://celloenthusiast.github.io/dougs-journal/

GitHub Pages provides the stable public front door. Google Apps Script runs the
private journal and stores journal data in Google Sheets / Drive.

## Current Apps Script build: v1.8 self-contained

The Apps Script web app now needs only two runtime source files:

- Code.gs
- Index.html

Index.html contains its CSS and JavaScript inline. This intentionally removes
HtmlService template includes from the request path so doGet() cannot fail while
trying to evaluate Styles.html or Script.html.

The Apps Script doGet() should be:

```javascript
function doGet() {
  return HtmlService.createHtmlOutputFromFile('Index')
    .setTitle('Doug's Journal')
    .setXFrameOptionsMode(HtmlService.XFrameOptionsMode.ALLOWALL)
    .addMetaTag(
      'viewport',
      'width=device-width, initial-scale=1, viewport-fit=cover'
    );
}
```

After replacing Code.gs and Index.html, deploy a NEW web-app version:

- Execute as: Me
- Who has access: Anyone

The GitHub wrapper already uses the account-neutral /exec URL:

https://script.google.com/macros/s/AKfycbwp8L0guuDD7uK3pS00qiIJy9GUJusKNJumhqFlWqpGnqDBNkYO1fjiPooRYfiUNAUFdw/exec

No PIN or journal content belongs in this public repository.


## Branding

All user-facing branding, backup/export names, and new attachment-folder names use **Doug's Journal**.
The existing session-storage key remains unchanged so current signed-in browsers are not forced to log in again.
