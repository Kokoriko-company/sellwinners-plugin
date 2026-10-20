---
name: ad-creative-research
description: Research ad creatives on Meta (Facebook and Instagram), Google and TikTok, with their hooks, copy, calls to action and landing pages. Use when the user wants ad inspiration, asks what ads a brand or niche is running, which creatives are scaling, or wants to study one ad in detail.
---

# Research ad creatives

Use the tools of the SellWinners connector. Every call except `usage_get` and `check_credits` counts once against the user's monthly quota, so prefer the tools that answer in one call.

## Pick the tool

- **Inspiration for a niche or product:** `creative_inspiration_pack` with `niche`, `keywords`, `max_ads` and `focus`: `reach` for the biggest ads, `new` for ads launched in the last 14 days, `long_running` for ads running 30 days or more. Each ad comes with its hook, copy, call to action and landing page.
- **One brand's Meta ads:** call `lookup` with the brand name or domain to get its shop id, then `search_ads` with `filters` `{"websiteIds": [<shop id>]}`. That returns all of the brand's ads, not one per brand.
- **Meta ads across brands:** `search_ads` with `query` or `keywords`, `status` `active`, and a `sort_by`: `reach` for the biggest, `reachGrowth7d` or `rankDelta7d` for the ones scaling now, `longestRunning` for proven winners, `newest` for fresh tests. Narrow with `media_type` (image, video, carousel, dco, dpa) and `country`. Results keep one ad per brand unless `filters` raise `maxAdsPerBrand`.
- **One ad in full:** `scan_ad` with the ad's `id` from `search_ads`. It returns the creative, copy, video transcript and hook, spend, rank, the linked shop and the page's history.
- **Google ads:** `search_google_ads_library`.
- **TikTok ads and organic posts:** `search_tiktok_library` with `type` `ad`, `organic` or `all`, and `domain` or `handle` to keep one brand.

Search tools answer with `data` and `pagination`. Ask for the next `page` only when the user wants more.

`create_ad_share_link` makes a public link that anyone holding it can open. Call it only when the user asks for a shareable link.

## Answer

- Group the ads by angle or hook rather than listing them one by one.
- For each ad give the brand, the hook (its opening line), the format, how long it has run or its reach signal, the call to action, the landing page, and a link to the creative.
- Close with what is working across the set: recurring hooks, offers, formats and lengths.
- When the user wants their own ads, write new hooks and scripts from those patterns in their brand's voice; don't copy a competitor's copy word for word.
- When an answer carries `restrictions`, the user's plan shortened it. Say what was left out.

When a tool refuses with `plan_not_eligible`, or an answer's `restrictions` say it covers only the demo brands, the user is on the Free plan, which reads a fixed set of demo brands only. Don't retry with other brands or other tools. Tell the user which brands the demo covers (the message lists them) and that every other brand needs a paid SellWinners plan.
