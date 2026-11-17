# Security and privacy

- **You sign in on Zuperbase.** The AI app never sees your password. You choose the organisation, the level and the
  areas on Zuperbase's own consent page.
- **OAuth 2.1 with PKCE.** Codes work once; refresh tokens rotate; tokens are stored only as hashes. Disconnecting
  an app stops every one of its tokens at once.
- **Inside the person's access.** Every call goes through the same checks as the person's own work in Zuperbase:
  their permissions, the connection's level and areas, approval limits, maker-checker and locked periods.
- **A full record.** Every save, posting and refusal is in the audit log with the app's name. Settings › Connected AI
  apps › *What AI apps did* lists them.
- **Limits.** Rate limits per address and per connection, and at most 300 saves a day per connection.
- **Hard limits.** No AI app can pay anyone, file a return, void a document, close a period, change users or
  permissions, or export or delete data.
- **Your data.** What the app reads is sent to its provider (for example Anthropic or OpenAI) and handled under
  their terms, which the consent page tells you before you allow it. Zuperbase does not use your data to train AI
  models.

Found a security issue? See [SECURITY.md](../SECURITY.md).
