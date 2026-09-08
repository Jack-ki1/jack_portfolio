# Development Guide: Jackson Kimotho Portfolio

Welcome to the development documentation for this portfolio application. This document details the folder structure, where to make specific changes, and best practices for developing and maintaining the site.

---

## 📂 Folder Structure & Architecture

This application is built with **React**, **TypeScript**, and **Vite**, utilizing **Tailwind CSS** for styling. 

```text
PORTFOLIO_JACKKIM/
├── public/                    # Static assets that don't need compilation
│   ├── images/                # Images like profile pictures and project screenshots (.webp)
│   ├── 404.html               # Custom 404 redirect for GitHub Pages
│   ├── robots.txt             # SEO crawler instructions
│   ├── sitemap.xml            # SEO sitemap for indexing
│   ├── JACK_CV_V1.pdf         # Your downloadable CV
│   └── JK_RESUME_V2.pdf       # Your downloadable resume
├── src/                       # Source code for the application
│   ├── components/            # Reusable UI components
│   │   └── Accordion.tsx      # Accordion component used in Services and FAQ
│   ├── main.tsx               # Entry point for React (mounts App to the DOM)
│   ├── App.tsx                # Main application component, layout, and sections
│   ├── index.css              # Global CSS styles and Tailwind imports
│   ├── constants.ts           # All text content, lists, skills, and links live here
├── index.html                 # The HTML template for the whole app
├── package.json               # Defines dependencies (React, tailwind) and npm scripts
├── vite.config.ts             # Configuration for the Vite bundler
├── tailwind.config.ts         # Optional Tailwind configuration (Vite plugin is used heavily here)
└── tsconfig.json              # TypeScript compilation rules
```

### Purpose of Key Files

- **`index.html`**: Contains the root `<div>` for React, fallback `<noscript>` information for basic SEO, and `<meta>` tags (Open Graph, Twitter Cards).
- **`src/App.tsx`**: Contains the core logic for the single-page application. Features scroll-spy, FormSubmit email routing, theme toggle, and section rendering (Hero, About, Projects, etc.).
- **`src/constants.ts`**: The single source of truth for text data. If you want to update text without touching React code, do it here. 
- **`src/index.css`**: Configures Tailwind, `@fontsource` font imports, and specific theme variables (e.g. `--accent`, `--bg`).

---

## 🛠️ How to Make Changes

### 1. Updating Projects, Blogs, and Skills
All structural lists pull their data directly from `src/constants.ts`.
1. Open `src/constants.ts`.
2. Add, remove, or modify items inside the `PROJECTS`, `BLOGS`, or `SKILLS` arrays.
3. Example of adding a new project:
   ```ts
   {
     title: 'NEW PROJECT NAME',
     category: 'Deep Learning',
     description: 'A brief description of what you built and the tools used.',
     image: 'images/your-new-image.webp', // Add this image to public/images/
     link: 'https://huggingface.co/your-link'
   }
   ```

### 2. Changing Images and Optimizations
* Place all raw images into `public/images/`.
* **Important:** This app uses `.webp` image formats to keep the portfolio lightweight. Run `npm run convert-images` when adding source PNG/JPEG files.
* For the main Hero images, look inside `src/App.tsx` at `<img src="images/jack1.webp" ... />`.

### 3. Contact Form (FormSubmit)
The contact form posts enquiries to `kimothojackson1125@gmail.com` through FormSubmit.
* The first real submission may require activating the address through the confirmation email sent by FormSubmit.
* If you prefer Formspree or a private serverless endpoint, replace the fetch URL in `src/App.tsx`; never commit API keys or SMTP credentials.

### 4. Search Engine Visibility
* Add the `google-site-verification` meta tag content from Google Search Console to `index.html`.
* Add the Bing Webmaster verification meta tag content to the same file, then submit `https://Jack-ki1.github.io/jack_portfolio/sitemap.xml` in both dashboards.
* Request indexing for `https://Jack-ki1.github.io/jack_portfolio/` after deployment. Search engines decide when to crawl; verification does not guarantee a ranking or immediate indexing.

### 5. Customizing the Theme (Colors & Fonts)
1. Open `src/index.css`.
2. Under the `:root` block, modify the CSS variables:
   ```css
   :root {
     --accent: #D4F06D; /* The vibrant lime green color */
     --bg: #121212;     /* Dark background */
   }
   ```
3. To change fonts, update the `@import` statements for `@fontsource/` and the `--font-sans` or `--font-anton` themes.

### 6. Resumes and CV Links
* Upload updated PDF versions to the `/public` folder with the exact names: `JACK_CV_V1.pdf` and `JK_RESUME_V2.pdf`.
* If you rename them, make sure to update the `onClick` window open handlers in `src/App.tsx` around the **About** section layout.

---

## 🚀 Deployment (GitHub Pages)

This project has been pre-configured to deploy seamlessly to GitHub Pages.

1. Ensure all your changes look good locally: 
   ```bash
   npm run dev
   ```
2. Build and push your code to the `master` branch.
3. GitHub Actions runs `npm ci`, builds `dist`, and deploys through GitHub Pages.

## 💡 Good Practices
* **Keep `App.tsx` organized**: If it grows too large, move sections (like Contact or Hero) into `src/components/`.
* **Version Control**: Commit your changes frequently with descriptive messages.
* **SEO**: When modifying `App.tsx` and adding logic, try to ensure elements are readable for screen readers (using standard semantic HTML or accessible links).
