# Apple Podcasts Scraper & Unofficial API (Python, Node.js, MCP)

[Run Apple Podcasts Scraper - Charts, Search & RSS Feeds on Apify](https://apify.com/evpp/apple-podcasts-charts) to export Apple Podcasts data as clean JSON, CSV, Excel, or an API feed. This repository is a developer quick-start kit with working Python and Node.js clients, an MCP configuration, a real sample dataset, and an n8n automation template.

[![Run on Apify](https://img.shields.io/badge/Run%20on-Apify-orange)](https://apify.com/evpp/apple-podcasts-charts)

## Why use this Apple Podcasts scraper?

- Export Apple Podcasts data without building or maintaining a custom scraper
- Get flat, schema documented JSON ready for analytics, lead generation, market research, and AI agents
- Run manually, on a schedule, through the Apify API, or through MCP compatible AI tools
- Use the included 25+ row sample dataset to prototype before running the live Actor

Built for Podcast booking agencies, PR firms, ad networks, podcast hosting competitors.

## Quick start on Apify

Open [https://apify.com/evpp/apple-podcasts-charts](https://apify.com/evpp/apple-podcasts-charts) and use this input:

```json
{
  "country": "us",
  "chart": "top",
  "genreId": "1488",
  "includeFeedUrl": true,
  "maxItems": 10
}
```

## Python

```bash
pip install -r requirements.txt
export APIFY_TOKEN=your_apify_token
python python/run.py
```

On Windows PowerShell, use `$env:APIFY_TOKEN="your_apify_token"` instead of `export`.

## Node.js

```bash
npm install
export APIFY_TOKEN=your_apify_token
node node/run.mjs
```

## MCP and AI agents

Add the hosted Apify MCP server from `mcp-config.json` to your MCP client:

```json
{
  "mcpServers": {
    "apify": {
      "type": "http",
      "url": "https://mcp.apify.com/?tools=evpp/apple-podcasts-charts"
    }
  }
}
```

Then ask your agent to run `evpp/apple-podcasts-charts`, inspect the output schema, or export the latest dataset. The direct MCP URL is `https://mcp.apify.com/?tools=evpp/apple-podcasts-charts`.

## n8n automation

Import `n8n-workflow.json` into n8n, select your Apify credential, replace the webhook placeholder, and activate the schedule. The workflow runs the Actor every morning and posts fresh dataset items to your webhook.

## Output schema

| Field | Type | Description |
|---|---|---|
| `podcastId` | string | Apple podcast collection ID |
| `name` | string | Podcast show title |
| `artistName` | string | Podcast creator / publisher name |
| `url` | string | Apple Podcasts page URL |
| `feedUrl` | string | RSS feed URL of the podcast (resolved via iTunes Lookup) |
| `primaryGenre` | string | Primary Apple Podcasts genre |
| `genres` | string[] | All Apple Podcasts genres the show is listed under |
| `artworkUrl` | string | Podcast cover artwork image URL |
| `releaseDate` | string | Release date of the latest episode as reported by Apple |
| `description` | string | Short show summary when provided by the source feed |
| `episodeCount` | integer | Number of episodes reported by iTunes Lookup |
| `contentAdvisoryRating` | string | Apple content advisory rating (e.g. Clean, Explict) |
| `rank` | integer | 1-based position in the chart (chart mode only) |
| `searchQuery` | string | Search term that produced this item (search mode only) |
| `country` | string | Storefront country code the item was scraped from |

## Real sample output

The first sanitized row from the included sample dataset:

```json
{
  "podcastId": "1322200189",
  "name": "Crime Junkie",
  "artistName": "Audiochuck",
  "url": "https://podcasts.apple.com/us/podcast/crime-junkie/id1322200189?uo=2",
  "feedUrl": "https://feeds.simplecast.com/qm_9xx0g",
  "primaryGenre": "True Crime",
  "genres": [
    "True Crime"
  ],
  "artworkUrl": "https://is1-ssl.mzstatic.com/image/thumb/Podcasts126/v4/8c/35/04/8c350430-2fbf-98d0-0a25-00b76550ffeb/mza_13445204151221888086.jpg/170x170bb.png",
  "releaseDate": "2026-11-23T00:00:00-07:00",
  "description": "Does hearing about a true crime case always leave you scouring the internet for the truth behind the story? Dive into your next mystery with Crime Junkie. Every Monday, join your host Ashley Flowers as she unravels all the details of infamous and underreported true crime cases with her best friend Brit Prawat. From cold cases to missing persons and heroes in our community who seek justice, Crime Junkie is your destination for theories and stories you won’t hear anywhere else. \n\nWhether you're a seasoned true crime enthusiast or new to the genre, you'll find yourself on the edge of your seat awaiting a new episode every Monday.\n\nIf you can never get enough true crime... Congratulations, you’ve found your people. Follow to join a community of Crime Junkies! \n\nCrime Junkie is presented by Audiochuck Media Company.",
  "episodeCount": 537,
  "contentAdvisoryRating": "Clean",
  "rank": 1,
  "country": "us"
}
```

## Files in this kit

| File | Purpose |
|---|---|
| `python/run.py` | Working Python Apify API example |
| `node/run.mjs` | Working Node.js Apify API example |
| `mcp-config.json` | MCP server configuration for AI agents |
| `sample-output.json` | First five sanitized sample rows |
| `dataset-snapshot.csv` | 25+ row evaluation snapshot |
| `DATASET_CARD.md` | Dataset documentation and provenance |
| `n8n-workflow.json` | Scheduled n8n automation template |

## Fresh data

This repository contains a static evaluation sample. For current data, run the live Actor: https://apify.com/evpp/apple-podcasts-charts

## Responsible use

The Actor reads public data from `podcasts.apple.com`. Review the source site's terms and applicable privacy rules before production use.
