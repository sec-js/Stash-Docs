---
title: Scraping metadata behind login
hide:
  - toc
---


A regular scraper can only scrape information from webpages that are open to public access. If you want to scrape a webpage that requires login or is behind a paywall, you need to use the "Visible CDP" technique.


Normal CDP scraping will launch a headless Chrome browser, which will not show up for any user interactions. "Visible CDP" turns the "headless Chrome" into a visible instance.

1. Prepare your scraper's .yml file and make sure it's valid and working. Your scraper should have the following setting inside:
```yaml
driver:
  useCDP: true
```
2. Open a command console. Go to Chrome's binary directory and run `chrome.exe --remote-debugging-port=9222`. This will launch a special Chrome instance that Stash scrapers can control later on.
3. In Stash, make sure that **Settings** > **Metadata Providers** > **Scraping** > **Chrome CDP Path** is set to `http://localhost:9222/json/version`.
4. Using the special Chrome instance you launched earlier, go to the webpage you want to scrape, log in with your username and password or pass any other human tests, until you see the page with the desired content.
5. Paste the webpage's URL in your Stash scene and start scraping. It should retrieve the information correctly.