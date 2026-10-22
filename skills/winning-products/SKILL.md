---
name: winning-products
description: Find products that are selling now in a niche, and the Shopify stores behind them. Use when the user asks for winning products, product ideas, what to sell, trending or best-selling products, or the fastest-growing stores in a niche or country.
---

# Find winning products

Use the tools of the SellWinners connector. Every call except `usage_get` and `check_credits` counts once against the user's monthly quota, so answer with as few calls as the question needs.

These steps and answer formats are defaults. When the user explicitly asks for a different format, order, number of results or SellWinners tool, follow the user. The rules on confirmations, public links, the plan and the monthly quota always apply.

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

When a tool refuses with `plan_not_eligible`, or an answer's `restrictions` say it covers only the demo brands, the user is on the Free plan, which reads a fixed set of demo brands only. Don't retry with other brands or other SellWinners tools. Tell the user which brands the demo covers (the message lists them) and that other brands need a paid SellWinners plan, with the plans link the message gives.

When a tool answers that the monthly quota is used up, or that the plan doesn't include MCP access, stop calling SellWinners tools for this request. Tell the user in one sentence, with the reset date or the plans link the message gives.
