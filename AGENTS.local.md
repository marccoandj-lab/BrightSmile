# AGENTS.md - Developer Guide for BrightSmile Dental Clinic Website

## Project Overview

- **Project Name**: BrightSmile Dental Clinic Website
- **Type**: Marketing/Business Website
- **Framework**: Next.js 16.1.6 (App Router)
- **Language**: TypeScript 5
- **Styling**: Tailwind CSS 4 with custom design system
- **Animations**: Framer Motion 12.34.0
- **UI Components**: Custom components with Lucide React icons

## Tech Stack

### Core Dependencies
- **React**: 19.2.3
- **Next.js**: 16.1.6 (using App Router architecture)
- **TypeScript**: 5
- **Tailwind CSS**: 4 with PostCSS
- **Framer Motion**: 12.34.0 (for animations)
- **Lucide React**: 0.563.0 (icon library)
- **clsx + tailwind-merge**: For conditional class merging (via `cn()` utility)

### Dev Dependencies
- **ESLint**: 9 with Next.js config
- **TypeScript**: Strict mode enabled
- **PostCSS**: @tailwindcss/postcss v4

## Project Structure

### Directory Organization
```
src/
├── app/                    # Next.js App Router pages
│   ├── layout.tsx         # Root layout with Header/Footer
│   ├── page.tsx           # Homepage
│   ├── globals.css        # Global styles and design tokens
│   ├── about/             # About page
│   ├── contact/           # Contact page
│   ├── services/          # Services page
│   ├── team/              # Team page
│   ├── faq/               # FAQ page
│   ├── privacy/           # Privacy policy
│   ├── terms/             # Terms of service
│   └── cookies/           # Cookie policy
├── components/
│   ├── layout/            # Layout components (Header, Footer)
│   ├── sections/          # Page sections (Hero, ServicesPreview)
│   ├── providers/         # React context providers (theme)
│   └── ui/                # Reusable UI components (theme-toggle)
└── lib/
    └── utils.ts           # Utility functions (cn helper)

public/
├── hero-video.mp4         # Hero section background video
└── *.svg                  # Icon assets
```

## Design System

### Color Palette (defined in globals.css)

**Primary (Deep Navy/Slate)**
- Used for text, backgrounds, and structural elements
- Range: `--primary-50` to `--primary-950`

**Accent (Soft Teal)**
- Primary brand color for CTAs and highlights
- Main value: `--accent-500: #14b8a6`
- Range: `--accent-50` to `--accent-900`

**CTA (Warm Coral)**
- Secondary accent for call-to-action elements
- Main value: `--cta-500: #f43f5e`
- Range: `--cta-50` to `--cta-700`

### Theme Support
- Light and dark mode supported via `ThemeProvider`
- Theme persisted to localStorage
- Respects system preference on first visit
- CSS custom properties automatically switch in dark mode

### Typography
- **Primary Font**: Geist Sans (via next/font/google)
- **Mono Font**: Geist Mono (via next/font/google)
- Font variables: `--font-geist-sans`, `--font-geist-mono`
- Display: swap (for performance)

### Custom CSS Classes (in globals.css)
- `.text-gradient` - Accent color gradient text
- `.text-gradient-cta` - CTA color gradient text
- `.bg-gradient-subtle` - Subtle background gradient
- `.glass` - Glassmorphism effect (backdrop blur)
- `.card-premium` - Premium card styling with hover effects
- `.btn-primary` - Primary button styling

## Key Conventions

### File Naming
- React components: PascalCase (e.g., `Header.tsx`, `ServicesPreview.tsx`)
- Utility files: camelCase (e.g., `utils.ts`)
- Pages: lowercase (Next.js convention, e.g., `page.tsx`)
- CSS: kebab-case for custom properties (e.g., `--primary-500`)

### Component Structure
- Use `"use client"` directive for client components (animations, interactivity)
- Server components by default (e.g., `layout.tsx`)
- Destructure props in function parameters
- Use TypeScript interfaces for prop types

### Styling Patterns
- Use Tailwind utility classes as primary styling method
- Use `cn()` utility from `@/lib/utils` for conditional classes
- Custom CSS properties for color tokens
- Responsive design: mobile-first with `sm:`, `md:`, `lg:`, `xl:` breakpoints

### Import Aliases
- `@/*` maps to `./src/*` (configured in tsconfig.json)
- Always use path aliases for imports: `@/components/...`, `@/lib/...`

