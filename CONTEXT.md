# Website Development Context

This document provides context for AI assistants to understand the website structure and make changes.

## Project Overview

**Website:** Maxim Murygin - Personal CV / Portfolio  
**Domain:** murygin.dev  
**Type:** Static HTML/CSS/JS website  
**Data Source:** LinkedIn data export (`export/` directory)

## Key Files

| File | Purpose |
|------|---------|
| `index.html` | Main HTML structure with all sections (~580 lines) |
| `styles.css` | All CSS styling including responsive design (~950 lines) |
| `script.js` | Animations, navigation, scroll effects (~170 lines) |
| `export/*.csv` | LinkedIn data export (source data) |

## Website Sections

1. **Hero** (lines 32-60) - Name, title, location, profile photo, CTAs
2. **About** (lines 64-88) - Professional summary with stats
3. **Experience** (lines 92-282) - Career timeline with achievements
4. **Skills** (lines 286-405) - Categorized skills grid
5. **Certifications** (lines 409-461) - Clickable certification cards
6. **Education** (lines 465-480) - University info
7. **Languages** (lines 482-505) - Language proficiency bars
8. **Recommendations** (lines 509-539) - Professional testimonials
9. **Contact** (lines 543-564) - Email and LinkedIn links

## Data Sources (LinkedIn Export)

| File | Content Used |
|------|--------------|
| `export/Profile.csv` | Name, headline, summary, location |
| `export/Positions.csv` | Work experience (company, title, description, dates) |
| `export/Education.csv` | University, degree, dates |
| `export/Skills.csv` | Technical and soft skills list |
| `export/Certifications.csv` | Certification names, URLs, authorities, dates |
| `export/Languages.csv` | Language proficiencies |
| `export/Recommendations_Received.csv` | Professional recommendations |

## Static Assets

| Path | Content |
|------|---------|
| `static/profile.jpeg` | Profile photo (circular avatar in hero) |
| `static/cv.pdf` | Downloadable CV |
| `static/openstack-coa.pdf` | OpenStack certification PDF |

## CSS Architecture

### CSS Variables (`:root`)
```css
--primary: #2563eb;           /* Main blue */
--primary-dark: #1d4ed8;      /* Hover state */
--gradient: linear-gradient(135deg, #2563eb 0%, #7c3aed 100%);
--background: #ffffff;
--background-alt: #f8fafc;    /* Alternating sections */
--text: #1e293b;
--text-secondary: #64748b;
--border: #e2e8f0;
--radius: 12px;
```

### Key CSS Classes

| Class | Purpose |
|-------|---------|
| `.timeline-item` | Experience entry with marker and content |
| `.timeline-marker` | Blue dot on timeline |
| `.skill-category` | Grouped skills with icon header |
| `.skill-tag` | Individual skill pill |
| `.cert-card` | Clickable certification card (`<a>` tag) |
| `.cert-logo` | Colored logo placeholder (aws, redhat, openstack, pagerduty) |
| `.education-card` | University info with icon |
| `.language-card` | Language with progress bar |
| `.recommendation-card` | Quote-style testimonial |
| `.hero-avatar` | Profile image container with pulse animation |
| `.avatar-image` | Circular profile photo |
| `.section-alt` | Alternating background color |

## JavaScript Functions

| Function | Purpose |
|----------|---------|
| Mobile nav toggle | Hamburger menu for mobile |
| Smooth scroll | Navigation links with header offset (80px) |
| Intersection Observer | Fade-in animations on scroll |
| `animateStats()` | Counter animation for stat numbers |
| Progress bar animation | Language bars animate on scroll |
| Active nav highlighting | Updates nav based on scroll position |
| Typing effect | Hero title typewriter animation |

## External Links

All external links use `target="_blank"`:

| Element | URL |
|---------|-----|
| Booking.com | https://www.booking.com |
| Rubius | https://rubius.com |
| TPU (Education) | https://tpu.ru/en |
| AWS Certs | youracclaim.com/badges/... |
| Red Hat Certs | redhat.com/rhtapps/services/certifications/badge/verify/... |
| OpenStack COA | coa.edu.mirantis.com/verify/... |
| PagerDuty Cert | verify.skilljar.com/c/... |
| LinkedIn | linkedin.com/in/mmurygin |
| Email | mailto:muriginm@gmail.com |

## Common Changes

### Update work experience
Edit timeline items in `index.html` (lines 92-282). Each position follows this structure:
```html
<div class="timeline-item">
    <div class="timeline-marker"></div>
    <div class="timeline-content">
        <div class="timeline-header">
            <h3>Job Title</h3>
            <a href="URL" target="_blank" class="company">Company</a>
            <span class="period">Start - End</span>
            <span class="location">City, Country</span>
        </div>
        <p class="timeline-description">Description</p>
        <ul class="achievements">
            <li>Achievement 1</li>
        </ul>
        <div class="tech-stack">
            <span class="tech-tag">Technology</span>
        </div>
    </div>
</div>
```

### Add new skill
Add to appropriate `.skill-category` in `index.html`:
```html
<span class="skill-tag">New Skill</span>
```

### Add new certification
Add to `.certs-grid` in `index.html`:
```html
<a href="VERIFICATION_URL" target="_blank" class="cert-card">
    <div class="cert-logo PROVIDER">XX</div>
    <h3>Certification Name</h3>
    <p class="cert-issuer">Issuing Authority</p>
    <p class="cert-date">Month Year</p>
</a>
```
For `.cert-logo`, use: `aws`, `redhat`, `openstack`, or `pagerduty` (or add new in CSS).

### Update profile photo
Replace `static/profile.jpeg`. Image is displayed as 280x280px circle.

### Update stats
Edit `.stat` elements in About section (lines 74-86):
```html
<div class="stat">
    <span class="stat-number">10+</span>
    <span class="stat-label">Years Experience</span>
</div>
```

### Change colors
Edit CSS variables in `styles.css` `:root` selector (lines 1-15).

## Responsive Breakpoints

- **Desktop:** Default styles
- **Mobile:** `@media (max-width: 768px)` - Single column, hamburger menu

## Build System

**None required** - This is a static site with no build step. Just edit files and commit.

## Local Development

```bash
cd /home/mmurygin/pr/murygin.dev
python3 -m http.server 8000
# Open http://localhost:8000
```

## Important Notes

- No frameworks used (vanilla HTML/CSS/JS)
- Google Fonts: Inter (loaded via `<link>` in head)
- All icons are inline SVGs (no icon library)
- Certifications are `<a>` tags (clickable cards)
- Company names in experience are `<a>` tags with links
- Print styles included for PDF export
- `.gitignore` excludes `.windsurf` directory
