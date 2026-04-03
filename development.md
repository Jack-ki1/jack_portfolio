# Development Guide: Jackson Kimotho Portfolio

Welcome to the development documentation for this portfolio application. This document details the folder structure, where to make specific changes, and best practices for developing and maintaining the site.

---

## 📂 Folder Structure & Architecture

This application is built with **React**, **TypeScript**, and **Vite**, utilizing **Tailwind CSS** for styling. 

```text
PORTFOLIO_JACKKIM/
├── public/                    # Static assets that don't need compilation
│   ├── images/                # Images like profile pictures and project screenshots (.webp)
│   ├── fonts/                 # Local font overrides (if any)
│   ├── 404.html               # Custom 404 redirect for GitHub Pages
│   ├── robots.txt             # SEO crawler instructions
│   ├── sitemap.xml            # SEO sitemap for indexing
│   ├── Jackson_Kimotho_CV.pdf # Your downloadable CV
│   └── Jackson_Kimotho_Resume.pdf
├── src/                       # Source code for the application
│   ├── components/            # Reusable UI components
│   │   └── Accordion.tsx      # Accordion component used in Services and FAQ
│   ├── main.tsx               # Entry point for React (mounts App to the DOM)
│   ├── App.tsx                # Main application component, layout, and sections
│   ├── index.css              # Global CSS styles and Tailwind imports
│   ├── constants.ts           # All text content, lists, skills, and links live here
│   └── vite-env.d.ts          # TypeScript declarations for Vite
├── index.html                 # The HTML template for the whole app
├── package.json               # Defines dependencies (React, tailwind) and npm scripts
├── vite.config.ts             # Configuration for the Vite bundler
├── tailwind.config.ts         # Optional Tailwind configuration (Vite plugin is used heavily here)
└── tsconfig.json              # TypeScript compilation rules
```

### Purpose of Key Files

- **`index.html`**: Contains the root `<div>` for React, fallback `<noscript>` information for basic SEO, and `<meta>` tags (Open Graph, Twitter Cards).
- **`src/App.tsx`**: Contains the core logic for the single-page application. Features scroll-spy, formspree logic for sending emails, theme toggle, and section rendering (Hero, About, Projects, etc.).
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
* **Important:** This app is optimized for `.webp` image formats to boost Lighthouse and SEO scores. It's recommended to convert images to `.webp` before linking them in `constants.ts` or `App.tsx`.
* For the main Hero images, look inside `src/App.tsx` at `<img src="images/jack1.webp" ... />`.

### 3. Contact Form (Formspree)
The contact form uses "Formspree".
* In `src/App.tsx`, search for `fetch('https://formspree.io/f/YOUR_FORM_ID'`.
* Replace `YOUR_FORM_ID` with the ID provided by your Formspree dashboard to receive emails properly.

### 4. Customizing the Theme (Colors & Fonts)
1. Open `src/index.css`.
2. Under the `:root` block, modify the CSS variables:
   ```css
   :root {
     --accent: #D4F06D; /* The vibrant lime green color */
     --bg: #121212;     /* Dark background */
   }
   ```
3. To change fonts, update the `@import` statements for `@fontsource/` and the `--font-sans` or `--font-anton` themes.

### 5. Resumes and CV Links
* Upload updated PDF versions to the `/public` folder with the exact names: `Jackson_Kimotho_CV.pdf` and `Jackson_Kimotho_Resume.pdf`.
* If you rename them, make sure to update the `onClick` window open handlers in `src/App.tsx` around the **About** section layout.

---

## 🚀 Deployment (GitHub Pages)

This project has been pre-configured to deploy seamlessly to GitHub Pages.

1. Ensure all your changes look good locally: 
   ```bash
   npm run dev
   ```
2. Build and push your code to your main branch.
3. To trigger the deploy script:
   ```bash
   npm run deploy
   ```
*(This command runs `gh-pages -d dist` to move the built assets to a dedicated gh-pages branch.)*

## 💡 Good Practices
* **Keep `App.tsx` organized**: If it grows too large, move sections (like Contact or Hero) into `src/components/`.
* **Version Control**: Commit your changes frequently with descriptive messages.
* **SEO**: When modifying `App.tsx` and adding logic, try to ensure elements are readable for screen readers (using standard semantic HTML or accessible links).