### Animation Patterns
- Use Framer Motion for complex animations
- Common patterns:
  - `initial`, `animate`, `transition` props for entrance animations
  - `whileInView` with `viewport={{ once: true }}` for scroll animations
  - Stagger children with delay: `transition={{ delay: index * 0.1 }}`

## Development Workflow

### Running the Project
```bash
npm run dev      # Start development server (http://localhost:3000)
npm run build    # Build for production
npm run start    # Start production server
npm run lint     # Run ESLint
```

### TypeScript Configuration
- **Strict mode enabled**: All strict type checking rules active
- **Target**: ES2017
- **Module resolution**: bundler
- **JSX**: react-jsx (automatic runtime)
- **Path aliases**: `@/*` → `./src/*`

### ESLint Configuration
- Uses `eslint-config-next` presets
- Configured in `eslint.config.mjs` (flat config)
- Ignores: `.next/`, `out/`, `build/`, `next-env.d.ts`

## Component Patterns

### Layout Components
- **Header**: Fixed position, glassmorphism on scroll, responsive mobile menu
- **Footer**: Four-column layout with branding, links, contact, and hours
- Both use consistent branding (BrightSmile logo with Stethoscope icon)

### Section Components
- **Hero**: Full-screen video background with overlay, animated content, stats, floating badges
- **ServicesPreview**: Grid of service cards with icons, hover effects, and links

### Provider Pattern
- `ThemeProvider` wraps app in root layout
- Provides `theme`, `toggleTheme`, `setTheme` via context
- Use `useTheme()` hook to access theme state

### UI Component Pattern
- Export named functions (not default)
- Include proper TypeScript types
- Handle hydration mismatches (see `ThemeToggle` placeholder pattern)

## Best Practices

### Performance
- Use Next.js Image component for images (currently using img tags - room for optimization)
- Optimize fonts with `next/font` (already implemented)
- Use `viewport={{ once: true }}` for animations to prevent re-triggering
- Video has `autoPlay`, `loop`, `muted`, `playsInline` for mobile compatibility

### Accessibility
- Include `aria-label` on icon-only buttons
- Use semantic HTML elements
- Maintain color contrast ratios
- Support keyboard navigation

### SEO
- Define metadata in `layout.tsx`
- Include title, description, and keywords
- Use semantic HTML structure
- Implement proper heading hierarchy

### Code Organization
- Keep components focused and single-purpose
- Extract reusable logic to utilities
- Use constants for repeated data (e.g., `navLinks`, `services`)
- Separate layout, section, and UI components

