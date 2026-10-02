<img src="assets/logo-400.png" width="72" alt="klaro.legal">

# klaro.legal MCP server: contracts and official letters in plain language

Paste a contract, an official letter, a tax assessment or a set of terms and
conditions, and get it back explained clause by clause in everyday language,
from Claude, ChatGPT, Cursor or any MCP client. Six languages. No account, no
API key. Hosted by [klaro.legal](https://klaro.legal); this repository holds the
public metadata, the server code is not open source.

```
https://klaro.legal/api/mcp
```

Streamable HTTP · no authentication · listed in the
[official MCP registry](https://registry.modelcontextprotocol.io/v0/servers?search=klaro)
as `legal.klaro/document-explainer` and as a
[Glama connector](https://glama.ai/mcp/connectors/legal.klaro/document-explainer).

[![klaro.legal MCP connector](https://glama.ai/mcp/connectors/legal.klaro/document-explainer/badges/score.svg)](https://glama.ai/mcp/connectors/legal.klaro/document-explainer)

## What it explains, and what it does not

It explains **what a document says**. It does not review it, score it, flag
clauses as unfair, or tell you what to do. That line is deliberate: klaro.legal
is software, not a law firm. What matters in your case is for a qualified lawyer
to decide, and every answer says so.

Typical documents: rental agreements, employment contracts, letters from a tax
office or an immigration authority, insurance policies, terms and conditions,
utility and telecoms contracts.

## Tools

- `explain_document`: send the document text and, optionally, the language the
  explanation should be written in. Returns a short summary plus one entry per
  clause: the original wording, then what it means. Takes 20 to 60 seconds.
- `get_explanation`: if `explain_document` was still running, it returns an
  `analysis_id` — pass it here to pick up the finished result. *read-only*

Explanation languages: `de`, `en`, `es`, `fr`, `it`, `pt`. The document itself
may be in any language.

## Setup

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

See [llms-install.md](llms-install.md) for a one-call check that it works.

## Text in, not files

The tool takes **text**. If you hold a PDF, let your assistant extract the text
first — most clients do that by themselves. Photos and scans without a text
layer will not work this way; for those, use the upload form on the website,
which runs OCR before the analysis.

## Privacy

Documents are anonymised before the analysis and processed inside the EU. The
analysis itself runs on AWS Bedrock in Paris (`eu-west-3`); the text is not sent
to any other AI provider. Details: [klaro.legal/en-us/privacy](https://klaro.legal/en-us/privacy)

## Also available

- **Upload form** in the browser, including photos and scans:
  [klaro.legal](https://klaro.legal/en-us)
- **Embeddable widget** for your own site, in all six interface languages:
  [klaro.legal/en-us/embed-widget](https://klaro.legal/en-us/embed-widget)

---

Operated by Martin Schenk S.L., Madrid · [klaro.legal](https://klaro.legal) ·
questions: info@klaro.legal
