
2025-07-14 16:16

Status:

Tags: [Github](../../../3%20-%20Tags/Github.md) [React](../../../3%20-%20Tags/React.md)

---
# Deploying Your React Project to GitHub Pages - Github
If your project is already on your local machine and pushed to GitHub, you're in a good starting position. You can jump straight into the deployment steps.

Here's how to get your React app hosted on GitHub Pages, assuming you've already created the React project locally and pushed it to a GitHub repository.

### Step 1: Install `gh-pages`

The `gh-pages` package simplifies the deployment process for Create React App projects.

Open your terminal, navigate to your React project's root directory, and run:

Bash

```
npm install --save-dev gh-pages
# OR
yarn add --dev gh-pages
```

	### Step 2: Configure `package.json` for Deployment

You need to tell your React project where it will be hosted on GitHub Pages and how to deploy.

Open your `package.json` file (it's in your project's root directory) and make these two additions:

1. **Add `homepage` property:**
    
    - This specifies the base URL of your deployed app. Replace `YOUR_USERNAME` with your GitHub username and `YOUR_REPOSITORY_NAME` with the exact name of your GitHub repository.
        
    
    JSON
    
    ```
    // Inside your package.json, typically near the top level, after "version"
    "homepage": "http://ganeshreddychimmula.github.io/YOUR_REPOSITORY_NAME",
    ```
    
    For example, if your GitHub username is `octocat` and your repository is `my-react-app`, it would be `"homepage": "http://octocat.github.io/my-react-app"`.
    
2. **Add `predeploy` and `deploy` scripts:**
    
    - These scripts automate the build and push process. Add them inside the `"scripts"` object.
        
    
    JSON
    
    ```
    // Inside your package.json, within the "scripts" object
    "scripts": {
        "start": "react-scripts start",
        "build": "react-scripts build",
        "test": "react-scripts test",
        "eject": "react-scripts eject",
        "predeploy": "npm run build", // This runs 'build' before 'deploy'
        "deploy": "gh-pages -d build" // This pushes the 'build' folder to 'gh-pages' branch
    },
    ```
    
    Your `package.json` should now look something like this (with your specific project details and other scripts/dependencies):
    
    JSON
    
    ```
    {
      "name": "my-react-app",
      "version": "0.1.0",
      "private": true,
      "homepage": "http://YOUR_USERNAME.github.io/YOUR_REPOSITORY_NAME",
      "dependencies": {
        // ... your dependencies
      },
      "devDependencies": {
        "gh-pages": "^x.x.x" // The version number might be different
      },
      "scripts": {
        "start": "react-scripts start",
        "build": "react-scripts build",
        "test": "react-scripts test",
        "eject": "react-scripts eject",
        "predeploy": "npm run build",
        "deploy": "gh-pages -d build"
      },
      // ... other configurations
    }
    ```
    
for vite project:
```
{

  "name": "donation-inventory",

  "private": true,

  "version": "0.0.0",

  "homepage": "http://ganeshreddychimmula.github.io/animal-shelter-donation-inventory",

  "type": "module",

  "scripts": {

    "dev": "vite",

    "build": "vite build",

    "lint": "eslint .",

    "preview": "vite preview",

    "predeploy": "npm run build",

    "deploy": "gh-pages -d dist" --<dist instead of vite

  },

  "dependencies": {

    "react": "^19.1.0",

    "react-dom": "^19.1.0"

  },

  "devDependencies": {

    "@eslint/js": "^9.30.1",

    "@types/react": "^19.1.8",

    "@types/react-dom": "^19.1.6",

    "@vitejs/plugin-react": "^4.6.0",

    "eslint": "^9.30.1",

    "eslint-plugin-react-hooks": "^5.2.0",

    "eslint-plugin-react-refresh": "^0.4.20",

    "gh-pages": "^6.3.0",

    "globals": "^16.3.0",

    "vite": "^7.0.4"

  }

}
```
>     "deploy": "gh-pages -d dist" -->dist instead of vite [^1]


### Step 3: Deploy Your Application

With the configuration in place, you can now deploy your React app.

Run this command in your project's root directory:

Bash

