### This is a [Hugo](https://gohugo.io/) project.

## Getting Started

### Run

First, run the development server:

```bash
hugo new site
cd <name-of-your-new-project>
# and then
hugo server
```

Open [http://localhost:1313](http://localhost:3000) with your browser to see the result.

You won't actually see anything, just yet, and that's because you don't have any template files. That's easily resolved. In the layouts/ directory, create a file index.html and put a basic HTML structure in there:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>Document</title>
  </head>
  <body>
    <h1>Nice. It's looking good already.</h1>
  </body>
</html>
```

You'll also add some files to the content/ and data/ directories to make sure git tracks them.

```bash
touch content/.keep data/.keep
```

This is as basic as you can get with a Hugo project. There's just enough here now for us to install Netlify CMS.

## Getting Started With Netlify CMS

### Add the Netlify CMS files to Hugo

In Hugo, static files that don't need to be processed by the build commands live in the `bash static/ ` directory. You'll install the Netlify CMS admin and config files there. Create a directory `bash admin/ ` and within it, create two files `bash index.html ` and `bash config.yml`. In the `bash index.html`, add the following content:

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Content Manager</title>
    <!-- Include the script that enables Netlify Identity on this page. -->
    <script src="https://identity.netlify.com/v1/netlify-identity-widget.js"></script>
  </head>
  <body>
    <!-- Include the script that builds the page and powers Netlify CMS -->
    <script src="https://unpkg.com/netlify-cms@^2.0.0/dist/netlify-cms.js"></script>
  </body>
</html>
```

In the config.yml file, you can add this basic configuration — you can customize as you see fit, this sample file is just to get you started.
You can start editing the page by modifying `layouts/index.js`. The page auto-updates as you edit the file.

```yaml
backend:
  name: git-gateway
  branch: main # Branch to update (optional; defaults to master)
media_folder: static/img
public_folder: /img
collections:
  - name: "blog"
    label: "Blog"
    folder: "content/blog"
    create: true
    slug: "{{year}}-{{month}}-{{day}}-{{slug}}"
    editor:
      preview: false
    fields:
      - { label: "Title", name: "title", widget: "string" }
      - { label: "Publish Date", name: "date", widget: "datetime" }
      - { label: "Description", name: "description", widget: "string" }
      - { label: "Body", name: "body", widget: "markdown" }
```

Note: You won't be able to access the CMS just yet — you still need to deploy the project with Netlify and authenticate with Netlify Identity. You'll handle this in the next few steps of this guide.

## Pushing to GitHub

It's now time to commit your changes and push to GitHub. You can run the following commands to initialize a git repository and push the changes so far.

```bash
git init # Initialize a git repository
git add . # Add every file
git commit -m "Initial Commit" # Commit every file with the message 'Initial Commit'
git remote add origin https://github.com/YOUR_USERNAME/NEW_REPO_NAME.git # Create a new repo on GitHub and add it to this project as a remote repository.
git push -u origin main # Push your changes
```
