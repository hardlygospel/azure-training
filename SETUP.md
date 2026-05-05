# Setup Guide 🚀

Instructions for uploading to GitHub and integrating with your homepage.

## Step 1: Initialize Git & Create GitHub Repo

### Local Setup
```bash
cd ~/repos/azure-training
git init
git add .
git commit -m "Initial commit: Azure training hub (AZ-900 + AZ-801)"
```

### Create GitHub Repository
1. Go to [github.com/new](https://github.com/new)
2. **Repository name:** `azure-training`
3. **Description:** "Azure Fundamentals (AZ-900) & Administrator (AZ-801) quick reference guide"
4. **Public** (so others can learn)
5. **Create repository**

### Push to GitHub
```bash
git remote add origin https://github.com/YOUR-USERNAME/azure-training.git
git branch -M main
git push -u origin main
```

---

## Step 2: Enable GitHub Pages

### Option A: Use docs/ folder (Recommended)
1. Copy all content to `docs/` folder
2. GitHub Pages → Source: main / docs
3. Access at: `https://YOUR-USERNAME.github.io/azure-training`

### Option B: Use README.md
1. GitHub Pages → Source: main / root
2. Serve README.md as homepage

### Option C: Build HTML (Advanced)
```bash
# Use a static site generator (Jekyll, Hugo)
npm install -g jekyll
jekyll new --skip-bundle .
jekyll build
```

---

## Step 3: Create Training Section on Homepage

### If you have hardlygospel.github.io repo:

**Add to your homepage HTML/Markdown:**

```html
<section id="training">
  <h2>Training & Certifications</h2>
  <div class="training-grid">
    <a href="https://github.com/YOUR-USERNAME/azure-training" class="card">
      <h3>🔷 Azure Training Hub</h3>
      <p>Complete guide to Azure Fundamentals (AZ-900) & Administrator (AZ-801)</p>
      <ul>
        <li>Cloud concepts & models</li>
        <li>Azure services</li>
        <li>Networking & compute</li>
        <li>Security & compliance</li>
      </ul>
      <button>View Guide</button>
    </a>
  </div>
</section>
```

**Or in Markdown:**
```markdown
## Training Resources

### Azure Certifications
- [Azure Training Hub](https://github.com/YOUR-USERNAME/azure-training) - Complete AZ-900 & AZ-801 guide
  - Cloud concepts & deployment models
  - Core Azure services (compute, storage, networking, databases)
  - Identity, security, and compliance
  - Hands-on examples and Q&A
```

---

## Step 4: Add Custom Domain (Optional)

If you want `yourname.dev/training`:

1. **Create subdirectory:** `training/` in homepage repo
2. **Copy content** from azure-training
3. **Update links** in navigation
4. **Commit & push**

**Result:** `yourname.dev/training` → Azure guides

---

## Step 5: Add Navigation Links

### Homepage Footer/Nav Bar:
```html
<nav>
  <a href="/">Home</a>
  <a href="/training">Training</a>
  <a href="/blog">Blog</a>
  <a href="/projects">Projects</a>
</nav>
```

### Training Hub Navigation:
```markdown
# Training Hub

- **[Azure Fundamentals (AZ-900)](./azure-fundamentals/)** - Start here
- **[Azure Administrator (AZ-801)](./azure-801/)** - Next level
- **[Common Q&A](./common-qa/)** - Answers to exam questions
- **[Quick Reference](./QUICK-REFERENCE.md)** - Cheat sheet
```

---

## Step 6: Customize for Your Brand

### Update README.md:
- Replace "Training Hub" with your branding
- Add your social links
- Update last modified date

### Create `_config.yml` (if using Jekyll):
```yaml
title: Azure Training Hub
description: Complete guide to Azure certifications
theme: just-the-docs
```

### Create CSS (if hosting standalone):
```css
:root {
  --primary: #0078d4; /* Azure blue */
  --text: #1e1e1e;
  --bg: #ffffff;
}
```

---

## Step 7: Maintenance

### Weekly:
- [ ] Review comments/issues
- [ ] Add new Q&A if needed

### Monthly:
- [ ] Check Azure docs for changes
- [ ] Update links if broken
- [ ] Test exam tips against latest exam

### Quarterly:
- [ ] Review passing scores (may change)
- [ ] Add new services if released
- [ ] Update pricing sections

---

## CDN Images Reference

All images used should be from public CDNs:

- **Microsoft Docs CDN:** `docs.microsoft.com/*`
- **Cloudflare CDN:** `cdnjs.cloudflare.com/*`
- **Unpkg:** `unpkg.com/*`
- **jsDelivr:** `cdn.jsdelivr.net/*`

**Test CDN:** Verify image loads from different location to confirm CDN working.

---

## SEO & Discovery

### Add to GitHub Topics:
- `azure`
- `azure-fundamentals`
- `azure-801`
- `certification`
- `study-guide`
- `az-900`
- `az-801`

### Add Badge to README:
```markdown
![Azure](https://img.shields.io/badge/Azure-0078D4?style=flat&logo=microsoft-azure)
![License](https://img.shields.io/badge/License-MIT-green)
![Last Updated](https://img.shields.io/badge/Last%20Updated-May%202026-blue)
```

### Add to Awesome Lists:
- [Awesome Azure](https://github.com/kristofferandreasen/awesome-azure)
- [Awesome Certifications](https://github.com/gitpod-io/awesome-certifications)

---

## Share & Promote

### Share on:
- **Reddit:** r/learnprogramming, r/Microsoft, r/Azure
- **Twitter:** `#Azure #AZ900 #AZ801 #MicrosoftCertified`
- **LinkedIn:** Learning resources post
- **DEV:** Dev.to article with link
- **Newsletter:** If you have one

---

## Troubleshooting

**GitHub Pages not working?**
- [ ] Repository is public
- [ ] `.github/pages` folder exists (if using)
- [ ] `index.md` or `README.md` exists
- [ ] No `.nojekyll` file preventing builds

**Links broken?**
- Use relative paths: `./chapter.md` not `/chapter.md`
- Test locally: `jekyll serve`

**Images not loading?**
- Use absolute CDN URLs
- Test CDN is accessible from your region
- Verify image format (PNG, JPG, SVG)

---

## Next Steps

1. **Create repo** on GitHub
2. **Push content**
3. **Enable GitHub Pages**
4. **Add to homepage**
5. **Share with community**
6. **Update monthly** with new content

---

**Happy studying! Let's get you certified! 🎯**
