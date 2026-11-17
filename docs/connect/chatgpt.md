# Connect ChatGPT

Custom connectors are available on ChatGPT plans that offer them, through developer mode. Menu names change from
time to time; if yours differ, look for **Apps & Connectors** or **connectors**.

1. Open **Settings › Apps & Connectors**, then **Advanced**, and turn on **developer mode**.
2. Create a connector named **Zuperbase** with this address:
   ```text
   https://mcp.zuperbase.co/mcp
   ```
   Choose OAuth as the sign-in method if asked.
3. Zuperbase opens in your browser. Sign in, pick the organisation and the access, then **Allow**.
4. In a new chat, add the Zuperbase connector and ask: *Who owes us money, and how long overdue is each one?*

ChatGPT gets Zuperbase's working rules from the connector itself. Read what it prepares before you approve it.

To change what ChatGPT may do later: Zuperbase › Settings › Connected AI apps › **Change**.
