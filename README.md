<h1>Hi 👋, I'm Hameed</h1>
<p>Remote Sensing and GIS specialist with a strong interest in geospatial data analysis and AI applications. Passionate about continuous learning and contributing to innovative projects. Currently enhancing my skills in German and planning to further my studies in Germany. 🚀</p>
<h2>🚀 Languages and Tools I Use</h2>
<p><a target="_blank" href="https://raw.githubusercontent.com/devicons/devicon/master/icons/python/python-original.svg" style="display: inline-block;"><img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/python/python-original.svg" alt="python" width="42" height="42" /></a>
<a target="_blank" href="https://upload.wikimedia.org/wikipedia/commons/2/21/Matlab_Logo.png" style="display: inline-block;"><img src="https://upload.wikimedia.org/wikipedia/commons/2/21/Matlab_Logo.png" alt="matlab" width="42" height="42" /></a></p>
<h2>⚡️ Where to find me</h2>
<p><a target="_blank" href="https://www.linkedin.com/in/hameedbasim" style="display: inline-block;"><img src="https://img.shields.io/badge/linkedin-logo?style=for-the-badge&logo=linkedin&logoColor=white&color=%230a77b6" alt="linkedin" /></a>
<a target="_blank" href="https://www.facebook.com/abb979" style="display: inline-block;"><img src="https://img.shields.io/badge/facebook-logo?style=for-the-badge&logo=facebook&logoColor=white&color=%230866ff" alt="facebook" /></a>
<a target="_blank" href="https://www.instagram.com/hameedbasimm" style="display: inline-block;"><img src="https://img.shields.io/badge/instagram-logo?style=for-the-badge&logo=instagram&logoColor=white&color=%23F35369" alt="instagram" /></a></p>
<h2>❤️ Support Me</h2>
<p><p>
<a href="https://www.buymeacoffee.com/hameedbasim">
<img src="https://cdn.buymeacoffee.com/buttons/v2/default-yellow.png" width="160" alt="buymeacoffee" />
</a>
</p>
</p>
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
