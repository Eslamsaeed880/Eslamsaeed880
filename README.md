<h1>Hi 👋, I'm A student of computers and artificial intelligence , Cairo University</h1>
<p></p>
<h2>🚀 Languages and Tools I Use</h2>
<p><a target="_blank" href="https://raw.githubusercontent.com/devicons/devicon/master/icons/c/c-original.svg" style="display: inline-block;"><img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/c/c-original.svg" alt="c" width="42" height="42"/></a>
<a target="_blank" href="https://raw.githubusercontent.com/devicons/devicon/master/icons/cplusplus/cplusplus-original.svg" style="display: inline-block;"><img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/cplusplus/cplusplus-original.svg" alt="cplusplus" width="42" height="42"/></a>
<a target="_blank" href="https://raw.githubusercontent.com/devicons/devicon/master/icons/java/java-original.svg" style="display: inline-block;"><img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/java/java-original.svg" alt="java" width="42" height="42"/></a>
<a target="_blank" href="https://raw.githubusercontent.com/devicons/devicon/master/icons/javascript/javascript-original.svg" style="display: inline-block;"><img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/javascript/javascript-original.svg" alt="javascript" width="42" height="42"/></a>
<a target="_blank" href="https://raw.githubusercontent.com/devicons/devicon/master/icons/python/python-original.svg" style="display: inline-block;"><img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/python/python-original.svg" alt="python" width="42" height="42"/></a>
<a target="_blank" href="https://raw.githubusercontent.com/devicons/devicon/master/icons/css3/css3-original-wordmark.svg" style="display: inline-block;"><img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/css3/css3-original-wordmark.svg" alt="css3" width="42" height="42"/></a>
<a target="_blank" href="https://raw.githubusercontent.com/devicons/devicon/master/icons/html5/html5-original-wordmark.svg" style="display: inline-block;"><img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/html5/html5-original-wordmark.svg" alt="html5" width="42" height="42"/></a>
<a target="_blank" href="https://raw.githubusercontent.com/devicons/devicon/master/icons/mysql/mysql-original-wordmark.svg" style="display: inline-block;"><img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/mysql/mysql-original-wordmark.svg" alt="mysql" width="42" height="42"/></a>
<a target="_blank" href="https://www.vectorlogo.zone/logos/sqlite/sqlite-icon.svg" style="display: inline-block;"><img src="https://www.vectorlogo.zone/logos/sqlite/sqlite-icon.svg" alt="sqlite" width="42" height="42"/></a>
<a target="_blank" href="https://www.svgrepo.com/show/303229/microsoft-sql-server-logo.svg" style="display: inline-block;"><img src="https://www.svgrepo.com/show/303229/microsoft-sql-server-logo.svg" alt="mssql" width="42" height="42"/></a>
<a target="_blank" href="https://cdn.worldvectorlogo.com/logos/django.svg" style="display: inline-block;"><img src="https://cdn.worldvectorlogo.com/logos/django.svg" alt="django" width="42" height="42"/></a>
<a target="_blank" href="https://www.vectorlogo.zone/logos/git-scm/git-scm-icon.svg" style="display: inline-block;"><img src="https://www.vectorlogo.zone/logos/git-scm/git-scm-icon.svg" alt="git" width="42" height="42"/></a>
<h2>⚡️ Where to find me</h2>
<p><a target="_blank" href="https://www.linkedin.com/in/https://www.linkedin.com/in/eslam-saeed-359087290?utm_source=share&utm_campaign=share_via&utm_content=profile&utm_medium=android_app" style="display: inline-block;"><img src="https://cdn.jsdelivr.net/npm/simple-icons@3.0.1/icons/linkedin.svg" alt="linkedin" width="42" height="42"/></a></p>

name: GitHub Snake Game

on:
  # Schedule the workflow to run daily at midnight UTC
  schedule:
    - cron: "0 0 * * *"
  # Allow manual triggering of the workflow
  workflow_dispatch:
  # Trigger the workflow on pushes to the main branch
  push:
    branches:
      - main
jobs:
  generate:
    runs-on: ubuntu-latest
    timeout-minutes: 10
    steps:
      # Step 1: Checkout the repository
      - name: Checkout Repository
        uses: actions/checkout@v3
      # Step 2: Generate the snake animations
      - name: Generate GitHub Contributions Snake Animations
        uses: Platane/snk@v3
        with:
          # GitHub username to generate the animation for
          github_user_name: ${{ github.repository_owner }}
          # Define the output files and their configurations
          outputs: |
            dist/github-snake.svg
            dist/github-snake-dark.svg?palette=github-dark
            dist/ocean.gif?color_snake=orange&color_dots=#bfd6f6,#8dbdff,#64a1f4,#4b91f1,#3c7dd9
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
      # Step 3: Deploy the generated files to the 'output' branch
      - name: Deploy to Output Branch
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./dist
          publish_branch: output
          # Optionally, you can set a custom commit message
          commit_message: "Update snake animation [skip ci]"
