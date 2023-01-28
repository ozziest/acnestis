# Acnestis

`Acnestis` is an open-source CLI tool for developers looking to create a minimalistic, hassle-free blog. With Acnestis, you can easily write and publish blog posts using plain markdown files, without the need for complex templates or build processes. The tool's simple and intuitive design makes it the perfect choice for developers who want to focus on creating content, rather than worrying about the technicalities of setting up a blog.

The name Acnestis, meaning the part of the back between the shoulder blades and the loins which an animal cannot reach to scratch, reflects the tool's goal of providing a simple yet powerful solution to the often complex task of blogging. Whether you're a developer looking to share your thoughts and expertise or just someone who wants to create a personal blog, Acnestis is the perfect tool to help you get started.

## How It Works?

- Create a repository on GitHub (`username.github.io`)
- Post your posts to the folder `_posts`
- Create `config.yml` file which describe your name and the blog description
- Put GitHub action file to build it.

## `config.yml`

```yml
title: Your blog title
description: The dead-simple blog ever
keywords: your blog, awesome
author: Your name
footer: acnestis - 2023
hostname: https://yoursite.com
```

## GitHub Action

```yml
name: Deploy static content to Pages

on:
  push:
    branches: ["master"]
  workflow_dispatch:

permissions:
  contents: read
  pages: write
  id-token: write

concurrency:
  group: "pages"
  cancel-in-progress: true

jobs:
  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v3
      - name: Setup Pages
        uses: actions/configure-pages@v3
      - name: Acnestis Build
        run: |
          npm i -g acnestis
          acnestis
      - name: Upload artifact
        uses: actions/upload-pages-artifact@v1
        with:
          path: "./dist"
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v1
```

## LICENSE

[MIT](LICENSE)
