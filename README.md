## Hi there 👋

<!--
**f4eakysam/f4eakysam** is a ✨ _special_ ✨ repository because its `README.md` (this file) appears on your GitHub profile.

Here are some ideas to get you started:

- 🔭 I’m currently working on ...
- 🌱 I’m currently learning ...
- 👯 I’m looking to collaborate on ...
- 🤔 I’m looking for help with ...
- 💬 Ask me about ...
- 📫 How to reach me: ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...
-->
name: Update cat

on:
  schedule:
    - cron: "*/60 * * * *"
jobs:
  update:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v2
      - name: Set env vars
        run: |
          echo ::set-env name=REPOSITORY::${{ github.repository }}
      - name: Use Node.js
        uses: actions/setup-node@v1
        with:
          node-version: "12.x"
      - name: Install node modules
        run: npm install
      - name: Update cat
        run: npm start
        env:
          API_KEY: ${{ secrets.API_KEY }}
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
      - uses: stefanzweifel/git-auto-commit-action@v4
        with:
          commit_user_name: github-actions[bot]
          commit_user_email: github-actions[bot]@users.noreply.github.com
          commit_author: Actions <github-actions[bot]@users.noreply.github.com>
          commit_message: "Hourly update :cat:"
