---
name: winning-products
description: Find products that are selling now in a niche, and the Shopify stores behind them. Use when the user asks for winning products, product ideas, what to sell, trending or best-selling products, or the fastest-growing stores in a niche or country.
---

# Find winning products

Use the tools of the SellWinners connector. Tool calls count against the user's SellWinners plan (`usage_get` shows what is left), so answer with as few calls as the question needs.

## Steps

1. Settle the niche (a word such as `coffee` or `pet supplies`, or a category), one to five product keywords, and the market as a two-letter country code if the user named one. Ask only when the niche is missing.
2. Call `find_winning_products` with `niche`, `keywords`, `country` and `max_results` (how many shops, 1 to 30; start with 10). It returns the best sellers whose title matches a keyword, taken from the fastest-growing shops of the niche, up to three per shop. When the answer says no category matched the niche, tell the user the products were found by keyword alone.
3. To widen the list of stores, call `search_shops` with the niche words as `query`, the `country`, and `sort_by` set to `growth30d`, `estMonthlySales` or `unitsSold`. For an exact category, first call `lookup_filter_ids` with `type` `categories`, then pass the ids as `filters` `{"categoryIds": [...]}`.
4. For a store the user wants to go deeper on, `find_similar_shops` with its domain lists its competitors, and the competitor-research skill covers a full brief.

Search tools answer with `data` and `pagination`. Ask for the next `page` only when the user wants more results.

## Answer

- Start with a table: product, store domain, price when present, the signal that makes it a winner (growth, estimated sales, units sold) and a link.
- Follow with two or three sentences on the pattern across the list: shared angles, price bands, markets.
- When an answer carries `restrictions`, the user's plan shortened it. Say what was left out.
- Keep product and image URLs as links. Don't paste raw JSON.

When a tool says a request is outside the user's plan (`plan_not_eligible`), don't try to get the same data another way, with other brands or other SellWinners tools. Tell the user in one sentence what the message says, and answer the rest of the question with what the plan covers.
