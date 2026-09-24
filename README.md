# Restaurant menu: admin creates, customers view

| Page | Who | Link |
|---|---|---|
| Customer menu | Customers (QR code) | `https://<username>.github.io/<repo>/` |
| Admin | Restaurant staff only | `https://<username>.github.io/<repo>/admin.html` |

## Settings
Repo, restaurant name, photo quality and QR link are set in `CONFIG` at the top of the script in `admin.html`.

## Files
- `index.html` – the customer menu (replaced each time you publish)
- `admin.html` – admin: publish menu + QR code generator
- `sw.js`, `manifest.webmanifest`, `icon.svg` – offline support and home-screen icon
- `pdf.min.js`, `pdf.worker.min.js` – PDF reader (pdf.js, Apache-2.0)
- `menu-qr-code.png`, `menu-qr-code.svg` – fixed QR code for the menu link
- `qrcode.js` – QR code generator (qrcode-generator by Kazuhiko Arase, MIT)

## One-time setup
1. Create a GitHub repository and upload all files from this folder to its root.
2. Settings → Pages → Deploy from a branch → `main`, `/ (root)` → Save.
3. Create an access token: GitHub → Settings → Developer settings → Fine-grained tokens → Generate.
   - Repository access: **Only select repositories** → this repo
   - Permissions → **Contents: Read and write**
4. Open `admin.html`, paste the token as the **Admin key**, keep **Remember me** ticked and tap **Sign in**.
   The browser can also save it like a password and autofill it next time.
   Or send staff a secret link: `https://restaurant-menu-bh.github.io/view/admin.html#key=YOUR_TOKEN`
   (saves the key on their device and removes it from the address bar).
   Never put the token inside any file in this repo.
5. Make your QR code point to the customer link.

## Tabs (several PDFs)
Add one PDF per section (Food, Drinks, Desserts…) and give each a name – customers see them as tabs.
The admin page loads the published menu first, so you can replace, rename, reorder or remove one tab without re-uploading the others.
Direct link to a tab: add `#tab-name`, e.g. `.../view/#drinks`.

## Updating the menu (admin)
Open admin.html → choose PDF → Convert → check preview → **Publish to customers**.
The customer link shows the new menu after about 1–2 minutes. The link and QR code never change.

## QR code
The QR link is fixed in admin.html (`MENU_URL` near the top of the script) to https://restaurant-menu-bh.github.io/view/.
Ready-made files are also in the repo: `menu-qr-code.png` and `menu-qr-code.svg`.
For another restaurant's repo, change `MENU_URL` to that repo's link.
Download PNG (with restaurant name and caption) for printing at home, or SVG (code only) for a print shop.

## Security
- Customers can only view. Changing the menu needs the access token.
- Anyone can open admin.html, but without the token they cannot publish.
- If the token is lost or leaked, delete it on GitHub and create a new one.

## Offline
- After a customer opens the menu once with internet, it opens on their phone without internet.
- "Add to Home Screen" gives them a menu icon.
- "Download copy" in admin saves `menu.html` for a tablet or USB stick with no internet at all.
