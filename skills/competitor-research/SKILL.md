---
name: competitor-research
description: Brief a competitor's Shopify store, covering its profile and traffic, best-selling products, biggest and fastest-growing ads, email marketing, and similar stores. Use when the user names a competitor's brand or domain and asks how it sells, advertises or emails, or asks who a store's competitors are.
---

# Brief a competitor

Use the tools of the SellWinners connector. Every call except `usage_get` and `check_credits` counts once against the user's monthly quota.

## Steps

1. If the user gave a name that could match several brands, call `lookup` with it and confirm which one they mean. A domain needs no lookup.
2. Call `brief_competitor` with `competitor` set to the domain, name or shop id. With no `sections` it returns all of them: `profile`, `products`, `ads`, `emails`, `similar`. Its ads are the biggest by reach. To see the ads gaining rank instead, pass `ad_rank_sort` `rank_delta` and `ad_rank_window` `7d`, `14d` or `30d`.
3. Go deeper only where the user's question needs it:
   - **Email strategy:** `analyze_shop_emails` with `shop` gives the sending rhythm, the days, the campaign types and the latest subjects. `search_emails` with `shop` and `intent` (`promo`, `welcome`, `abandoned_cart`, `newsletter` or `all`) finds specific emails, and `get_email_html` returns one email's HTML.
   - **The brand's ad accounts:** `search_advertisers` with the brand name as `query`.
   - **More competitors:** `find_similar_shops` with `shop`, sorted by `monthlyVisits`, `activeAds` or `growth30d`.

## Answer

Write the brief in this order, and leave out any part the data doesn't cover:

1. **Snapshot:** traffic, main markets, active ads, product count.
2. **What they sell:** top products with prices and links.
3. **How they advertise:** main angles, formats and offers, with links to the top ads.
4. **How they email:** how often, which days, which campaign types, typical offers.
5. **Takeaways:** three to five concrete opportunities for the user.

When an answer carries `restrictions`, the user's plan shortened it. Say what was left out. Don't paste raw JSON.