### Styling Guidelines
- Prefer Tailwind utilities over custom CSS when possible
- Use design tokens (CSS custom properties) for colors
- Maintain consistent spacing scale (Tailwind's spacing)
- Use rounded corners: `rounded-xl`, `rounded-2xl`, `rounded-3xl`, `rounded-full`
- Shadow hierarchy: `shadow-lg`, `shadow-xl`, `shadow-2xl`

### State Management
- Use React Context for global state (theme)
- Use local state for component-specific state
- Persist important state to localStorage when appropriate

## Common Patterns

### Conditional Class Names
```tsx
import { cn } from "@/lib/utils";

<div className={cn(
  "base-classes",
  condition && "conditional-classes",
  "more-classes"
)} />
```

### Scroll-based Styling
```tsx
const [scrolled, setScrolled] = useState(false);

useEffect(() => {
  const handleScroll = () => setScrolled(window.scrollY > 20);
  window.addEventListener("scroll", handleScroll);
  return () => window.removeEventListener("scroll", handleScroll);
}, []);
```

### Framer Motion Entrance Animation
```tsx
<motion.div
  initial={{ opacity: 0, y: 30 }}
  animate={{ opacity: 1, y: 0 }}
  transition={{ duration: 0.6, delay: 0.1 }}
>
  {content}
</motion.div>
```

### Framer Motion Scroll Animation
```tsx
<motion.div
  initial={{ opacity: 0, y: 20 }}
  whileInView={{ opacity: 1, y: 0 }}
  viewport={{ once: true }}
  transition={{ delay: 0.1 }}
>
  {content}
</motion.div>
```

### Hydration-Safe Client Components
```tsx
const [mounted, setMounted] = useState(false);

useEffect(() => {
  setMounted(true);
}, []);

if (!mounted) {
  return <div className="placeholder" />;
}
```

## Design Patterns to Follow

### Button Styles
- **Primary CTA**: `bg-accent-500 text-white rounded-full px-8 py-4 hover:bg-accent-600`
- **Secondary CTA**: `bg-white/10 backdrop-blur-sm border border-white/30 rounded-full`
- **Link Button**: `text-accent-600 font-medium flex items-center gap-1`

### Card Styles
- Use `card-premium` class for elevated cards
- Include hover effects: `hover:shadow-xl transition-all`
- Border: `border border-primary-100`
- Rounded corners: `rounded-xl` or `rounded-2xl`

### Icon Pattern
```tsx
import { IconName } from "lucide-react";

<div className="w-12 h-12 bg-gradient-to-br from-accent-500 to-accent-600 rounded-xl flex items-center justify-center text-white">
  <IconName size={24} />
</div>
```

### Badge Pattern
```tsx
<div className="inline-flex items-center gap-2 bg-accent-100 px-4 py-2 rounded-full">
  <span className="w-2 h-2 rounded-full bg-accent-500" />
  <span className="text-sm font-semibold text-accent-700">Label</span>
</div>
```

## Known Patterns in Codebase

### Navigation
- Fixed header that becomes glass/blurred on scroll
- Mobile menu with AnimatePresence for smooth transitions
- Consistent "Book Now" CTA in header

### Hero Section
- Full-screen video background with gradient overlay
- Animated entrance for all elements with staggered delays
- Stats row with large numbers
- Floating badges in corners
- Scroll indicator at bottom

### Content Sections
- Consistent padding: `py-24 lg:py-32 px-6`
- Max width container: `max-w-7xl mx-auto`
- Section badges with dot indicator
- Gradient text for emphasis: `text-gradient` or `text-gradient-cta`

## Potential Improvements

### Performance Optimizations
- Replace `<img>` tags with Next.js `<Image>` component
- Add lazy loading for below-fold images
- Optimize video file size or provide multiple formats
- Consider static generation for all pages

### Accessibility Enhancements
- Add skip-to-content link
- Ensure all interactive elements have focus styles
- Test with screen readers
- Add alt text to all images

### SEO Enhancements
- Add individual page metadata (currently only in root layout)
- Implement structured data (JSON-LD) for local business
- Add OpenGraph and Twitter Card meta tags
- Create sitemap and robots.txt

### Code Quality
- Add unit tests for utility functions
- Add component testing
- Add E2E tests for critical user flows
- Implement error boundaries

## Important Notes

### Client vs Server Components
- **Client components** (`"use client"`): Header, Footer, Hero, ServicesPreview, ThemeProvider, ThemeToggle, Homepage
- **Server components**: Root layout (default)
- Use client components when you need: hooks, event handlers, browser APIs, or Framer Motion

### Hydration Considerations
- Theme toggle includes hydration-safe pattern (placeholder before mount)
- ThemeProvider manages theme before and after hydration
- `suppressHydrationWarning` on `<html>` tag for theme class

### Responsive Design
- Mobile-first approach
- Breakpoints: `sm: 640px`, `md: 768px`, `lg: 1024px`, `xl: 1280px`
- Header switches to hamburger menu below `lg` breakpoint
- Grid layouts adapt: `grid-cols-1 md:grid-cols-2 lg:grid-cols-4`

### External Resources
- Uses Unsplash images (should be replaced with optimized local assets)
- Font loaded from Google Fonts (optimized via next/font)
- Video served from `/public` directory

## Quick Reference

### Adding a New Page
1. Create folder in `src/app/[page-name]/`
2. Add `page.tsx` with default export function
3. Add navigation link to `navLinks` array in `Header.tsx`
4. Add link to footer navigation in `Footer.tsx`

### Adding a New Component
1. Create file in appropriate `src/components/` subdirectory
2. Export named function (e.g., `export function MyComponent()`)
3. Add `"use client"` directive if using client features
4. Import using path alias: `@/components/...`

### Modifying Theme Colors
1. Update CSS custom properties in `src/app/globals.css`
2. Update both `:root` (light mode) and `.dark` (dark mode) sections
3. Follow existing naming convention: `--color-shade`

### Adding Animations
1. Import required components from `framer-motion`
2. Use `initial`, `animate`, `transition` for mount animations
3. Use `whileInView` with `viewport={{ once: true }}` for scroll animations
4. Stagger children with `delay: index * 0.1`

---

**Last Updated**: February 10, 2026
**Project Version**: 0.1.0
