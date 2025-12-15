# Personal GitHub Pages Website

This repository contains my personal GitHub Pages website.

## Structure

- `index.html` - Main homepage with personal information
- `ch7_exercises.html` - Exercises page with sidebar navigation
- `ltfp_exercise_ch7.md` - Source markdown file for exercises
- `photo.jpg` - Profile photo

## Setup Instructions

### 1. Customize the Main Page

Edit `index.html` and replace the placeholder information:
- **Your name** (in the header)
- **Contact information** (email, institution, department, location)
- **Research interests** (describe your research area)
- **Publications** (add your publications)
- **Links** (add links to your CV, GitHub, Google Scholar, etc.)

### 2. Enable GitHub Pages

1. Go to your repository on GitHub
2. Click on **Settings**
3. Navigate to **Pages** in the left sidebar
4. Under **Source**, select:
   - Branch: `main` (or `master` if that's your default branch)
   - Folder: `/ (root)`
5. Click **Save**
6. Wait a few minutes for GitHub to build your site

### 3. Access Your Site

Your site will be available at:
```
https://movinggk.github.io
```

The exercises page will be at:
```
https://movinggk.github.io/ch7_exercises.html
```

## Features

- ✅ Responsive design that works on mobile and desktop
- ✅ Modern, clean UI with gradient styling
- ✅ Math equation support using MathJax
- ✅ Markdown rendering for exercise solutions
- ✅ Easy navigation between pages

## Customization Tips

1. **Colors**: The site uses a purple gradient theme. You can customize colors in the `<style>` sections of the HTML files.

2. **Adding More Pages**: 
   - Create new HTML files following the structure of `ch7_exercises.html`
   - Add links to them in the "Links & Resources" section of `index.html`

3. **Math Equations**: The exercises page uses MathJax to render LaTeX equations. Make sure your markdown uses `$` for inline math and `$$` for display math.

## Comments Feature

The exercises page includes a comments section powered by **Giscus** (GitHub Discussions). The comments are already configured and will appear at the bottom of each problem page.

## Notes

- The exercises page (`ch7_exercises.html`) uses JavaScript to fetch and render the markdown file
- Math equations are rendered using MathJax
- The sidebar navigation allows easy browsing between problems
- Comments require GitHub Discussions to be enabled on your repository
