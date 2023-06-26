name: Update README with GitHub stats

on:
  schedule:
    - cron: "0 * * * *"

jobs:
  update-readme:
    name: Update README with GitHub stats
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repository content
        uses: actions/checkout@v2

      - name: Set up Node.js
        uses: actions/setup-node@v2
        with:
          node-version: 14

      - name: Install dependencies
        run: npm install

      - name: Generate README
        run: npm run generate-readme

      - name: Commit and push if changes detected
        run: |
          git diff --quiet || git commit -am "Update README" && git push
