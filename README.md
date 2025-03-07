```markdown
# Hosting a Resume with Hugo and GitHub Pages

## Purpose

This README provides step-by-step instructions for hosting a resume using **Hugo**, a static site generator, and **GitHub Pages**, a forge for hosting static websites. The guide is intended for beginners, particularly for individuals like Marvin McLaren, who have basic command-line experience but no prior knowledge of Git, static site generators, or forges.

Additionally, this README follows the key principles from Andrew Etter’s *Modern Technical Writing*, emphasizing the use of:

- **Lightweight markup languages** (Markdown)
- **Distributed version control** (Git)
- **Static site generators** (Hugo)
- **A forge for hosting** (GitHub Pages)

## Prerequisites

Before proceeding, ensure you have the following installed on your system:

- **Git** ([Download here](https://git-scm.com/))
- **Hugo** ([Install using Scoop](https://gohugo.io/getting-started/installing/)):

  ```powershell
  scoop install hugo
  ```

- A **GitHub account** ([Sign up here](https://github.com/))
- A **text editor** (e.g., VS Code, Notepad++, or any Markdown editor)

## Steps to Host Your Resume

### **1. Set Up the Hugo Site** (Aligns with Etter’s principle of static site generators)

```powershell
hugo new site my-resume-site
cd my-resume-site
```

A static site generator like Hugo enables quick deployment with minimal dependencies, reducing complexity compared to traditional CMS platforms (Etter’s focus on “lean” tools).

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

Etter emphasizes leveraging existing tools/themes rather than building everything from scratch.

### **3. Add Your Resume** (Markdown as a lightweight documentation format)

Create a Markdown file for your resume in the **`content/`** folder:

```powershell
hugo new resume.md
```

This command creates `content/resume.md` by default. Edit that file to include your information:

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

Markdown is simple, easy to maintain, and integrates seamlessly with version control—precisely what Etter recommends.

### **4. Build and Preview the Site**

```powershell
hugo server -D
```

Visit [http://localhost:1313/](http://localhost:1313/) to preview your resume. If your theme doesn’t auto-list pages, go to [http://localhost:1313/resume/](http://localhost:1313/resume/) (or whatever slug Hugo generated).

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
- [Pfeiffer’s *Technical Communication* - Chapter 8 on Writing Instructions](https://example.com/)

## FAQ

### **1. Why use Markdown instead of raw HTML?**

Markdown is lightweight, easy to read, and widely supported for formatting text without needing complex HTML tags. This aligns with Etter’s recommendation to use simple and widely adopted documentation formats.

### **2. I updated my resume, but I don’t see changes online. Why?**

Ensure you ran `hugo` to regenerate the site and renamed `public/` to `docs/` before pushing to GitHub. Static site generators do not auto-update, so you must build and redeploy after changes.

## Credits

- **John Doe** (Author)
- **Ananke Theme** by The New Dynamic (Licensed under MIT)
- **Peer Review Contributors** (Include names of anyone who reviewed your README)
- **GitHub Pages Documentation** (Referenced for deployment)
```