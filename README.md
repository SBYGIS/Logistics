# Logistics
Pages for Print versions of Salisbury Fire Department's Logistics Forms
# 📄 SFD Logistics — Print Pages

> Hosted print views for ArcGIS Online popup forms.  
> These pages are linked from AGOL map popups and open in a browser as a clean, printable summary of form data.

---

## 🧠 What Is This Repository? (Start Here)

Think of GitHub like a **shared filing cabinet in the cloud** — except instead of paper files, it holds code files (like HTML pages).

This repository (think: *one drawer in that cabinet*) holds all the **print pages** for our GIS forms. When someone clicks "Open Print View" in an AGOL popup, their browser opens one of these HTML files — the page then automatically pulls the form data from ArcGIS and displays it in a clean layout ready to print or save as a PDF.

### Why GitHub and not just a shared drive?

| Shared Drive | GitHub |
|---|---|
| Anyone can accidentally overwrite a file | Every change is tracked with a history |
| No public web address for files | Every file gets its own public URL |
| Hard to know what changed or when | You can see exactly who changed what |

---

## 🗂️ What's in This Repository

```
logistics/
│
├── README.md                        ← You are here
│
├── supply_requisition_print.html    ← Supply Requisition form
├── incident_report_print.html       ← Incident Report form (example)
├── equipment_checkout_print.html    ← Equipment Checkout form (example)
├── training_log_print.html          ← Training Log form (example)
└── ...add more as needed
```

Each `.html` file is one form's print page. They are completely independent — adding or editing one does not affect the others.

---

## 🌐 How GitHub Pages Works

**GitHub Pages** is a free feature that turns your repository into a website. Once it's turned on, every file in the repo gets a public URL automatically:

```
https://[your-username].github.io/[repository-name]/[filename].html
```

For example:
```
https://sbygis.github.io/logistics/supply_requisition_print.html
https://sbygis.github.io/logistics/incident_report_print.html
```

You don't need to do anything special — just upload the file and the URL works immediately (it may take 1–2 minutes to go live after uploading).

---

## 🚀 Setup: Enabling GitHub Pages (Do This Once)

You only need to do this once when you first create the repository.

1. Go to your repository on GitHub (e.g. `github.com/sbygis/logistics`)
2. Click the **Settings** tab (near the top right)
3. In the left sidebar, scroll down and click **Pages**
4. Under **Source**, click the dropdown and select **Deploy from a branch**
5. Under **Branch**, select **main** and leave the folder as `/ (root)`
6. Click **Save**
7. Wait about 2 minutes — then your site is live at `https://[username].github.io/[repo-name]/`

> ✅ You'll see a green banner in the Pages settings with your live URL once it's ready.

---

## ➕ How to Add a New Page

### Option A — Upload through the GitHub website (easiest)

1. Go to your repository on `github.com`
2. Click the **Add file** button (near the top right)
3. Select **Upload files**
4. Drag your `.html` file into the upload area
5. Scroll down to the **Commit changes** section
6. Type a short note in the first box describing what you added  
   *(Example: "Add incident report print page")*
7. Click the green **Commit changes** button
8. Done! The file is now live at its URL within 1–2 minutes.

### Option B — Create a file directly on GitHub

1. Go to your repository on `github.com`
2. Click **Add file** → **Create new file**
3. Type the filename at the top (e.g. `incident_report_print.html`)
4. Paste your HTML code into the editor
5. Scroll down, add a commit note, and click **Commit changes**

---

## ✏️ How to Update an Existing Page

1. Go to your repository on `github.com`
2. Click on the file you want to edit (e.g. `supply_requisition_print.html`)
3. Click the **pencil icon** (✏️) in the top right of the file preview
4. Make your changes in the editor
5. Scroll down, add a short note describing what you changed  
   *(Example: "Fix items table not showing size field")*
6. Click **Commit changes**
7. The live page updates within 1–2 minutes.

> 💡 **Tip:** Every change is saved in the history. If something breaks, you can always go back to a previous version — click **History** at the top of any file to see all past versions.

---

## 🔗 How to Link a Page from an AGOL Popup

Once your HTML file is uploaded, you link to it from the **Arcade expression** in your AGOL popup. The link is built automatically and passes the feature's GlobalID so the page can fetch its own data.

In the Arcade expression, find this line near the top:

```javascript
var PRINT_URL = 'https://sbygis.github.io/logistics/supply_requisition_print.html';
```

Change the filename to match whichever page you're linking to. The rest of the expression handles building the full URL with the GlobalID attached.

### The full URL your popup generates looks like this:
```
https://sbygis.github.io/logistics/supply_requisition_print.html?globalid={xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}
```

The `?globalid=...` part is added automatically — you don't type it manually. The HTML page reads that ID and queries ArcGIS for the data.

---

## 📋 Adding a New Form — Checklist

Use this checklist every time you set up a print page for a new form:

- [ ] Get the HTML print page file (built with Claude or copied from an existing one)
- [ ] Upload it to this repository (see **How to Add a New Page** above)
- [ ] Note the public URL: `https://sbygis.github.io/logistics/[filename].html`
- [ ] In AGOL, open the layer's popup settings
- [ ] Add a new **Attribute Expression** element
- [ ] Paste in the Arcade expression for that form
- [ ] Update the `PRINT_URL` variable at the top of the Arcade expression to match the new file's URL
- [ ] Save the popup and test by clicking a feature on the map

---

## ❓ Common Questions

**Q: I uploaded the file but the URL isn't working.**  
A: Wait 1–2 minutes and try again. GitHub Pages takes a moment to publish new files. If it still doesn't work after 5 minutes, check Settings → Pages to make sure Pages is enabled and set to the `main` branch.

**Q: The page loads but shows "No items found."**  
A: This usually means the feature has no related records yet, or the GlobalID wasn't passed correctly. Check the URL in your browser — it should end with `?globalid={...some ID...}`.

**Q: The page loads but shows dashes (—) for all the fields.**  
A: The page couldn't fetch the parent record. This can happen if the ArcGIS feature service requires a login. Contact your GIS administrator to check whether the service is publicly accessible.

**Q: I want to change the look of all the pages at once.**  
A: Each page is currently self-contained. If you want a shared stylesheet in the future, that's a more advanced setup — ask your GIS team.

**Q: Can I have the same page work for two different layers?**  
A: Yes, with some extra logic in the HTML. The easiest approach is to pass a `?layer=...` parameter in the URL and have the page switch which service URL it queries based on that.

---

## 🧰 Files Reference

| File | Form | AGOL Layer |
|---|---|---|
| `supply_requisition_print.html` | Supply Requisition | SFD_Supply_Requisition_Form |
| *(add rows as you add pages)* | | |

---

## 📬 Questions?

Contact the GIS team or open an **Issue** in this repository (click the Issues tab at the top) to report a problem or request a new page.
