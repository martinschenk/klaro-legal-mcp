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

**Three ways in, exactly one per call:** `text` for plain text, `pdf` for a
base64-encoded PDF, `images` for base64-encoded photos or scans of the pages
(JPEG, PNG, HEIC, WebP; up to 15 pages, 8 MB decoded in total). Photos and scans
without a text layer are read by OCR before the analysis, so a letter taken with
a phone works. Sending two of the three at once is rejected with a message
saying so. Files above 8 MB belong in the upload form on the website, which takes
up to 50 MB.
