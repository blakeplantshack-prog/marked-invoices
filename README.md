# Marked Invoices

A dashboard for The Plant Shack's weekly plant invoices. It is one web page (`index.html`) served by GitHub Pages, and it goes alongside the [stickers app](https://blakeplantshack-prog.github.io/plant-shack-stickers/). It is not connected to the till.

The **Marked Invoices Google Sheet is the back end**. The page reads it and saves small changes straight back into it, so the sheet keeps working exactly as before.

- **This week**: the Plants tab, one tab button per supplier, with totals, stickers to print and a status on every line. Edit qty, retail and notes, or press **Now in system** to move a price from Not In System to Retail.
- **Previous weeks**: any W tab, laid out the same way.
- **Orders**: the Orders tab by supplier. Tick orders off or add a new one under a supplier.
- **Price look up**: search this week and the last 5 weeks for what you paid and what you sold it for.

Before every save the page re-reads that row of the sheet. If the row has moved (someone added or deleted rows), it saves nothing and reloads.

## Using it on a shop computer

1. Open https://blakeplantshack-prog.github.io/marked-invoices/ in Chrome and bookmark it.
2. Press **Sign in with Google** and use the Google account that has the Marked Invoices sheet (or one it is shared with as an editor).
3. Google sign-ins last about an hour. When the page asks again, press the button again.

## One-time Google setup (so the GitHub page can open the sheet)

The page needs a Google "OAuth client ID". It is not a password and is safe to have in a public repo.

1. Go to https://console.cloud.google.com/ signed in as blakeplantshack@gmail.com and create a project called **Marked Invoices**.
2. **APIs & Services → Library**: search **Google Sheets API** and press **Enable**.
3. **APIs & Services → OAuth consent screen** (Google Auth Platform): choose **External**, app name **Marked Invoices**, and your email for the support and contact fields. Under **Audience → Test users**, add every Google account that will use the page (yours first).
4. **APIs & Services → Credentials → Create credentials → OAuth client ID**: type **Web application**. Under **Authorised JavaScript origins** add `https://blakeplantshack-prog.github.io`. Leave redirect URIs empty. Press **Create**.
5. Copy the **Client ID** (ends in `.apps.googleusercontent.com`) and put it in `index.html` on the line `const GOOGLE_CLIENT_ID = "";`.

While the app is in "Testing", only the test users can sign in, and Google shows a "Google hasn't verified this app" screen the first time. Press **Continue**. That's expected for a private shop tool.
