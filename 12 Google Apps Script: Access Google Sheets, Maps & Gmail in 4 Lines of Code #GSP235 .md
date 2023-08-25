# GSP235
### [Google Sheets](http://sheets.google.com/create) > In first cell paste `Cloud Hustlers, India` > Enter
### Extensions > Apps Script > paste the code and replace the username 
```cmd
function sendMap() {
    var sheet = SpreadsheetApp.getActiveSheet();
    var address = sheet.getRange("A1").getValue();
    var map = Maps.newStaticMap().addMarker(address);
    GmailApp.sendEmail("REPLACE-YOUR-USERNAME", "Map", 'See below.', {attachments:[map]});
}
```
### Rename the code.gs file with `Cloudhustler` > Run > Review Permissions > Select GCP account > Allow
