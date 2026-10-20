# SellWinners for Claude

![SellWinners](assets/logo.png)

SellWinners gives Claude e-commerce and advertising intelligence. Ask in plain words and Claude finds products that are selling now, studies the ads behind them on Meta, Google and TikTok, briefs a competitor's Shopify store and email marketing, and tells you what changed for the brands you track.

The plugin connects Claude to the SellWinners MCP server and adds four skills that tell Claude which tools to use for each kind of question and how to present the answer.

## What you can ask

- "Find winning products in the pet supplies niche in the US."
- "Show me the strongest running video ads for collagen supplements, and what their hooks have in common."
- "Brief me on gymshark.com: products, ads and emails."
- "What did the brands I track launch this week?"
- "Track allbirds.com and save its three biggest ads to my Footwear board."

## Skills

| Skill | Use it for |
| - | - |
| `winning-products` | Best-selling products in a niche and the fastest-growing stores that sell them |
| `ad-creative-research` | Meta, Google and TikTok ads: hooks, copy, calls to action, landing pages, scaling creatives |
| `competitor-research` | A brief on one store: profile, products, ads, emails and similar stores |
| `brand-tracking` | Daily radar and changes for tracked brands, plus tracking, boards and saved items |

In Claude Code you can also run each one directly, for example `/sellwinners:competitor-research gymshark.com`.

## Setup

1. Create a SellWinners account at [sellwinners.com](https://sellwinners.com) and an API key at [sellwinners.com/dashboard/keys](https://sellwinners.com/dashboard/keys).
2. Install the plugin. Claude Code asks for the API key when the plugin is enabled and keeps it in your system's secure credential store, not in a settings file.
3. Ask a question. Claude calls the SellWinners tools it needs.

## Plans

- **Paid plans** read every brand, store, ad and email, within the plan's monthly quota and rate limit.
- **Free** is a demo: the tools answer only about a fixed set of demo brands, which the answers list. A question about any other brand is refused, and Claude tells you which brands the demo covers instead of retrying.

Plans, prices and quotas are on the [pricing page](https://sellwinners.com/pricing).

## What the plugin sends, and where

- The plugin itself runs no code on your machine and stores nothing. It contains only skills (Markdown) and one MCP server reference.
- Claude sends each tool call to the SellWinners MCP server at `https://mcp.sellwinners.com/mcp` over HTTPS, with your API key in the `X-API-Key` header. A call carries only the arguments Claude chose for that tool, such as a niche, keywords, a store domain or an ad id. Your conversation is not sent.
- SellWinners counts each tool call once against your plan's monthly quota, except the usage tools (`usage_get`, `check_credits`), and keeps a request log for metering, abuse prevention and support. The [privacy policy](https://sellwinners.com/privacy) covers what is kept and for how long.
- Write tools change your own SellWinners account only: tracked brands, boards, favorites and share links. Tools that delete, archive or create a public link require an explicit confirmation, and the skills tell Claude to ask you first.
- Answers can contain links to ad images, videos and product pages. Opening one fetches it from SellWinners or from the store that hosts it.

## Privacy

The [SellWinners privacy policy](https://sellwinners.com/privacy) applies to everything the plugin sends. It describes the data collected, how it is used and stored, which providers process it, how long it is kept, and how to reach us. The plugin collects no data of its own.

## Support

- Documentation: [sellwinners.com/docs](https://sellwinners.com/docs) and [sellwinners.com/mcp](https://sellwinners.com/mcp)
- Contact: [sellwinners.com/contact](https://sellwinners.com/contact) or support@sellwinners.com
- Terms: [sellwinners.com/terms](https://sellwinners.com/terms)

## License

MIT. See [LICENSE](LICENSE).
