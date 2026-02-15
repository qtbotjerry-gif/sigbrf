# SignalBrief Website - GitHub Pages Deployment Instructions

## Prerequisites
- GitHub account
- Repository named `sigbrf` (or any name)

---

## Step 1: Create GitHub Repository

1. Go to https://github.com/new
2. **Repository name:** `sigbrf`
3. **Description:** SignalBrief landing page
4. **Visibility:** Public (required for GitHub Pages)
5. **DO NOT** initialize with README, .gitignore, or license
6. Click **Create repository**

---

## Step 2: Push Local Code to GitHub

Run these commands from your terminal:

```bash
cd /Users/jerry/.openclaw/workspace/sigbrf_site

# Add GitHub remote (replace YOUR_USERNAME with your GitHub username)
git remote add origin https://github.com/YOUR_USERNAME/sigbrf.git

# Push code
git branch -M main
git push -u origin main
```

**Note:** You may be prompted for GitHub credentials. If using 2FA, you'll need a Personal Access Token instead of your password.

### Creating a Personal Access Token (if needed):
1. Go to https://github.com/settings/tokens
2. Click "Generate new token (classic)"
3. Give it a name (e.g., "SignalBrief Deploy")
4. Select scope: `repo` (full control of private repositories)
5. Click "Generate token"
6. Copy the token and use it as your password when pushing

---

## Step 3: Enable GitHub Pages

1. Go to your repository on GitHub
2. Click **Settings** (top menu)
3. Click **Pages** (left sidebar)
4. Under **Source**, select:
   - Branch: `main`
   - Folder: `/ (root)`
5. Click **Save**
6. Wait 1-2 minutes for the site to build

**Your site will initially be available at:**
`https://YOUR_USERNAME.github.io/sigbrf/`

---

## Step 4: Configure Custom Domain (sigbrf.com)

### In GitHub:
1. Still in **Settings → Pages**
2. Under **Custom domain**, enter: `sigbrf.com`
3. Click **Save**
4. Check "Enforce HTTPS" (after DNS propagates)

### In GoDaddy (DNS Configuration):
1. Log in to GoDaddy
2. Go to **My Products** → **DNS**
3. Find **sigbrf.com**
4. Add/Update these records:

**A Records (for apex domain):**
```
Type: A
Name: @
Value: 185.199.108.153
TTL: 600 seconds

Type: A
Name: @
Value: 185.199.109.153
TTL: 600 seconds

Type: A
Name: @
Value: 185.199.110.153
TTL: 600 seconds

Type: A
Name: @
Value: 185.199.111.153
TTL: 600 seconds
```

**CNAME Record (for www subdomain):**
```
Type: CNAME
Name: www
Value: YOUR_USERNAME.github.io
TTL: 600 seconds
```

5. Click **Save**
6. Wait 10-60 minutes for DNS propagation

---

## Step 5: Verify Deployment

After DNS propagates, verify these URLs work:
- ✅ https://sigbrf.com
- ✅ https://www.sigbrf.com

Both should show the SignalBrief landing page with HTTPS enabled.

---

## Step 6: Update Placeholders

Before launching, update the HTML files to replace placeholders:

1. **Stripe Links:**
   - `STRIPE_STARTER_LINK` → Starter plan checkout URL
   - `STRIPE_PRO_LINK` → Pro plan checkout URL
   - `STRIPE_PORTAL_LINK` → Customer portal URL

2. **Form Links:**
   - `INTAKE_FORM_LINK` → Google Form or intake processor URL
   - `UPDATE_FORM_LINK` → Update podcast form URL

3. **Support Email:**
   - `SUPPORT_EMAIL` → Your support email address

Then commit and push changes:
```bash
git add .
git commit -m "Update links and placeholders"
git push
```

---

## Troubleshooting

**Issue:** DNS not resolving
- **Solution:** Wait longer (up to 48 hours max, usually 1-6 hours)
- **Check:** Use `dig sigbrf.com` to verify DNS records

**Issue:** HTTPS not available
- **Solution:** Wait for GitHub to provision SSL certificate (can take 24 hours)
- **Ensure:** Custom domain is correctly set in GitHub Pages settings

**Issue:** 404 error
- **Solution:** Ensure branch is set to `main` and folder is `/ (root)` in Pages settings
- **Verify:** CNAME file exists in repository root

**Issue:** Push failed
- **Solution:** Create a Personal Access Token (see Step 2)
- **Verify:** Remote URL is correct: `git remote -v`

---

## Commands Summary

```bash
# Clone or navigate to site directory
cd /Users/jerry/.openclaw/workspace/sigbrf_site

# Add remote (only first time)
git remote add origin https://github.com/YOUR_USERNAME/sigbrf.git

# Push changes
git add .
git commit -m "Your commit message"
git push

# Check DNS
dig sigbrf.com

# Check CNAME
dig www.sigbrf.com CNAME
```

---

## Next Steps

After deployment is complete:
1. Test all links on the live site
2. Update Stripe checkout success URLs to point to https://sigbrf.com/success.html
3. Update Stripe cancel URLs to point to https://sigbrf.com
4. Share the link and monitor for errors

---

**Deployment Location:** /Users/jerry/.openclaw/workspace/sigbrf_site  
**GitHub Pages:** Enabled after following steps above  
**Custom Domain:** sigbrf.com (configured via CNAME file)
