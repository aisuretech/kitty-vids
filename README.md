# Kitty Vids: Pet Video Gallery & Encyclopedia Platform

A modern, headless CMS-powered web platform for pet video discovery and educational content, built with Next.js 16, Keystatic, and YouTube API integration.

Kitty Vids is a production-ready template for creating multi-tenant pet communities with video galleries, encyclopedia guides, and content management—supporting both cat and dog themes with zero vendor lock-in.

## Live Demo
- Production: https://www.kitty-vids.com

<!-- Use absolute production URLs for README images (https://...), not relative paths. -->
![Kitty Vids Pet Community Hub](https://www.kitty-vids.com/images/cat-community-hero.png)

## Why This Project Is Discoverable on GitHub
- **Next.js 16 with Turbopack**: Modern React framework with fastest bundler—ideal for developers learning high-performance SSR patterns
- **Keystatic CMS Integration**: File-based, Git-native content management—no database required, version control built-in
- **Multi-Tenant Ready**: Single codebase supports both cat and dog themes via environment variables—template for scaling
- **YouTube Data API v3**: Production patterns for external API integration, caching, and server-side data fetching in Next.js

## Table of Contents
- [Features](#features)
- [Tech Stack](#tech-stack)
- [Quick Start](#quick-start)
- [Project Structure](#project-structure)
- [Environment Variables](#environment-variables)
- [Architecture](#architecture)
- [Learning Modules](#learning-modules)
- [Deployment](#deployment)
- [SEO and Performance](#seo-and-performance)
- [Screenshots](#screenshots)
- [Use Cases](#use-cases)
- [Roadmap](#roadmap)
- [Contributing](#contributing)
- [FAQ](#faq)
- [Suggested GitHub Topics](#suggested-github-topics)
- [Links](#links)
- [License](#license)

## Features

### For Learners & Content Consumers
- **Video Gallery with Smart Filtering**: Browse YouTube cat/dog videos by tags, trending, or categories—learn pet care through multimedia
- **Encyclopedia Guides**: Comprehensive, searchable guides on pet behavior, health, training, and nutrition managed via headless CMS
- **Responsive Design**: Mobile-first interface built with Tailwind CSS—optimized for all screen sizes
- **Tag-Based Discovery**: Organize and filter videos/articles by topic, difficulty, and audience (e.g., "beginner", "health", "training")

### For Developers & Content Managers
- **Keystatic Admin UI**: Git-backed CMS—manage guides and images without database migrations or API complexity
- **Type-Safe Content**: Full TypeScript support for content schemas with autocomplete and validation
- **API Routes Ready**: Extensible Next.js API structure for custom endpoints, webhooks, and third-party integrations
- **Multi-Tenant Architecture**: Environment-based theme switching (cats/dogs)—single deployment serves multiple brands

## Tech Stack
- **Frontend**: React 19, TypeScript, Tailwind CSS, Markdoc, react-markdown
- **Runtime/Platform**: Next.js 16 (Turbopack), Node.js 18+
- **Analytics and Monitoring**: Sitemap generation (next/sitemap), robots.txt, structured data ready
- **Testing**: ESLint 9 (configured), TypeScript compiler checks
- **PWA**: Static site generation (SSG) with ISR (Incremental Static Regeneration)

## Quick Start

### Prerequisites
- Node.js 18 or higher ([install](https://nodejs.org))
- YouTube Data API v3 key ([get it free](https://console.cloud.google.com/apis/credentials))
- Git (for Keystatic CMS)

### Install and Run
```bash
# Clone the repository
git clone https://github.com/aisuretech/kitty-vids.git
cd cat

# Install dependencies
npm install

# Set up environment variables
cp .env.example .env.local
# Edit .env.local and add your YOUTUBE_API_KEY

# Start development server
npm run dev
```

Open http://localhost:3000 in your browser.

### Build and Validate
```bash
# Type check and lint
npm run lint

# Build for production
npm run build

# Run production build locally
npm start
```

## Project Structure
```text
cat/
├── public/
│   ├── images/
│   │   └── guides/
│   │       ├── cats/          # Cat guide images
│   │       └── dogs/          # Dog guide images
│   ├── favicon.ico
│   └── robots.txt
├── src/
│   ├── app/
│   │   ├── page.tsx           # Home page
│   │   ├── layout.tsx         # Root layout
│   │   ├── globals.css        # Global styles
│   │   ├── theme.css          # Theme variables
│   │   ├── sitemap.ts         # Dynamic sitemap generation
│   │   ├── robots.ts          # Robots.txt configuration
│   │   ├── guides/
│   │   │   ├── page.tsx       # All guides listing
│   │   │   └── [slug]/        # Dynamic guide detail pages
│   │   ├── videos/            # Video gallery page
│   │   ├── categories/        # Category browsing
│   │   ├── popular/           # Popular content
│   │   ├── about/
│   │   ├── faq/
│   │   ├── contact/
│   │   ├── privacy/
│   │   ├── terms/
│   │   ├── cookies/
│   │   ├── dmca/
│   │   ├── keystatic/         # CMS admin panel
│   │   └── api/
│   │       └── keystatic/     # Keystatic API endpoints
│   ├── components/
│   │   ├── Header.tsx         # Navigation
│   │   ├── Footer.tsx
│   │   ├── GuideCard.tsx      # Guide list item
│   │   ├── VideoCard.tsx      # Video thumbnail
│   │   ├── MarkdocRenderer.tsx
│   │   ├── CategoryFilter.tsx
│   │   ├── TagCloud.tsx
│   │   └── LoadingSkeleton.tsx
│   ├── content/
│   │   └── guides/
│   │       ├── cats/          # Cat encyclopedia (markdown)
│   │       └── dogs/          # Dog encyclopedia (markdown)
│   ├── lib/
│   │   ├── reader.ts          # Content file reader
│   │   ├── youtube.ts         # YouTube API client
│   │   └── theme.ts           # Theme utilities
│   └── types/
│       └── youtube.ts         # YouTube API types
├── config/
│   └── site.config.ts         # Site metadata
├── keystatic.config.ts        # CMS schema and configuration
├── next.config.ts
├── tsconfig.json
├── tailwind.config.ts
├── eslint.config.mjs
├── postcss.config.mjs
├── package.json
└── .env.example
```

## Environment Variables
Create a `.env.local` file in the project root:

```env
# YouTube Data API key (required)
# Get it from: https://console.cloud.google.com/apis/credentials
YOUTUBE_API_KEY=your_youtube_api_key_here

# Site theme: 'cat' or 'dog' (optional, defaults to 'cat')
SITE_THEME=cat
```

**Development theme testing:**
```bash
# Use cat theme
cp .env.cat .env.local && npm run dev

# Use dog theme
cp .env.dog .env.local && npm run dev
```

## Architecture

Kitty Vids follows a hybrid static + dynamic generation pattern optimized for content discovery:

1. **Content Layer**: Encyclopedia guides stored as markdown in Git (`src/content/guides/cats`, `src/content/guides/dogs`)—read at build time via `reader.ts`
2. **CMS Layer**: Keystatic admin UI (`/keystatic`) provides Git-backed content management—changes committed to repository
3. **Video Layer**: YouTube API integration fetches video metadata server-side—cached and paginated for performance
4. **Presentation Layer**: React 19 components with TypeScript render guides, videos, and category pages—Tailwind CSS styling
5. **Deployment**: Static HTML generated at build time (SSG/ISR) deployed to Vercel—zero runtime database

```text
┌─────────────────────────────────────────────────────────────┐
│                    User Browser                             │
│                   (Client-side)                             │
└──────────────────────┬──────────────────────────────────────┘
                       │
                       ▼
┌─────────────────────────────────────────────────────────────┐
│                  Next.js 16 (Vercel)                        │
│  ┌──────────────────────────────────────────────────────┐  │
│  │  Pages (SSG + ISR)                                   │  │
│  │  • /guides/[slug]     → Rendered at build time       │  │
│  │  • /videos            → Dynamic with caching         │  │
│  │  • /categories        → Tag-based filtering          │  │
│  └──────────────────────────────────────────────────────┘  │
│  ┌──────────────────────────────────────────────────────┐  │
│  │  API Routes                                          │  │
│  │  • /api/keystatic/... → CMS backend                  │  │
│  └──────────────────────────────────────────────────────┘  │
└──────────┬──────────────────────────────┬──────────────────┘
           │                              │
           ▼                              ▼
    ┌─────────────────┐            ┌──────────────────┐
    │   Git Repo      │            │  YouTube API v3  │
    │  (Keystatic)    │            │    (External)    │
    │  src/content/   │            │                  │
    │  guides/        │            │  • Search videos │
    │                 │            │  • Get metadata  │
    └─────────────────┘            │  • Cache results │
                                   └──────────────────┘
```

## Learning Modules

This project is excellent for learning:

- **Next.js 16 Patterns**: Server components, ISR, API routes, dynamic routing with `[slug]`
- **CMS Integration**: Keystatic for file-based content management in Git workflows
- **TypeScript Best Practices**: Strict mode, content type schemas, API type safety
- **React 19 Features**: Server components, suspense boundaries, concurrent rendering
- **External API Integration**: YouTube API pagination, caching strategies, error handling
- **SEO for Next.js**: Dynamic sitemap generation, robots.txt, Open Graph metadata

## Deployment

**Recommended deployment target**: Vercel (optimized for Next.js)

```bash
# Build locally to verify
npm run build

# Push to GitHub
git add .
git commit -m "Deploy to Vercel"
git push origin main
```

**Deploy to Vercel:**
1. Go to [vercel.com](https://vercel.com)
2. Import this repository
3. Add environment variable: `YOUTUBE_API_KEY` in project settings
4. Deploy—Vercel will auto-detect Next.js and use optimal build settings

**Production URL:**
- https://www.kitty-vids.com

**Other supported platforms:**
- Self-hosted: `npm run build && npm start` (Node.js 18+)
- Docker: `docker build -t kitty-vids . && docker run -p 3000:3000 -e YOUTUBE_API_KEY=xxx kitty-vids`

## SEO and Performance

- **Dynamic Sitemap**: Automatically generated at `/sitemap.xml`—includes all guides and pages for search engine discovery
- **Robots.txt**: Configured for optimal crawl patterns and exclusions
- **Static Generation**: Encyclopedia guides pre-rendered as HTML at build time—instant page loads, zero JavaScript
- **Image Optimization**: Next.js Image component caching—automatic format selection (WebP, AVIF)
- **Markdown to HTML**: Markdoc parser converts guides to semantic HTML—improves readability and SEO
- **Structured Data**: Open Graph meta tags ready for social sharing and rich snippets

## Screenshots
<!-- Use absolute production URLs for all screenshot images (https://...), not ./assets paths. -->

| Feature | Preview |
|---------|---------|
| Home & Video Gallery | ![](https://www.kitty-vids.com/images/guides/cats/cat-nutrition-101-feeding-for-long-term-health/preview.png) |
| Encyclopedia Guide | ![](https://www.kitty-vids.com/images/guides/cats/understanding-cat-body-language-what-your-feline-is-really-saying/preview.png) |

## Use Cases

- **Pet Education Platform**: Build a community site for pet owners to learn care, training, and health topics
- **YouTube Content Hub**: Curate and organize pet videos by topic, difficulty, and audience level
- **Multi-Brand SaaS**: One codebase serves cat lovers, dog owners, exotic pet communities—theme-switched via env vars
- **Content Marketing**: Static-generated guides rank in search engines—combine with video embeds for engagement
- **Admin Training**: Learn how to build a headless CMS interface with Keystatic + Next.js for content teams

## Roadmap

- [ ] User authentication & role-based content management
- [ ] Video upload directly to platform (currently YouTube-only)
- [ ] Advanced search with Algolia or Meilisearch integration
- [ ] User comments and community discussions on guides
- [ ] Email newsletter signup for new content notifications
- [ ] Mobile app version using React Native + shared API
- [ ] Internationalization (i18n) support for multiple languages
- [ ] Webhook integration for automated content scheduling

## Contributing

Contributions are welcome. Whether you're fixing bugs, adding features, or improving docs:

1. Fork the repository: https://github.com/aisuretech/kitty-vids
2. Create a feature branch: `git checkout -b feature/your-feature-name`
3. Make your changes and test locally: `npm run dev`
4. Commit with clear messages: `git commit -m "feat: add feature description"`
5. Push to your fork: `git push origin feature/your-feature-name`
6. Open a pull request with description of changes

**Development Guidelines:**
- Use TypeScript strictly—no `any` types without justification
- Run `npm run lint` before committing
- Add tests for new features (testing infrastructure to be added)
- Follow Tailwind CSS conventions for styling

## FAQ

### How do I add new encyclopedia guides?
Access the Keystatic admin panel at `/keystatic` in development. Click "Cat Guides" (or "Dog Guides"), then "Create Entry". Add title, description, cover image, and content in Markdoc format. Content is saved to Git—commit it to deploy.

### How do I fetch and display different YouTube videos?
Edit `src/lib/youtube.ts` to modify the YouTube API search query, tags, or order. The API client supports pagination—see `getVideos()` for examples. Cached results prevent rate limiting.

### Can I use this for other pet types (birds, reptiles)?
Yes. Add a new environment variable like `SITE_THEME=birds`, then duplicate `src/content/guides/cats/` to `src/content/guides/birds/`. Create a new Keystatic collection in `keystatic.config.ts` and add navigation options in your header.

### How do I deploy to production?
Push your code to GitHub, connect your repository to Vercel, add the `YOUTUBE_API_KEY` environment variable in Vercel settings, and deploy. Vercel auto-detects Next.js and builds optimally.

### What's the difference between development and production Keystatic?
In development, Keystatic uses local file storage—changes are saved to your local `src/content/` folder. In production, Keystatic must use Git storage (content commits are pushed to your repository). Keystatic local mode doesn't work in production environments.

### How do I customize the theme or branding?
Edit `src/app/theme.css` for color variables, logos, and fonts. Modify `config/site.config.ts` for site metadata. Use `src/lib/theme.ts` to apply theme switches based on `SITE_THEME` environment variable.

## Suggested GitHub Topics
Add these in repository settings for discoverability:
- nextjs
- react
- keystatic
- cms
- headless-cms
- typescript
- tailwindcss
- youtube-api
- content-management
- pet-education
- multi-tenant
- ssr
- ssg
- vercel
- jamstack

## Links
- GitHub Organization: https://github.com/aisuretech/
- Website: https://www.kitty-vids.com/
- Contact: info@AISureTech.com

## License
MIT License

See LICENSE file for full details.