```
npm run deploy
# OR
yarn deploy
```

This command will:

1. **Build your app:** It first runs `npm run build` (due to the `predeploy` script), which creates an optimized, production-ready version of your app in a folder named `build`.
    
2. **Push to `gh-pages` branch:** It then takes the contents of this `build` folder and pushes them to a new branch in your GitHub repository called `gh-pages`. This branch is specifically used by GitHub Pages.
    

### Step 4: Configure GitHub Pages Settings

The final step is to tell GitHub to serve your site from the `gh-pages` branch.

1. Go to your project's repository on **GitHub.com**.
    
2. Click on the **Settings** tab (usually near the top right, under your repository name).
    
3. In the left sidebar, click on **Pages**.
    
4. Under the "Build and deployment" section:
    
    - For "Source", click the dropdown and select the **`gh-pages` branch**.
        
    - Make sure the folder is set to **`/ (root)`**.
        
5. Click the **Save** button.
    

---

### Verification and Troubleshooting

After saving, GitHub Pages will start building and deploying your site. This usually takes a few minutes (sometimes up to 10-15 minutes).

- **Check the URL:** After a short while, revisit the **Pages** section in your GitHub repository settings. You should see a message indicating your site is published, along with the live URL (e.g., `https://YOUR_USERNAME.github.io/YOUR_REPOSITORY_NAME/`).
    
- **Troubleshooting:** If you see a blank page or a 404 error:
    
    - **Wait a bit:** Give it more time.
        
    - **Clear browser cache:** Sometimes old content is cached.
        
    - **Inspect `homepage` URL:** Double-check that your `homepage` URL in `package.json` exactly matches your GitHub username and repository name (case-sensitive!).
        
    - **Check browser console:** Open your browser's developer tools (usually F12) and check the "Console" and "Network" tabs for errors. If assets (like JS or CSS files) are failing to load with 404s, it's almost certainly an incorrect `homepage` path.
        
    - **React Router:** If you're using React Router, `BrowserRouter` might cause issues on GitHub Pages. Consider switching to `HashRouter` if direct URL access and refresh behavior are problematic.
        

You should now have your React app live on GitHub Pages! Let me know if you run into any specific issues during the process.


## [^1]:  `Error: ENOENT: no such file or directory, stat 'D:\web-development\donation-inventory\build'` 
[^1]:  `Error: ENOENT: no such file or directory, stat 'D:\web-development\donation-inventory\build'` 
You've hit a common snag when mixing Vite with the `gh-pages` package, and the error message `Error: ENOENT: no such file or directory, stat 'D:\web-development\donation-inventory\build'` is very descriptive!

The problem is that **Vite's default build output directory is `dist`**, not `build`, as you can see in your build output:

```
vite v7.0.4 building for production...
✓ 36 modules transformed.
dist/index.html            0.47 kB │ gzip:  0.30 kB
dist/assets/index-CXI0_HDg.css     6.23 kB │ gzip:  2.06 kB
dist/assets/index-BPpGXFa2.js   193.37 kB │ gzip: 60.81 kB
✓ built in 528ms
```

However, your `deploy` script is configured to look for a directory named `build`:

JSON

```
"deploy": "gh-pages -d build"
```

### The Solution

You just need to tell `gh-pages` to look for the `dist` directory instead of `build`.

**Change your `deploy` script in `package.json` from:**

JSON

```
"deploy": "gh-pages -d build"
```

**To:**

JSON

```
"deploy": "gh-pages -d dist"
```

### Updated `package.json`

Your `scripts` section should now look like this:

JSON

```
{
  "name": "donation-inventory",
  "private": true,
  "version": "0.0.0",
  "homepage": "http://ganeshreddychimmula.github.io/animal-shelter-donation-inventory",
  "type": "module",
  "scripts": {
    "dev": "vite",
    "build": "vite build",
    "lint": "eslint .",
    "preview": "vite preview",
    "predeploy": "npm run build",
    "deploy": "gh-pages -d dist"  <-- Changed this line!
  },
  "dependencies": {
    "react": "^19.1.0",
    "react-dom": "^19.1.0"
  },
  "devDependencies": {
    "@eslint/js": "^9.30.1",
    "@types/react": "^19.1.8",
    "@types/react-dom": "^19.1.6",
    "@vitejs/plugin-react": "^4.6.0",
    "eslint": "^9.30.1",
    "eslint-plugin-react-hooks": "^5.2.0",
    "eslint-plugin-react-refresh": "^0.4.20",
    "gh-pages": "^6.3.0",
    "globals": "^16.3.0",
    "vite": "^7.0.4"
  }
}
```

