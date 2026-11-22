# IPIndex

IPIndex brings registered-IP diligence into Claude. Name a company and IPIndex
searches official patent, trademark, and copyright records in the United
States, Europe, and Canada, groups the results by owner, and links every record
to its official source. Turn a completed search into a citation-backed
diligence report, all through the hosted IPIndex service at
`https://mcp.ipindex.ai/mcp`.

## What IPIndex Searches

| Region | Source | Records |
| --- | --- | --- |
| United States | USPTO and U.S. Copyright Office | Patents, trademarks, and copyrights |
| Europe and worldwide | EPO (DOCDB/INPADOC) | Patent publications from European, PCT, and national offices such as the UK |
| Canada | CIPO | Patents and trademarks |

EPO results come from the EPO's DOCDB/INPADOC collection, and each publication
is linked to the official national record where the office publishes one. U.S.
records are searched by default. Ask to include the EPO or Canada and IPIndex
adds them to the same search.

## What You Can Do

- Search a company's portfolio, including former names and subsidiaries.
- Review the recorded assignment history of a U.S. patent or trademark.
- Look up a patent by its number and check its status.
- Run Deep Analysis on U.S. records to review recorded documents, prosecution
  history, and maintenance fee payments.
- Export results to a spreadsheet and generate a citation-backed report in
  HTML or PDF.

## Example Requests

- `Search all U.S. registered IP for Nalu Medical.`
- `Show the recorded assignment history for the first patent.`
- `Search U.S. and EPO patents for [company name], including former name [name].`
- `Search Canadian patents and trademarks for [company name].`
- `Generate a citation-backed diligence report from these results.`

## Getting Started

1. Add IPIndex from the Claude directory. In Claude Code you can also run
   `/plugin install ipindex --marketplace RedlineIQ/ipindex-plugins`.
2. Choose Connect when Claude asks. You sign in to your IPIndex account at
   `https://mcp.ipindex.ai` and approve access; Claude never sees your
   password.
3. Start a new conversation and ask for a search.

IPIndex requires an account with an IPIndex Pro subscription. Searches count
toward your monthly allowance, which is shared with the IPIndex app, and a Deep
Analysis uses five searches. Setup help, plan details and a subscribe link are
at https://mcp.ipindex.ai/support.

## What This Plugin Contains

- One skill that tells Claude how to run IPIndex searches, reports, and
  exports, and keeps IP research on IPIndex instead of general web browsing.
- One remote MCP server, `ipindex-mcp-hosted`, at `https://mcp.ipindex.ai/mcp`,
  connected with OAuth.

The plugin runs no local programs, hooks, or scripts and contains no
credentials.

## Data And Privacy

- **What is sent:** the requests you make through IPIndex tools (company
  names, patent or trademark numbers, search options, and research you choose
  to save) go to the IPIndex service at `mcp.ipindex.ai`, operated by
  BroadNarrow Labs, LLC. The plugin sends nothing anywhere else.
- **What IPIndex does with it:** IPIndex queries official record sources (the
  USPTO, the U.S. Copyright Office, and, only when you ask, the EPO and CIPO)
  from its own servers. For Deep Analysis it retrieves public documents from
  official sites with a managed cloud browser.
- **What is stored:** your saved research, generated reports, and the usage
  records needed to run your account, as described in the privacy policy.
- **Your control:** revoke Claude's access at any time at
  `https://mcp.ipindex.ai/settings/connectors`.

Privacy policy: https://www.ipindex.ai/privacy

## Support

- Help: https://mcp.ipindex.ai/support
- Website: https://www.ipindex.ai
- Terms: https://www.ipindex.ai/terms
- Privacy: https://www.ipindex.ai/privacy
- Email: info@ipindex.ai

IPIndex results are screening data from public registries. They are not legal
advice or a title opinion.
