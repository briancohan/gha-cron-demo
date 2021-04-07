# GHA Cron Demo
Simple Example of Updating Repo with Github Actions Cron Scheduling

Last Updated:
Wed Apr  7 21:48:29 UTC 2021

It's worth noting that [cron is not guaranteed to run the scheduled time](https://upptime.js.org/blog/2021/01/22/github-actions-schedule-not-working/)

To do this, I created 

name: Update

on:
  schedule:
    - cron:  '* * * * *'

jobs:
  update:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout Repo
        uses: actions/checkout@v2

      - name: Update Readme
        run: |
          echo "# GHA Cron Demo" > README.md
          echo "Simple Example of Updating Repo with Github Actions Cron Scheduling" >> README.md
          echo "" >> README.md
          echo "Last Updated:" >> README.md
          date >> README.md
          echo "" >> README.md
          echo "It's worth noting that [cron is not guaranteed to run the scheduled time](https://upptime.js.org/blog/2021/01/22/github-actions-schedule-not-working/)" >> README.md
          echo "" >> README.md
          echo "To do this, I created `.github/workflows/cron.yml`" >> README.md
          echo "" >> README.md
          cat .github/workflows/cron.yml >> README.md
          
      - name: Push Changes
        run: |
          git config --global user.email "actions@users.noreply.github.com"
          git config --global user.name "README-bot"
          git add -A
          git commit -m "Updated content" || exit 0
          git push
