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

You need a SellWinners account. What the tools can do depends on your plan; see [Plans](#plans).

1. Create an account at [sellwinners.com](https://sellwinners.com) if you don't have one.
2. Install the plugin and connect it to your account:
   - **claude.ai, Claude Desktop or Cowork:** add SellWinners from **Customize → Plugins → Discover**, open its **Connectors** tab, select **Add** if it shows Not added, then **Connect**. On Team or Enterprise plans, an Owner adds the connector first.
   - **Claude Code:** install it with `/plugin install sellwinners --marketplace Kokoriko-company/sellwinners-plugin` (Claude Code 2.1.275 or later; or install it from `/plugin`), then run `/mcp`, choose the **sellwinners** server (listed as `plugin:sellwinners:sellwinners`) and select **Authenticate**. Claude Code stores the sign-in with its other credentials and renews it on its own.

   Either way your browser opens SellWinners. Log in as usual and select **Allow**. If you're in more than one SellWinners workspace, the same page asks which one Claude works in: the connection then uses that workspace's plan, saved items and tracked brands, and uses its credits.
3. Ask a question. Claude calls the SellWinners tools it needs.

To disconnect, open **Dashboard → MCP server → Connected apps** on sellwinners.com and select **Disconnect**. In Claude Code, **Clear authentication** in `/mcp` also ends the connection on SellWinners. A connection that goes unused ends on its own after 60 days.

**Using an API key instead.** For scripts and machines where no browser can open, leave the plugin's sign-in aside and add the server with a key from [sellwinners.com/dashboard/keys](https://sellwinners.com/dashboard/keys):

```bash
claude mcp add --transport http sellwinners-key https://mcp.sellwinners.com/mcp --header "X-API-Key: YOUR_KEY"
```

With a key, used-up credits, the rate limit or a plan without MCP access comes back as an HTTP error (402, 429 or 403) that gives the reason. A tool your plan doesn't include answers with a short message, as it does when you're signed in.

## Plans

Your SellWinners plan decides what the tools can do, how many credits you have each month and how fast you can use them. A tool call costs one credit for each result it returns (one product, one ad, one row of a list); an empty answer and an error cost nothing. Plans are described on the [pricing page](https://sellwinners.com/pricing).

When you're signed in and a request is outside your plan, or your credits for the month are used up, the tool answers with a short message. Claude tells you what it says, with the link SellWinners gives, and doesn't try to get around it.

## What the plugin sends, and where

- The plugin itself runs no code on your machine and stores nothing. It contains only skills (Markdown) and one MCP server reference.
- Signing in happens on sellwinners.com, in your browser. Claude never sees your password. SellWinners gives Claude an access token that lasts one hour and a refresh token that renews it; the connection appears under **Dashboard → MCP server → Connected apps** until you disconnect it.
- Claude sends each tool call to the SellWinners MCP server at `https://mcp.sellwinners.com/mcp` over HTTPS, with the access token in the `Authorization` header. A call carries only the arguments Claude chose for that tool, such as a niche, keywords, a store domain or an ad id. Your conversation is not sent.
- Tool calls use your plan's credits, as the [pricing page](https://sellwinners.com/pricing) describes. SellWinners keeps a request log for metering, abuse prevention and support. The [privacy policy](https://sellwinners.com/privacy) covers what is kept and for how long.
- Write tools change your own SellWinners account only: tracked brands, boards, favorites and share links. Tools that delete or archive something or create a public link require an explicit confirmation, and the skills tell Claude to ask you first.
- Answers can contain links to ad images, videos and product pages. Opening one fetches it from SellWinners or from the store that hosts it.

## Privacy

The [SellWinners privacy policy](https://sellwinners.com/privacy) applies to everything the plugin sends. It describes the data collected, how it is used and stored, which providers process it, how long it is kept, and how to reach us. The plugin collects no data of its own.

## Support

- Documentation: [sellwinners.com/mcp](https://sellwinners.com/mcp) and the API reference at [sellwinners.com/docs](https://sellwinners.com/docs)
- Contact: [sellwinners.com/contact](https://sellwinners.com/contact) or support@sellwinners.com
- Security issues: support@sellwinners.com, with "Security" in the subject
- Terms: [sellwinners.com/terms](https://sellwinners.com/terms)

## Repository layout

The same folder is also the source of the SellWinners plugin for ChatGPT. Each directory reads its own manifest, and both use the same skills and the same MCP server:

| Files | Used by |
| - | - |
| `.claude-plugin/plugin.json`, `.claude-plugin/marketplace.json`, `.mcp.json` | Claude |
| `plugin.json`, `mcp.json` ([Agent Plugins](https://agent-plugins.org) format) | ChatGPT |
| The skills folder and the images folder | Both |

Claude ignores the ChatGPT files. The ChatGPT package is a ZIP of the ChatGPT files, the skills and the images.

## License

MIT. See [LICENSE](LICENSE).
