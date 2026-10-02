# Installing the klaro.legal MCP server

The server is remote (Streamable HTTP) and needs no authentication. Nothing to
clone, build or run.

```json
{
  "mcpServers": {
    "klaro-legal": {
      "type": "streamableHttp",
      "url": "https://klaro.legal/api/mcp"
    }
  }
}
```

No API key, no account, no sign-up.

**Check that it works:** call `explain_document` with
`{"text": "The tenant pays a deposit of 1200 euro. Notice period is three months.", "language": "en"}`.
The answer explains both clauses in plain language and ends with a disclaimer
and a link to klaro.legal.

**If the answer says it is still running**, it returns an `analysis_id` — call
`get_explanation` with that id after about 30 seconds. A full document takes
20 to 60 seconds.

**Input is text, not files.** Pass the document text. If you hold a PDF, extract
its text first; the server does not accept binary uploads. For photos and scans
without a text layer, use the upload form on the website, which runs OCR.
