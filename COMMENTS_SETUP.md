# Comments Setup Guide (Giscus)

This guide will help you set up Giscus comments for your GitHub Pages site.

## What is Giscus?

Giscus is a comments system powered by GitHub Discussions. It's free, privacy-friendly, and works perfectly with static sites like GitHub Pages.

## Setup Steps

### Step 1: Install the Giscus App

1. Go to [https://github.com/apps/giscus](https://github.com/apps/giscus)
2. Click **Install**
3. Select your repository (`movinggk/movinggk.github.io`)
4. Click **Install** again

### Step 2: Enable Discussions

1. Go to your repository on GitHub
2. Click on **Settings**
3. Scroll down to **Features**
4. Check the box for **Discussions**
5. Click **Set up discussions**

### Step 3: Create a Discussion Category

1. In your repository, go to the **Discussions** tab
2. Click **New category**
3. Name it "General" (or any name you prefer)
4. Click **Create category**

### Step 4: Get Your Category ID

**Easiest Method - Use Giscus Config Tool (Recommended):**

1. Go to [https://giscus.app](https://giscus.app)
2. Enter your repository: `movinggk/movinggk.github.io`
3. The tool will automatically:
   - Detect your repository ID (you already have: `77006229`)
   - Show all available categories
   - Generate the complete script with the correct category ID
4. Copy the generated script and replace the one in `ltfp_exercise_ch7.html`

**Manual Method - Get Category ID via Browser:**

1. Go to your repository on GitHub: `https://github.com/movinggk/movinggk.github.io`
2. Click on the **Discussions** tab
3. Click on your category name (`exercises_discussion`)
4. Look at the URL - it should be something like:
   `https://github.com/movinggk/movinggk.github.io/discussions/categories/1234567`
5. The number at the end (`1234567`) is your category ID

**Alternative - Use GitHub API (if repository is public):**

```bash
curl https://api.github.com/repos/movinggk/movinggk.github.io/discussions/categories
```

Look for the category with `"slug": "exercises_discussion"` and note its `"id"` field.

### Step 5: Update the HTML File

Open `ltfp_exercise_ch7.html` and replace these placeholders:

```html
data-repo-id="YOUR_REPO_ID"
data-category-id="YOUR_CATEGORY_ID"
```

With your actual IDs from Step 4.

### Step 6: Customize (Optional)

You can customize the Giscus widget by modifying these attributes in the script tag:

- `data-theme`: Change to `"dark"`, `"preferred_color_scheme"`, or `"transparent_dark"`
- `data-mapping`: Options are `"pathname"`, `"url"`, `"title"`, or `"og:title"`
- `data-input-position`: `"top"` or `"bottom"`
- `data-reactions-enabled`: `"1"` (enabled) or `"0"` (disabled)
- `data-lang`: Language code (e.g., `"en"`, `"ko"`, `"ja"`)

## Quick Setup (Recommended)

The easiest way to set up Giscus is using their configuration tool:

1. Go to [https://giscus.app](https://giscus.app)
2. Fill in:
   - **Repository**: `movinggk/movinggk.github.io`
   - **Discussion category**: Select "General" (or create one)
   - **Page ↔ Discussions mapping**: Choose "Page pathname"
   - **Features**: Enable reactions if desired
   - **Theme**: Choose your preferred theme
3. Click **Generate** and copy the script
4. Replace the Giscus script section in `ltfp_exercise_ch7.html` (around line 170)
5. The script will automatically include all the correct IDs

## Testing

After setup:
1. Commit and push your changes
2. Wait for GitHub Pages to rebuild
3. Visit your site and scroll to the comments section
4. You should see the Giscus comments widget

## Troubleshooting

**Comments not showing?**
- Make sure the Giscus app is installed on your repository
- Verify Discussions are enabled
- Check that you've entered the correct repository and category IDs
- Ensure your site is publicly accessible (required for Giscus)

**Want to add comments to other pages?**
- Copy the comments section HTML and Giscus script to any other HTML page
- Each page will have its own discussion thread based on the `data-mapping` setting

## More Information

- Giscus Documentation: [https://github.com/giscus/giscus](https://github.com/giscus/giscus)
- Giscus Configuration Tool: [https://giscus.app](https://giscus.app)