### Next Steps

1. **Save** your `package.json` file with the change.
    
2. Run `npm run deploy` again.
    

This time, `npm run build` will create the `dist` folder, and `gh-pages -d dist` will correctly find that folder and push its contents to your `gh-pages` branch.

Remember to also ensure your GitHub Pages settings for the repository are configured to serve from the `gh-pages` branch and the `/ (root)` folder, as discussed in the previous steps.

## What am I doing wrong, even though I am running npm run deploy, the github live page is showing 404 error that it cannot retrieve  
[^2](vscode-file://vscode-app/c:/Users/gchim/AppData/Local/Programs/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-browser/workbench/workbench.html) net::ERR_ABORTED 404 (Not Found)Understand this error  
animal-shelter-donation-inventory/:8 GET [https://ganeshreddychimmula.github.io/assets/index-BPpGXFa2.js](vscode-file://vscode-app/c:/Users/gchim/AppData/Local/Programs/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-browser/workbench/workbench.html) net::ERR_ABORTED 404 (Not Found)

ganeshreddychimmula: what would be the best commit message for the last changes  i did

GitHub Copilot: A suitable commit message for your last changes would be:

```
Add new donation entry for Alice Johnson (Food, 10kg, 2024-07-11) to initialDonations
```

ganeshreddychimmula: I moved all the to data.json

GitHub Copilot: A clear commit message for your change would be:

```
Move donation data from data.js to data.json for better data management
```

ganeshreddychimmula: is it suggested to seperate more components from App.jsx to individual files or is it good now? and why?

GitHub Copilot: Your current structure already separates major components like `Header`, `DonationForm`, and `Modal` into their own files, which is good practice. The remaining code in `App.jsx` mainly handles state management, rendering logic, and composition of these components.

**Suggestions:**
- If the donation list rendering (`donationLListElements`) or the summary/filter sections grow more complex, consider extracting them into their own components (e.g., `DonationList`, `DonationSummary`, `DonationFilter`).
- For now, your separation is sufficient for maintainability and readability, given the app's current size and complexity.

**Why?**
- Separating components improves readability, reusability, and testability.
- Over-separation for small/simple logic can add unnecessary complexity.
- As features grow, refactoring into more components is recommended.

**Summary:**  
Your structure is good for now. Refactor further only if individual sections become complex or need to be reused elsewhere.

ganeshreddychimmula: What am I doing wrong, even though I am running npm run deploy, the github live page is showing 404 error that it cannot retrieve 
animal-shelter-donation-inventory/:9  GET https://ganeshreddychimmula.github.io/assets/index-CXI0_HDg.css net::ERR_ABORTED 404 (Not Found)Understand this error
animal-shelter-donation-inventory/:8  GET https://ganeshreddychimmula.github.io/assets/index-BPpGXFa2.js net::ERR_ABORTED 404 (Not Found)

GitHub Copilot: This error is happening because your app is deployed to a subfolder (`animal-shelter-donation-inventory`) on GitHub Pages, but Vite by default builds with asset URLs relative to the root (`/`).  
As a result, your site tries to load assets from `/assets/...` instead of `/animal-shelter-donation-inventory/assets/...`.

**How to fix:**  
Set the `base` option in your `vite.config.js` to match your repo name:

````js
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react'

// https://vite.dev/config/
export default defineConfig({
  plugins: [react()],
  base: '/animal-shelter-donation-inventory/', // <-- Add this line
})
````

Then rebuild and redeploy:

```sh
npm run build
npm run deploy
```

This will make all asset URLs relative to `/animal-shelter-donation-inventory/` and fix the 404 errors.

---
## References