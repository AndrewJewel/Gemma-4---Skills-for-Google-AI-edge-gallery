---
name: latam-pulse
description: Fetches and summarizes the latest business, tech, and startup news from Latin America in real time. Use this skill whenever the user asks about current LATAM news, mercados latinoamericanos, startups en LATAM, business headlines, latest tech news, or says things like "qué está pasando en LATAM", "noticias de negocios", "últimas noticias tech", "what's happening in Mexico/Brazil/Argentina/Colombia", or wants a market briefing. Returns an interactive responsive card with the top headlines.
metadata:
  homepage: https://github.com/google-ai-edge/gallery/discussions/categories/skills
---

# LATAM Pulse

A real-time business and tech news skill focused on Latin America.
Pulls fresh headlines from Google News RSS (routed through public CORS
proxies, since Google News does not emit CORS headers), filters them by
topic and region, and renders an interactive, responsive briefing card
directly in the chat.

No API key required.

Built for entrepreneurs, founders, and operators who need to stay current
on LATAM markets without leaving their phone.

---

## Instructions

Call the `run_js` tool with the following exact parameters:

- script name: index.html
- data: A JSON string with the following fields:
  - topic: String. The topic to search for. Must be one of:
    "business", "technology", "startups", "fintech", "general".
    Default to "business" if the user does not specify.
  - country: String. Two-letter ISO country code. Must be one of:
    "mx" (Mexico), "br" (Brazil), "ar" (Argentina), "co" (Colombia),
    "cl" (Chile), "pe" (Peru), "all" (all of LATAM).
    Default to "all" if the user does not specify a country.
  - language: String. Either "es" (Spanish) or "en" (English).
    Default to "es" unless the user is writing in English.

## How to interpret the user's request

1. **Detect topic** — Map the user's intent to one of the 5 topics above.
   - "startup", "founder", "VC", "fundraising" → `startups`
   - "fintech", "neobank", "payments" → `fintech`
   - "tech", "AI", "software" → `technology`
   - "economy", "markets", "business" → `business`
   - Anything else → `general`

2. **Detect country** — If the user mentions a specific country, use its
   ISO code. Otherwise default to `all`.

3. **Detect language** — Mirror the language of the user's prompt.

4. **Call the tool** with the JSON string. Do not add commentary before
   the tool call — let the webview render the result.

5. **After the tool returns**, briefly acknowledge the result in 1 sentence
   (in the user's language) and ask if they want a deeper analysis of any
   specific headline.

## Example user prompts that should trigger this skill

- "Qué noticias hay de startups en México hoy?"
- "Dame el pulso de negocios en LATAM"
- "What's happening with fintech in Brazil?"
- "Últimas noticias tech"
- "Briefing del día"
