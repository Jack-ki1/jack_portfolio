# Jackson Kimotho Portfolio - Data Scientist & AI Engineer

Welcome to the source code for my professional portfolio. This project is built with **React**, **TypeScript**, and **Tailwind CSS**, designed to showcase data-driven projects across GitHub and Hugging Face.

---

## 🚀 Customization Guide

### 1. How to Attach Your CV and Resume
To make your CV and Resume downloadable or viewable:
1.  **Prepare the Files**: Name your files `Jackson_Kimotho_CV.pdf` and `Jackson_Kimotho_Resume.pdf`.
2.  **Place in Public Folder**: Move these PDF files into the `/public` directory of this project.
3.  **Update the Code**: In `src/App.tsx`, find the buttons for "MY CV" and "RESUME" (around line 159). Update the `onClick` handler to point to your files:
    ```tsx
    <button className="btn-outline" onClick={() => window.open('/Jackson_Kimotho_CV.pdf', '_blank')}>MY CV</button>
    <button className="btn-outline" onClick={() => window.open('/Jackson_Kimotho_Resume.pdf', '_blank')}>RESUME</button>
    ```

### 2. How to Use Images from Your Device
If you want to use local images instead of Unsplash URLs:
1.  **Place Images**: Put your images in the `/public/images` folder (create the folder if it doesn't exist).
2.  **Reference in Constants**: In `src/constants.ts`, change the `image` path to point to your local file:
    ```ts
    // Example for a project image
    image: '/images/my-project-screenshot.png'
    ```
3.  **Reference in App.tsx**: For the Hero or About sections, update the `src` attribute of the `<img>` tags:
    ```tsx
    <img src="/images/my-profile-pic.jpg" alt="Jackson Kimotho" ... />
    ```

### 2b. How to Add Content to Projects & Skills
All project and skill data is managed in `src/constants.ts`. 

**To add a new project:**
1.  Open `src/constants.ts`.
2.  Add a new object to the `PROJECTS` array:
    ```ts
    {
      title: 'NEW PROJECT NAME',
      category: 'Category (e.g., Deep Learning)',
      description: 'A brief description of what you built and the tools used.',
      image: 'URL or local path',
      link: 'Link to GitHub or Hugging Face'
    }
    ```

**To update your skills:**
1.  Find the `SKILLS` array in `src/constants.ts`.
2.  Modify existing skills or add new ones:
    ```ts
    { name: 'New Skill', level: 85, category: 'Category' }
    ```
    The progress bars in the UI will automatically adjust based on the `level` percentage.

### 3. How to Upload to GitHub Pages
To host this project for free on GitHub Pages:
1.  **Install gh-pages**: Run `npm install gh-pages --save-dev`.
2.  **Update package.json**:
    *   Add a `"homepage": "https://<your-username>.github.io/<your-repo-name>"` field.
    *   Add these scripts:
        ```json
        "predeploy": "npm run build",
        "deploy": "gh-pages -d dist"
        ```
3.  **Deploy**: Run `npm run deploy`.
4.  **Settings**: Go to your GitHub repository settings -> Pages, and ensure the source is set to the `gh-pages` branch.

### 4. Overall Good Practices
*   **Image Optimization**: Use compressed images (WebP or optimized JPEG) to ensure fast loading times.
*   **Responsive Testing**: Always check your site on mobile devices. Tailwind's `md:` and `lg:` prefixes help manage different screen sizes.
*   **Clean Code**: Keep your `constants.ts` organized. If the file gets too large, consider splitting it into `projects.ts`, `blogs.ts`, etc.
*   **Accessibility**: Use descriptive `alt` tags for images and ensure high contrast for text readability.
*   **Version Control**: Commit your changes frequently with descriptive messages (e.g., "feat: add hugging face integration").

---

Created with ❤️ by Jackson Kimotho.
