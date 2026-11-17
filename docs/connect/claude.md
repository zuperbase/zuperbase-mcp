# Connect Claude (web and desktop)

Custom connectors are available on Claude plans that allow them. Menu names change from time to time; if yours
differ, look for **Connectors** or **custom connector**.

1. Open **Settings › Connectors** and choose **Add custom connector**.
2. Name it **Zuperbase** and paste the address:
   ```text
   https://mcp.zuperbase.co/mcp
   ```
3. Choose **Connect**. Zuperbase opens in your browser.
4. Sign in, pick the organisation and what Claude may do (**Read only**, **Prepare drafts** or **Bookkeeper**) and the
   areas, then **Allow**.
5. In a chat, turn the Zuperbase connector on and ask: *Help me set up my business in Zuperbase.*

The Zuperbase skill (the rules for working in Zuperbase) is in
[`plugins/zuperbase/skills/zuperbase/SKILL.md`](../../plugins/zuperbase/skills/zuperbase/SKILL.md). Where Claude lets you
add skills, upload that folder as a skill. The connector sends the same rules on its own, so this is optional.

To change what Claude may do later: Zuperbase › Settings › Connected AI apps › **Change**.
