# How to Find Your Category ID

You need the category ID to complete the Giscus setup. Here are the easiest ways to find it:

## Method 1: Use Giscus Config Tool (Easiest - Recommended)

1. Go to **https://giscus.app**
2. Enter your repository: `movinggk/movinggk.github.io`
3. The tool will automatically show you:
   - Your repository ID
   - All available categories with their IDs
4. Select `exercises_discussion` from the dropdown
5. Copy the complete generated script
6. Replace the script in `ltfp_exercise_ch7.html` (around line 177)

**This is the easiest method - it does everything for you!**

## Method 2: Find it in the Browser URL

1. Go to: `https://github.com/movinggk/movinggk.github.io`
2. Click on the **Discussions** tab
3. Click on your category: **exercises_discussion**
4. Look at the URL in your browser - it will be something like:
   ```
   https://github.com/movinggk/movinggk.github.io/discussions/categories/1234567
   ```
5. The number at the end (`1234567`) is your **category ID**

## Method 3: Use GitHub API (if repository is public)

Run this command in your terminal:

```bash
curl https://api.github.com/repos/movinggk/movinggk.github.io/discussions/categories
```

Look for the category with `"slug": "exercises_discussion"` and copy the `"id"` value.

## Method 4: Check if Discussions are Enabled

If you get a "Not Found" error, make sure:

1. **Discussions are enabled:**
   - Go to your repository Settings
   - Scroll to "Features"
   - Make sure "Discussions" is checked ✅

2. **The category exists:**
   - Go to the Discussions tab
   - If you don't see "exercises_discussion", create it:
     - Click "New category"
     - Name it "exercises_discussion"
     - Click "Create category"

## Quick Fix

If you're having trouble, just use **Method 1** (Giscus config tool) - it's the simplest and most reliable way!

