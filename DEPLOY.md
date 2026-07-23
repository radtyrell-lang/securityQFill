# Deploying SecurityQFill to GitHub Pages

Step-by-step instructions for the founder. Estimated time: 20–30 minutes end to end.

---

## What you need before starting

- A GitHub account (free) — create one at github.com if you don't have one
- Git installed on your machine (`git --version` to check)
- The two HTML files in this directory: `index.html` and `thank-you.html`
- Optional: a custom domain purchased via Namecheap (~$10/year)

---

## Step 1 — Create a free Tally form (email capture)

1. Go to https://tally.so and create a free account.
2. Click "New form". Set the title to "SecurityQFill Early Access".
3. Add a single field: Email (required). Set the submit button label to "Reserve my spot".
4. Under Settings > Redirect, set the "Thank you page" redirect URL to your GitHub Pages URL + `/thank-you.html` (e.g., `https://tyrelltle.github.io/securityqfill/thank-you.html`). You can update this after Step 3 once you know the URL.
5. Click "Share" and copy the embed URL — it looks like `https://tally.so/embed/XXXXXXXX`.
6. Create a second Tally form for the survey (the 4-question survey on the thank-you page). Title it "SecurityQFill Survey". Add the 4 questions from VALIDATION.md Section 4. Copy its embed URL.
7. In `index.html`, replace both instances of `YOUR_FORM_ID` with your sign-up form's ID (the alphanumeric part after `/embed/`).
8. In `thank-you.html`, replace `YOUR_SURVEY_FORM_ID` with your survey form's ID.

Tally is free for unlimited responses on the basic plan. No payment card required.

**Fallback (if you skip Tally):** Uncomment the Formspree `<form>` blocks in both HTML files and comment out the Tally iframes. Create a free Formspree account at formspree.io, create two endpoints (one for sign-up, one for survey), and replace `YOUR_FORM_ID` / `YOUR_SURVEY_FORM_ID` accordingly.

---

## Step 2 — Create a GitHub repository

1. Go to https://github.com/new
2. Repository name: `securityqfill` (this becomes part of the URL)
3. Set visibility to **Public** — GitHub Pages requires a public repo on the free plan
4. Do NOT initialize with a README (you will push files directly)
5. Click "Create repository"

---

## Step 3 — Push the landing page files

Run these commands in your terminal from the `landing-page/` directory (where `index.html` lives):

```bash
# Initialize a new git repo in the landing-page directory
git init
git add index.html thank-you.html

# Commit
git commit -m "initial landing page"

# Point to the GitHub repo you created
git remote add origin https://github.com/tyrelltle/securityqfill.git

# Push to the main branch
git push -u origin main
```

If GitHub asks you to authenticate, use a Personal Access Token (Settings > Developer settings > Personal access tokens > Generate new token, select `repo` scope).

---

## Step 4 — Enable GitHub Pages

1. Go to your repository on GitHub: `https://github.com/tyrelltle/securityqfill`
2. Click **Settings** (top tab)
3. In the left sidebar, click **Pages**
4. Under "Source", select **Deploy from a branch**
5. Branch: `main`, folder: `/ (root)` — click **Save**
6. GitHub will display your site URL within 1–2 minutes: `https://tyrelltle.github.io/securityqfill/`
7. Test both pages:
   - `https://tyrelltle.github.io/securityqfill/`
   - `https://tyrelltle.github.io/securityqfill/thank-you.html`

---

## Step 5 (Optional) — Add a custom domain via Namecheap

A custom domain like `securityqfill.com` costs ~$10/year and looks more trustworthy than a GitHub subdomain.

1. Buy the domain at https://namecheap.com (search `securityqfill.com` or a variant)
2. In your GitHub Pages settings (same page as Step 4), enter your custom domain in the "Custom domain" field and click Save
3. GitHub will create a `CNAME` file in your repo automatically
4. In Namecheap, go to your domain's DNS settings and add these records:

   | Type  | Host | Value                   | TTL  |
   |-------|------|-------------------------|------|
   | A     | @    | 185.199.108.153         | Auto |
   | A     | @    | 185.199.109.153         | Auto |
   | A     | @    | 185.199.110.153         | Auto |
   | A     | @    | 185.199.111.153         | Auto |
   | CNAME | www  | tyrelltle.github.io.    | Auto |

5. Wait 15–30 minutes for DNS to propagate
6. Back in GitHub Pages settings, check "Enforce HTTPS" once the green check appears
7. Update your Tally redirect URL to use the custom domain (e.g., `https://securityqfill.com/thank-you.html`)

---

## Step 6 — Update Tally redirect URL

Once you know your final URL (GitHub subdomain or custom domain), go back to your Tally sign-up form settings and update the redirect to point to the correct `thank-you.html` URL.

---

## Step 7 — Test end-to-end before posting anywhere

1. Open the live URL in an incognito window
2. Enter a test email and click "Reserve my spot"
3. Confirm you are redirected to `thank-you.html`
4. Confirm the survey loads on the thank-you page
5. Confirm a test response appears in your Tally dashboard
6. If using Formspree, confirm the email notification arrives at radtyrell@gmail.com

Only post in communities (Hacker News, Indie Hackers, etc.) after confirming the end-to-end flow works.

---

## Updating the page later

To push changes to the live page:

```bash
# From the landing-page/ directory
git add index.html thank-you.html
git commit -m "update copy"
git push
```

GitHub Pages deploys within 1–2 minutes of each push.

---

## Swapping in real social proof

When early users give you real quotes, replace the placeholder in `index.html`:

Find this HTML comment in `index.html`:

```html
<!-- PLACEHOLDER: Replace this quote block with a real quote after first user interviews. -->
```

Update `.quote-text` and `.quote-attr` with the real name and quote, then push.

---

## Support

Questions about this setup? radtyrell@gmail.com
