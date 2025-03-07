# Hosting a Resume with Hugo and GitHub Pages

## Purpose

This README provides step-by-step instructions for hosting a resume using **Hugo**, a static site generator, and **GitHub Pages**, a forge for hosting static websites. The guide is intended for beginners, particularly for individuals like Marvin McLaren, who have basic command-line experience but no prior knowledge of Git, static site generators, or forges.

Hosting a resume on a static site provides **several advantages**:
- **Easy Maintenance** – Updating a Markdown file is faster than editing raw HTML.
- **Professional Presentation** – A hosted website makes sharing your resume seamless.
- **Version Control** – Track changes over time using Git.
- **Free Hosting** – GitHub Pages allows you to publish your site at no cost.
- **Improved Accessibility** – Your resume is available on any device via a URL.

Additionally, this README follows the key principles from Andrew Etter’s *Modern Technical Writing*, emphasizing the use of:

- **Lightweight markup languages** (Markdown) to ensure easy formatting.
- **Distributed version control** (Git) for tracking changes.
- **Static site generators** (Hugo) to create a fast, efficient site.
- **A forge for hosting** (GitHub Pages) for seamless deployment.

## Prerequisites

Before proceeding, ensure you have the following installed on your system:

- **Git** ([Download here](https://git-scm.com/))
  - Required for tracking changes in your resume and deploying to GitHub.
- **Hugo** ([Install using Scoop](https://gohugo.io/getting-started/installing/)):

  ```powershell
  scoop install hugo
  ```
  - A static site generator that simplifies site creation with pre-built themes.
- **A GitHub account** ([Sign up here](https://github.com/))
  - Required to host your resume for free using GitHub Pages.
- **A text editor** (e.g., VS Code, Notepad++, or any Markdown editor)
  - Helps you edit the Markdown resume efficiently.

## Steps to Host Your Resume

### **1. Set Up the Hugo Site** (Aligns with Etter’s principle of static site generators)

```powershell
hugo new site my-resume-site
cd my-resume-site
```

This command generates a Hugo site with the necessary directory structure, making it easy to manage content. A static site generator like Hugo enables quick deployment with minimal dependencies, reducing complexity compared to traditional CMS platforms.

### **2. Add a Theme** (Supports the principle of reusing existing solutions)

We’ll use the Ananke theme:

```powershell
git init
git submodule add https://github.com/theNewDynamic/gohugo-theme-ananke.git themes/ananke
```

Then, edit `config.toml`:

```toml
theme = "ananke"
baseURL = "https://yourusername.github.io/my-resume-site/"
languageCode = "en-us"
title = "My Hugo Resume Site"
```

This configuration sets the site’s theme and metadata. Etter emphasizes leveraging existing tools/themes rather than building everything from scratch to save time and effort.

### **3. Add Your Resume** (Markdown as a lightweight documentation format)

Create a Markdown file for your resume in the **`content/`** folder:

```powershell
echo "" > content/caibaitong_wang.md
```

This creates `content/caibaitong_wang.md`. Open the file and add your resume content:

```markdown
---
title: "My Resume"
date: 2025-03-05T21:00:00
draft: false
---

## John Doe
**Software Engineer**  
Email: johndoe@example.com  
LinkedIn: [linkedin.com/in/johndoe](https://linkedin.com/in/johndoe)

### Education
- B.Sc. in Computer Science, XYZ University

### Experience
- Software Developer at ABC Corp (2022–Present)
```

Using Markdown ensures a **clean structure** that can be converted to HTML easily. This aligns with Etter’s principle of using lightweight markup for technical documentation.

### **4. Build and Preview the Site**

```powershell
hugo server -D
```

Visit [http://localhost:1313/](http://localhost:1313/) to preview your resume. If your theme doesn’t auto-list pages, go to [http://localhost:1313/caibaitong_wang/](http://localhost:1313/caibaitong_wang/) (or whatever slug Hugo generated).

### **5. Deploy to GitHub Pages** (Distributed version control + hosting on a forge)

1. Create a **GitHub repository** (e.g., `my-resume-site`).
2. Push your Hugo project to GitHub:

   ```powershell
   git remote add origin https://github.com/yourusername/my-resume-site.git
   git branch -M main
   git add .
   git commit -m "Initial commit"
   git push -u origin main
   ```

3. Generate the static site:

   ```powershell
   hugo
   ```

   This places your final HTML in a `public/` folder.

4. Rename `public` to `docs`:

   ```powershell
   mv public docs
   ```

5. Commit and push again:

   ```powershell
   git add .
   git commit -m "Deploy site to docs folder"
   git push
   ```

6. Enable GitHub Pages in **Settings → Pages**:

   - **Source**: `main` branch
   - **Folder**: `/docs`
   - Save

GitHub will provide a URL like `https://yourusername.github.io/my-resume-site/`. That’s your live site!

## Further Resources

- [Hugo Documentation](https://gohugo.io/documentation/)
- [GitHub Pages Guide](https://pages.github.com/)
- [Markdown Guide](https://www.markdownguide.org/)
- [Andrew Etter’s *Modern Technical Writing*](https://www.oreilly.com/library/view/modern-technical-writing/9781492049395/)
- [Git Workflow Explained](https://www.atlassian.com/git/tutorials/)
- [Static Site Generators: Why Use Them?](https://www.staticgen.com/)

## FAQ

### **1. Why use Markdown instead of raw HTML?**

Markdown is lightweight, easy to read, and widely supported for formatting text without needing complex HTML tags. This aligns with Etter’s recommendation to use simple and widely adopted documentation formats.

### **2. I updated my resume, but I don’t see changes online. Why?**

Ensure you ran `hugo` to regenerate the site and renamed `public/` to `docs/` before pushing to GitHub. Static site generators do not auto-update, so you must build and redeploy after changes.

### **3. What if my GitHub Pages URL returns a 404 error?**

Check that GitHub Pages is enabled under **Settings → Pages**, with `main` as the source branch and `/docs` as the folder. Also, confirm your `baseURL` in `config.toml` is correct.

### **4. Why did I get a "failed to push" error when committing?**

This usually happens when your local branch is behind the remote branch. Run `git pull --rebase origin main` before pushing again.

### **5. Why is my site displaying the README instead of my resume?**

Ensure your resume is placed inside `content/`, and that `hugo` correctly generates the HTML version of it in `docs/` before deploying.

### 6. How do I change the theme of my Hugo site?

To change your Hugo theme, update the theme value in config.toml to a different theme name. Make sure to download and add the theme to the themes/ directory.

### 7. How do I add navigation links to my resume?

Edit config.toml and add a [menu] section under [params]. For example:

[menu]
  [[menu.main]]
    name = "Resume"
    url = "/caibaitong_wang/"
    weight = 1

### 8. How can I ensure my changes are reflected immediately?

Use hugo server -D to preview changes locally before deploying. If GitHub Pages does not update immediately, try clearing your browser cache and reloading.

### 9. How do I troubleshoot broken links in my Hugo site?

Check if the generated HTML files in docs/ contain the expected URLs. If links are broken, verify your baseURL in config.toml and ensure pages are correctly generated by running hugo.

### 10. Why is my theme’s styling missing when I visit my site?

If your theme’s styling is missing, check that your baseURL is correct in config.toml. Also, ensure that CSS files from the theme are included correctly in the docs/ folder when deploying.

## Credits

- **John Doe** (Author)
- **Ananke Theme** by The New Dynamic (Licensed under MIT)
- **Peer Review Contributors** (Include names of anyone who reviewed your README)
- **GitHub Pages Documentation** (Referenced for deployment)

