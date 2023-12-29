---
last_reviewed: 2023-12-29
title: How I Built This Website
excerpt: "-"
tags:
---
This website is powered by 2 Github Repository, namely,
1. [davzoku/leetcode-obsidian-frontend](https://github.com/davzoku/leetcode-obsidian-frontend) : The Next.js frontend hosted in Netlify
2. [davzoku/leetcode-obsidian-vault](https://github.com/davzoku/leetcode-obsidian-vault): The Obsidian Vault containing the Leetcode Solutions.

In fact, the setup is forked from [matthewwong525/linked-blog-starter](https://github.com/matthewwong525/linked-blog-starter) and [matthewwong525/linked-blog-starter-md](https://github.com/matthewwong525/linked-blog-starter-md).  It is also well-explained in this [video link](https://www.youtube.com/watch?v=rKSpK1dXn4E).

The Obsidian Git plugin is set up to push any changes in X minute intervals. This will trigger a Github Action workflow to combine the code from both repositories and build into a production build for hosting.

Matthew's implementation supports hosting on Vercel, while I prefer to host on Netlify. This results in a difference in the final deploy step in the [publish.yml](https://github.com/davzoku/leetcode-obsidian-vault/blob/main/.github/workflows/publish.yml).

Otherwise, the remaining changes are mostly aesthetic changes and support for Google Analytics and Progressive Web App (PWA).