# murygin.dev

Personal portfolio website for Maxim Murygin — Senior Site Reliability Engineer.

## Overview

A modern, responsive single-page portfolio showcasing professional experience, skills, certifications, and contact information. Built with vanilla HTML, CSS, and JavaScript.

**Live site:** [murygin.dev](https://murygin.dev)

## Features

- **Responsive Design** — Mobile-first approach with smooth transitions
- **Modern UI** — Clean layout with gradient accents and subtle animations
- **Smooth Scrolling** — Navigation with scroll-aware highlighting
- **Intersection Observer Animations** — Fade-in effects as sections come into view
- **Print Styles** — Optimized for PDF/print output
- **No Build Step** — Pure HTML/CSS/JS, no dependencies

## Sections

- **Hero** — Introduction with profile photo and CTAs
- **About** — Professional summary
- **Experience** — Career timeline (Booking.com, Rubius)
- **Skills** — Infrastructure, programming, monitoring, databases, practices
- **Certifications** — AWS, Red Hat, OpenStack, PagerDuty
- **Education** — Tomsk Polytechnic University
- **Recommendations** — Professional endorsements
- **Contact** — Email and LinkedIn links

## Tech Stack

| Layer | Technology |
|-------|------------|
| Markup | HTML5 |
| Styling | CSS3 (custom properties, flexbox, grid) |
| Interactivity | Vanilla JavaScript (ES6+) |
| Fonts | Inter (Google Fonts) |

## Project Structure

```
murygin.dev/
├── index.html      # Main HTML file
├── styles.css      # All styles
├── script.js       # Animations and interactions
├── static/
│   ├── profile.jpeg
│   ├── cv.pdf
│   └── openstack-coa.pdf
└── old-cv-site/    # Previous version (archived)
```

## Local Development

Simply open `index.html` in a browser, or serve with any static file server:

```bash
# Python
python -m http.server 8000

# Node.js
npx serve .
```

## License

© 2025 Maxim Murygin. All rights reserved.
