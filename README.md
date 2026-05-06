# TRIGO TMMMS New Hire Orientation

Browser-based new hire orientation training for **TRIGO Global Quality Solutions** inspectors at **Toyota Motor Manufacturing Mississippi (TMMMS)**.

The entire app is a single self-contained `index.html` file — no build step, no server, no dependencies beyond a modern browser. It works from disk, USB, email attachment, intranet share, or as a hosted site.

---

## What's inside

11 training modules covering:

| # | Module | Type |
|---|---|---|
| 1 | New Hire Information | Text + quiz |
| 2 | Shift Times & Call-In Line | Text + quiz |
| 3 | Cell Phone Policy | Text + quiz |
| 4 | Attendance Policy | 10-slide deck + checkpoints + final exam |
| 5 | Dress Code Policy | Text + quiz |
| 6 | Safety Processes | Text + quiz |
| 7 | EPIC Inspector Processes | Text + quiz |
| 8 | EPIC Inspector Scanning Guide | 22-slide deck + checkpoints + final exam |
| 9 | Example Materials & Forms | Text + quiz |
| 10 | Handbook Highlights | 23-slide deck + checkpoints + final exam |
| 11 | Health & Safety Awareness Training | 27-slide deck + checkpoints + final exam |

Plus three signed acknowledgment forms (attendance, emergency contact, completion) and an admin console for HR.

---

## Hosting on GitHub Pages

This is the recommended deployment path — free, zero-config, and the file is already named `index.html`.

1. Create a new public or private repo on GitHub.
2. Push the contents of this folder to the repo's default branch (typically `main`):
   ```bash
   git init
   git add .
   git commit -m "Initial deployment"
   git branch -M main
   git remote add origin https://github.com/<your-username>/<your-repo>.git
   git push -u origin main
   ```
3. In the repo on GitHub, go to **Settings → Pages**.
4. Under **Build and deployment → Source**, choose **Deploy from a branch**.
5. Pick branch `main` and folder `/ (root)`. Save.
6. After about a minute, the site is live at `https://<your-username>.github.io/<your-repo>/`.

The `.nojekyll` file in this folder is what tells GitHub Pages to skip its Jekyll processor and just serve the file as-is.

### Custom domain (optional)

If you have a domain like `orientation.trigo-yourcompany.com`:

1. In your DNS, create a CNAME record pointing to `<your-username>.github.io`.
2. Rename `CNAME.example` in this folder to `CNAME` and put your domain in it (one line, no protocol).
3. Commit and push. Then in **Settings → Pages → Custom domain**, enter the domain and check "Enforce HTTPS" once the cert provisions (~10 minutes).

---

## Other ways to deploy

**Internal file share / SharePoint / network drive:** Just copy `index.html` to the share. Users open it in their browser — no server needed.

**USB stick or email attachment:** Same — open `index.html` in any modern browser.

**Static web host (Netlify, Cloudflare Pages, S3, Azure Blob, etc.):** Drop `index.html` in the bucket / connect the repo. Set `index.html` as the default document.

---

## Where data is stored

The app uses **the user's own browser storage** — nothing is sent to a server. There is no backend.

- **Employee progress, signatures, quiz results:** browser `localStorage` under key `trigo_orientation_v1`.
- **Uploaded supervisor videos:** browser `IndexedDB` database `trigo_orientation_videos`.

This means each computer/browser holds its own roster of employees. If you need centralized records, the admin console exports completion transcripts as printable PDFs (via the browser's print-to-PDF). The app evicts the oldest employee record at 100 entries (FIFO by start date).

---

## Admin access

There is an admin console with a records browser, question editor, and video manager.

- **Password:** see source comment near the admin gate (or ask the developer).
- The admin password is hardcoded in `index.html`. This is a known limitation and is acceptable for the intended use case (internal training on shared machines, not public-facing).

---

## Browser support

Tested on current Chrome, Edge, Firefox, and Safari. The Great Vibes signature font loads from Google Fonts on first run; once cached, the app works fully offline.

---

## Editing the policy text

Most policy content lives inside the `MODULES` array near the top of the script section. Slide decks are stored as base64 JPEG arrays (`SLIDES`, `SAFETY_SLIDES`, `EPIC_SCANNING_SLIDES`, `ATTENDANCE_SLIDES`). Quiz questions for sections-type modules live alongside their `body` text in each section's `quiz` array; slides-type modules use `checkpoints[].quiz` and `finalQuiz`.

For non-trivial edits to slide images, the source materials and generation scripts are not in this deployment folder — keep those in a separate working folder.

---

## License

Internal training material. All rights reserved by TRIGO Global Quality Solutions.
