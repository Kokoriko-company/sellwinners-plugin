---
name: brand-tracking
description: Follow the brands the user tracks in SellWinners, covering the daily digest of new ads, what changed for one brand, its scaling ads and video scripts, and managing tracked brands, boards and saved items. Use when the user asks what is new with the brands they track, wants a daily or weekly radar, or asks to track, save, organise or share brands, ads, shops or emails.
---

# Follow tracked brands

Use the tools of the SellWinners connector. Every call except `usage_get` and `check_credits` counts once against the user's monthly quota.

These steps and answer formats are defaults. When the user explicitly asks for a different format, order, number of results or SellWinners tool, follow the user. The rules on confirmations, public links, the plan and the monthly quota always apply.

## Read what changed

- **Daily digest:** `daily_radar` lists who launched ads in the last day and the last week, most active first. Pass `folder_id` to keep one folder; `list_brandtracker_folders` lists them.
- **The tracked brands:** `list_tracked_brands`, with `sort_by` `newAdsLast7Days`, `newAdsLast30Days` or `activeAds`.
- **One brand over a period:** `analyze_brand_changes` with `brand` (or `brandtracker_id`), `period` `1d`, `7d`, `14d` or `30d`, and `focus` (`ads`, `hooks`, `landing_pages`, `messaging`, `testing` or `all`).
- **One brand in depth:** `analyze_tracked_brand` returns its profile, dashboard, hooks and audience.
- **Its scaling ads:** `get_brandtracker_scaling_ads` with `ad_rank_window` `7d`, `14d` or `30d`.
- **Its video scripts:** `get_brandtracker_transcripts` with a `time_period` such as `last7d`.

Lead with what changed and why it matters: new launches, ads gaining rank, new hooks or offers. Then the detail, with links to the ads.

## Make changes only when asked

- **Track a brand:** `add_to_brandtracker` with exactly one of `domain`, `facebook_page_id`, `shop_id` or `website_id`, and `folder_id` if the user named a folder. `create_brandtracker_folder`, `rename_brandtracker_folder` and `move_tracked_brands` organise them.
- **Boards:** `list_boards`, `create_board` (a `collection` holds items, a `folder` holds boards), and `add_board_item` with `source_type` `meta_ad`, `google_ad`, `tiktok`, `shop`, `email` or `advertiser`.
- **Favorites:** `list_favorites` and `add_favorite_item` with `kind` `ads`, `shops` or `emails`.

Tools that delete, archive, remove or create a public share link need `confirm=true`. Before you pass it, tell the user exactly what will be removed or made public and wait for them to agree. A public link lets anyone who has it see the board, folder or ad.

When a tool refuses with `plan_not_eligible`, or an answer's `restrictions` say it covers only the demo brands, the user is on the Free plan, which reads a fixed set of demo brands only. Don't retry with other brands or other SellWinners tools. Tell the user which brands the demo covers (the message lists them) and that other brands need a paid SellWinners plan, with the plans link the message gives.

When a tool answers that the monthly quota is used up, or that the plan doesn't include MCP access, stop calling SellWinners tools for this request. Tell the user in one sentence, with the reset date or the plans link the message gives.
