# Meadowlark Endocrinology Website Specification

## Overview
Informational website for a new private endocrinology practice with patient inquiry form and link to external EHR patient portal.

## Technology Stack
- **Framework:** Astro (static site generator with component architecture)
- **Build Tool:** Vite (included with Astro - fast dev server, HMR, optimized builds)
- **Styling:** Tailwind CSS (utility-first CSS framework)
- **Hosting:** Netlify
- **Form Handling:** Netlify Forms (email notifications to practice)
- **Build Output:** Static HTML (no client-side JavaScript shipped)

## Site Structure

### Pages
1. **Why Choose Us** (`src/pages/index.astro`) - homepage
2. **About Membership** (`src/pages/about-membership.astro`)
3. **Become a Member** (`src/pages/become-a-member.astro`) - contains inquiry form

### Navigation (single level)
| Position | Label | Link |
|----------|-------|------|
| 1 | Why Choose Us | Internal page |
| 2 | About Membership | Internal page |
| 3 | Become a Member | Internal page |
| 4 (rightmost) | Current Patient | External: Praxis EHR portal (placeholder URL) |

## Page Layout (consistent across all pages)

```
┌─────────────────────────────────────┐
│            HEADER                   │
│  (Logo / Practice Name)             │
├─────────────────────────────────────┤
│            NAV BAR                  │
│  Why Choose Us | About | Become | Current Patient →
├─────────────────────────────────────┤
│                                     │
│         CONTENT SECTION             │
│    (Page-specific content)          │
│                                     │
├─────────────────────────────────────┤
│            FOOTER                   │
│  (Contact info, address, hours)     │
└─────────────────────────────────────┘
```

## Become a Member Form Fields

| Field | Type | Required |
|-------|------|----------|
| Name | text | Yes |
| Address | text/textarea | Yes |
| Phone | tel | Yes |
| Email | email | Yes |
| Patient Specifics | textarea | No |

Form submits via Netlify Forms → email notification to practice.

## Branding

- **Practice Name:** Meadowlark Endocrinology
- **Color Palette** (configured in `tailwind.config.mjs`):
  ```js
  colors: {
    primary: {
      DEFAULT: '#fc6f03',  // Orange
      dark: '#a34802',
      light: '#fa974b',
    },
    accent: {
      DEFAULT: '#5279b7',  // Blue
      light: '#7f93b3',
    },
    background: {
      DEFAULT: '#f8f9fa',
      light: '#ffffff',
    },
  }
  ```
  Usage: `bg-primary`, `text-accent`, `hover:bg-primary-dark`, etc.
- **Typography:** Clean, readable sans-serif fonts (system font stack or Google Fonts)
- **Logo:** To be designed (text-based initially, or with meadowlark bird icon)

## File Structure (Astro + Tailwind)

```
/
├── astro.config.mjs              # Astro configuration (includes Tailwind integration)
├── tailwind.config.mjs           # Tailwind config (custom colors, fonts)
├── package.json
├── public/
│   └── images/                   # Static assets (logo, images)
├── src/
│   ├── components/
│   │   ├── Header.astro          # Logo / Practice name
│   │   ├── NavBar.astro          # Navigation links
│   │   ├── Footer.astro          # Contact info, address, hours
│   │   └── MemberForm.astro      # Become a Member form
│   ├── layouts/
│   │   └── BaseLayout.astro      # Shared layout (header, nav, content slot, footer)
│   ├── pages/
│   │   ├── index.astro           # Why Choose Us (homepage)
│   │   ├── about-membership.astro
│   │   └── become-a-member.astro
│   └── styles/
│       └── global.css            # Tailwind directives (@tailwind base, etc.)
└── netlify.toml                  # Netlify build configuration
```

## Components

| Component | Purpose |
|-----------|---------|
| `BaseLayout.astro` | Wraps all pages with header, nav, content slot, footer |
| `Header.astro` | Practice logo and name |
| `NavBar.astro` | Single-level navigation with "Current Patient" external link |
| `Footer.astro` | Contact info, address, office hours |
| `MemberForm.astro` | Patient inquiry form with Netlify Forms integration |

## Implementation Steps

0. **Save specification** - Copy this plan to `SPECIFICATION.md` in project directory
1. **Initialize Astro project** - `npm create astro@latest`
2. **Add Tailwind integration** - `npx astro add tailwind`
3. **Configure Tailwind** - Add custom colors to `tailwind.config.mjs`
4. **Create components:**
   - `Header.astro` - Practice logo/name
   - `NavBar.astro` - Navigation with external portal link
   - `Footer.astro` - Contact info
   - `MemberForm.astro` - Patient inquiry form
5. **Create BaseLayout.astro** - Compose components with content slot
6. **Build pages:**
   - `index.astro` - Why Choose Us (homepage)
   - `about-membership.astro` - Membership information
   - `become-a-member.astro` - Uses MemberForm component
7. **Configure Netlify Forms** - Add form attributes for Netlify detection
8. **Add netlify.toml** - Build configuration
9. **Test locally** - `npm run dev`
10. **Deploy to Netlify** - Connect Git repo or CLI deploy

## Verification

**Local Development:**
- [ ] `npm run dev` starts dev server without errors
- [ ] All pages load at localhost:4321
- [ ] Navigation works between all pages
- [ ] "Current Patient" link opens external portal in new tab
- [ ] Responsive design works on mobile/tablet/desktop

**Build & Deploy:**
- [ ] `npm run build` completes without errors
- [ ] `npm run preview` serves production build correctly
- [ ] Deploy to Netlify succeeds
- [ ] Form submission sends email notification (test on deployed site)

**Accessibility:**
- [ ] Semantic HTML (header, nav, main, footer elements)
- [ ] Alt text on images
- [ ] Keyboard navigation works

## Future Considerations (not in initial scope)
- Blog section (Astro has built-in content collections for this)
- Praxis EHR deep integration (if API available)
- Online appointment scheduling
- Headless CMS integration (Astro supports many: Contentful, Sanity, etc.)
