# Instructions for Sonnet 🤖

This file is for Claude Sonnet to understand the Azure Training project and complete GitHub setup.

---

## Project Summary

**What:** Complete Azure exam study guide (AZ-900 Fundamentals + AZ-801 Administrator)  
**Where:** `/Users/hardlygospel/repos/azure-training/`  
**Status:** Fully written (~3,250 lines), git initialized, ready to push  
**Next:** Push to GitHub, set up GitHub Pages, integrate with homepage

---

## Current State

✅ 18 markdown files created (see README.md)  
✅ Git repo initialized with initial commit  
✅ Project structure:
- `azure-fundamentals/` — 4 chapters + README
- `azure-801/` — 5 chapters + README  
- `common-qa/` — Q&A + troubleshooting guide
- Root: README, QUICK-REFERENCE, SETUP guide

---

## What Sonnet Should Do

### Task 1: Create GitHub Repository
- Create repo: `azure-training`
- Visibility: **Public**
- Description: "Azure Fundamentals (AZ-900) & Administrator (AZ-801) quick reference guide - exam prep with Q&A"
- Topics: `azure`, `azure-fundamentals`, `azure-801`, `certification`, `study-guide`, `az-900`

### Task 2: Push to GitHub
```bash
cd ~/repos/azure-training
git remote add origin https://github.com/YOUR-USERNAME/azure-training.git
git branch -M main
git push -u origin main
```

### Task 3: Set Up GitHub Pages (Optional)
- Enable GitHub Pages
- Source: main branch / root directory
- Theme: Choose one (e.g., "just-the-docs" for dark theme)
- Result: Serve at `https://YOUR-USERNAME.github.io/azure-training`

### Task 4: Add to Homepage (hardlygospel.github.io)
**Location:** Homepage repo (if exists)  
**Action:** Add "Training" section with link to azure-training repo

**Sample HTML:**
```html
<section id="training" class="training">
  <h2>Training & Certifications</h2>
  <div class="training-card">
    <h3>🔷 Azure Certifications Guide</h3>
    <p>Complete quick reference for Azure Fundamentals (AZ-900) and Azure Administrator (AZ-801)</p>
    <ul>
      <li><strong>AZ-900:</strong> Cloud concepts, Azure services, pricing, security</li>
      <li><strong>AZ-801:</strong> Identity, networking, compute, storage, monitoring</li>
      <li><strong>Q&A:</strong> Common exam questions with answers</li>
      <li><strong>Troubleshooting:</strong> Diagnostic guides and checklists</li>
    </ul>
    <a href="https://github.com/hardlygospel/azure-training" class="btn">View on GitHub</a>
    <a href="https://hardlygospel.github.io/azure-training" class="btn btn-alt">Read Guide</a>
  </div>
</section>
```

**Sample Markdown:**
```markdown
## Training Resources

### Azure Certifications
**[Azure Training Hub](https://github.com/hardlygospel/azure-training)** — Complete guide to passing Azure Fundamentals (AZ-900) and Administrator (AZ-801) exams

- 📖 **AZ-900:** Cloud concepts, deployment models, Azure services, pricing, security, compliance
- 🛠️ **AZ-801:** Identity & access, virtual networking, compute management, storage & backup, monitoring
- ❓ **Common Q&A:** Answers to 50+ frequently asked exam questions
- 🔧 **Troubleshooting Guide:** Diagnostic checklists and CLI commands

[View Full Guide](https://github.com/hardlygospel/azure-training)
```

---

## File Locations

- **Project root:** `/Users/hardlygospel/repos/azure-training/`
- **Memory file:** `/Users/hardlygospel/.claude/projects/-Users-hardlygospel/memory/project_azure_training.md`
- **Homepage repo:** `~/repos/hardlygospel.github.io` (if exists)
- **GitHub account:** tasmaniamate@gmail.com (from context)

---

## Important Notes

1. **Username:** User's GitHub username needed for exact repo URLs
2. **Homepage:** Check if `hardlygospel.github.io` repo exists first
3. **CDN:** All images already use public CDN links (cloudflare, etc.)
4. **No secrets:** No API keys or credentials in files
5. **Ready to ship:** Can be made public immediately

---

## Success Criteria

- [ ] Repo created on GitHub (public)
- [ ] All files pushed to main branch
- [ ] GitHub Pages enabled (optional but recommended)
- [ ] Training section added to homepage
- [ ] Links working (test both HTTP and docs)
- [ ] Topics/badges added to repo

---

## Useful Commands

```bash
# Verify current state
cd ~/repos/azure-training
git log --oneline
git status
find . -name "*.md" | wc -l

# Check homepage repo (if exists)
ls ~/repos/hardlygospel.github.io

# Test local serving (if Jekyll installed)
cd ~/repos/azure-training
jekyll serve
# Access at http://localhost:4000
```

---

**Ready to go! Push this to GitHub and integrate with homepage.** 🚀
