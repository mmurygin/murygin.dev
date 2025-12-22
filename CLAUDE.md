# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Static HTML/CSS/JS personal portfolio website for Maxim Murygin (Senior Site Reliability Engineer). No build system, frameworks, or dependencies required. Deployed to AWS S3 + CloudFront via GitHub Actions.

**Live site:** https://murygin.dev
**Primary branch:** main (deploys automatically)

## Development Commands

### Local Development Server

```bash
# Python (recommended)
python3 -m http.server 8000
# Then open http://localhost:8000

# Node.js alternative
npx serve .
```

### Deployment

Deployment is fully automated via GitHub Actions. Push to `main` branch triggers:
1. S3 sync (excludes .git, .github, *.md files)
2. CloudFront cache invalidation for: index.html, styles.css, scripts.js, static/cv.pdf

**No manual deployment steps required.**

## Architecture

### File Structure

- **index.html** (~580 lines) - Complete page structure with all sections
- **styles.css** (~950 lines) - All styling with CSS variables, responsive design, print styles
- **script.js** (~170 lines) - Animations, navigation, scroll effects
- **static/** - Profile photo, CV PDF, certification PDFs
- **export/** - LinkedIn data export (CSV files, source of truth for content)

### CSS Architecture

Uses CSS variables (`:root`) for theming. Key variables:
- `--primary`, `--primary-dark` - Blue accent colors
- `--gradient` - Blue to purple gradient
- `--background`, `--background-alt` - Light backgrounds
- `--text`, `--text-secondary` - Text colors
- `--radius` - Border radius (12px)

**Alternating sections:** Use `.section-alt` class for background variation.

### HTML Section Structure

Page follows this order (all in index.html):
1. **Hero** (lines 32-60) - Name, title, profile photo, CTAs
2. **About** (lines 64-88) - Summary with animated stats
3. **Experience** (lines 92-282) - Timeline with `.timeline-item` divs
4. **Skills** (lines 286-405) - Categorized `.skill-tag` elements
5. **Certifications** (lines 409-461) - Clickable `.cert-card` links
6. **Education** (lines 465-480) - University card
7. **Languages** (lines 482-505) - Progress bars
8. **Recommendations** (lines 509-539) - Quote cards
9. **Contact** (lines 543-564) - Email/LinkedIn links

### JavaScript Features

All in script.js:
- Mobile hamburger menu toggle
- Smooth scroll navigation (80px header offset)
- Intersection Observer for fade-in animations
- `animateStats()` - Counter animations in About section
- Language progress bar animations
- Active nav link highlighting based on scroll position
- Typewriter effect for hero title

## Data Source

**LinkedIn export in `export/` directory is the source of truth.** When updating content:

1. Update the LinkedIn export CSV files:
   - `Profile.csv` - Name, headline, summary, location
   - `Positions.csv` - Work experience
   - `Skills.csv` - Technical skills
   - `Certifications.csv` - Certs with URLs
   - `Education.csv` - University info
   - `Languages.csv` - Language proficiency
   - `Recommendations_Received.csv` - Testimonials

2. Manually sync changes to index.html (no automated import)

## Common Content Updates

### Add Work Experience

Add new `.timeline-item` div in Experience section (lines 92-282):

```html
<div class="timeline-item">
    <div class="timeline-marker"></div>
    <div class="timeline-content">
        <div class="timeline-header">
            <h3>Job Title</h3>
            <a href="https://company.com" target="_blank" class="company">Company Name</a>
            <span class="period">Jan 2020 - Dec 2023</span>
            <span class="location">City, Country</span>
        </div>
        <p class="timeline-description">Role description</p>
        <ul class="achievements">
            <li>Key achievement 1</li>
            <li>Key achievement 2</li>
        </ul>
        <div class="tech-stack">
            <span class="tech-tag">Technology</span>
        </div>
    </div>
</div>
```

### Add Skills

Add to appropriate `.skill-category` in Skills section (lines 286-405):

```html
<span class="skill-tag">New Skill Name</span>
```

### Add Certifications

Add to `.certs-grid` (lines 409-461):

```html
<a href="https://verification-url.com" target="_blank" class="cert-card">
    <div class="cert-logo aws">AWS</div>
    <h3>Certification Full Name</h3>
    <p class="cert-issuer">Issuing Authority</p>
    <p class="cert-date">Month Year</p>
</a>
```

Supported `.cert-logo` classes: `aws`, `redhat`, `openstack`, `pagerduty` (add new in styles.css if needed).

### Update Profile Photo

Replace `static/profile.jpeg`. Displayed as 280x280px circular image.

### Update Downloadable CV

Replace `static/cv.pdf`.

## Technical Constraints

- **No build system** - Direct file editing only
- **No package manager** - No npm, yarn, or dependencies
- **No frameworks** - Vanilla HTML/CSS/JS only
- **No icon libraries** - All icons are inline SVG
- **External font** - Inter font from Google Fonts (already loaded in `<head>`)
- **Print styles** - Included for PDF export (`@media print` in styles.css)

## Responsive Design

Single breakpoint:
- **Desktop:** Default styles
- **Mobile:** `@media (max-width: 768px)` - Single column, hamburger menu, adjusted spacing

## External Links

All external links use `target="_blank"`:
- Company links in experience timeline
- Certification verification links
- Education institution link
- LinkedIn profile
- Email (uses `mailto:`)

## Deployment Notes

**AWS Infrastructure:**
- S3 bucket: murygin.dev
- Region: eu-west-2 (London)
- CloudFront distribution (ID in GitHub secrets)

**GitHub Secrets Required:**
- `AWS_ACCESS_KEY_ID`
- `AWS_SECRET_ACCESS_KEY`
- `CLOUDFRONT_DISTRIBUTION_ID`

**Files excluded from deployment:** `.git/*`, `.github/*`, `*.md`

## Color Theme

All colors defined as CSS variables in styles.css:
- Primary blue: `#2563eb`
- Primary dark blue: `#1d4ed8`
- Gradient: Blue (#2563eb) to purple (#7c3aed) at 135deg
- White background with light gray alternate (`#f8fafc`)
- Dark text (`#1e293b`) with gray secondary (`#64748b`)

To change theme: edit `:root` variables in styles.css (lines 1-15).
