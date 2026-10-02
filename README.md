<img src="assets/logo-400.png" width="72" alt="klaro.legal">

# klaro.legal MCP server: contracts and official letters in plain language

Paste a contract, an official letter, a tax assessment or a set of terms and
conditions, and get it back explained clause by clause in everyday language,
from Claude, ChatGPT, Cursor or any MCP client. Text, a PDF or photos of the
pages all work: a photographed letter is read by OCR before the analysis. Six
languages. No account, no API key. Hosted by [klaro.legal](https://klaro.legal);
this repository holds the public metadata, the server code is not open source.

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

- `explain_document`: send the document as `text`, as a base64-encoded `pdf`, or
  as base64-encoded `images` of its pages (JPEG, PNG, HEIC, WebP; up to 15 pages
  and 8 MB decoded). Exactly one of the three. `language` picks the language of
  the explanation. Returns a short summary plus one entry per clause: the
  original wording, then what it means. Plain text takes 20 to 60 seconds, a
  scan or photo longer because of OCR. *read-only*
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

## Text, PDF or photos

Three ways in, one at a time:

- **`text`** — the fastest route. Most clients already extract the text of a PDF
  by themselves, and then this is all that is needed.
- **`pdf`** — the file itself, base64-encoded, up to 8 MB decoded. Used when the
  PDF has no usable text layer, or when its layout carries meaning.
- **`images`** — photos or scans of the pages, base64-encoded, in page order, up
  to 15 pages and 8 MB decoded in total. This is the route for a letter someone
  photographed with a phone: OCR reads it first, then the analysis runs.

Anything larger than 8 MB is better handled by the
[upload form](https://klaro.legal/en-us), which takes files up to 50 MB — a
base64 payload travels through the client's context window, and that is where
the limit comes from, not from the analysis.

## Privacy

Documents are anonymised before the analysis and processed inside the EU. The
analysis itself runs on AWS Bedrock in Paris (`eu-west-3`); the text is not sent
to any other AI provider. Details: [klaro.legal/en-us/privacy](https://klaro.legal/en-us/privacy)

## Also available

- **Upload form** in the browser, for files above 8 MB and up to 50 MB:
  [klaro.legal](https://klaro.legal/en-us)
- **Embeddable widget** for your own site, in all six interface languages:
  [klaro.legal/en-us/embed-widget](https://klaro.legal/en-us/embed-widget)

---

Operated by Martin Schenk S.L., Madrid · [klaro.legal](https://klaro.legal) ·
questions: info@klaro.legal
