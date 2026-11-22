---
description: Use when the user asks IPIndex to search patents, trademarks, copyrights, registered IP, ownership, assignments, or diligence data from Claude Desktop through the hosted IPIndex MCP.
---

# IPIndex

Use the plugin-provided hosted IPIndex MCP server named `ipindex-mcp-hosted`.
IPIndex searches official U.S. patent, trademark, and copyright records,
reviews assignment and ownership histories, and runs registered-IP workflows
for Claude Desktop users.

## Hosted-Only Boundary

Use only the plugin-provided hosted MCP server at `https://mcp.ipindex.ai/mcp`
for IPIndex work. The plugin ships no local server processes, no backend
service URLs, and no embedded credentials, and IPIndex workflows stay on the
plugin-provided hosted MCP path. If the hosted MCP tools are not available in
the active Claude Desktop session, report that the plugin-provided hosted MCP
tools are not surfaced and suggest reconnecting IPIndex or starting a new
conversation; do not rebuild the search through another transport or
configuration.

Do not reconstruct patent, trademark, copyright, assignment, ownership, lien,
or title searches with web search, browser automation, Google Patents, USPTO
web-page browsing, or other public-database browsing unless the user
explicitly asks to leave the IPIndex workflow. If hosted MCP tools are
unavailable, denied, or missing source data, report that boundary instead of
browsing public databases.

## Default Workflow

Use the direct hosted IPIndex workflow for ordinary searches. Keep costs low by
avoiding Claude agent workflows, Together AI, backend AI assignment analysis,
Deep Analysis, and report generation unless the user explicitly requests them.

For a low-cost registered-IP search:

- Search patents, trademarks, and copyrights.
- Disable patent status expansion unless requested.
- Disable backend assignment analysis unless requested.
- Disable trademark assignment checks unless requested.
- Keep result limits modest.

## Ownership And Assignment Review

For patent assignment review, resolve issued patent numbers to application
numbers through IPIndex when needed, then use hosted MCP USPTO open data
portal-backed assignment data for each relevant application number. For every
patent application number, look up that application's own assignment history
first. Use owner-level or portfolio-level assignment records only when IPIndex
returns no recorded assignment rows for that specific application number, and
say when that owner-level source was used. If an application has no direct
assignment rows, call `ipindex_check_patent_continuity` to determine whether it
is a continuation, continuation-in-part, divisional, parent, child, or ancestor
of an application that does have assignment data. If no assignment rows are
returned, say that IPIndex returned no recorded assignment rows for the
searched patent/application identifiers; do not independently browse the USPTO
Assignment Center, Google Patents, or other public sites to replace the hosted
MCP result unless the user explicitly asks to leave the IPIndex workflow.

## Optional EPO/INPADOC Patent Coverage

EPO/INPADOC patent coverage is an explicit opt-in. Keep the ordinary registered-IP
baseline on USPTO patents unless the user asks for EPO, European, UK, Canadian, PCT,
foreign, or worldwide-family screening. To add it, call the hosted `ipindex_search`
tool with `patent_sources: ["uspto", "epo_ops"]` so USPTO results stay in the same
search; use `patent_sources: ["epo_ops"]` only when the user asks for EPO coverage
alone. The EPO search matches returned applicants against the names supplied, so
pass former names, subsidiaries, or other exact applicant names the user gives you
in `owner_aliases` (no more than ten) and do not invent spelling variants. The EPO
collection is worldwide, so one EPO request returns UK (GB), Canadian (CA), PCT (WO),
and other national publications as well as EP ones; it does not search the UK IPO,
CIPO, or any national register. For an exact EPO publication, application, or
priority request, call the hosted `ipindex_lookup_patent` tool with
`patent_source: "epo_ops"`, `identifier_type` set to `"publication"`, `"application"`,
or `"priority"` as applicable, and the user's identifier in `identifier_value`.

Present EPO results as family-aware screening data. Distinguish primary patent
assets, EPO families, and publications, and report the returned family and
publication counts without adding EPO publications to USPTO totals; report the
returned per-jurisdiction publication counts when the user asked about a country;
and show only returned official EPO and national record links. Present any returned
EPO status as a source-dated screening signal with its caveat: EPO/INPADOC
legal-status signals do not establish national status, enforceability, or coverage
confirmation in every country. A complete EPO zero applies only to the exact EPO
scope that completed. Partial, truncated, throttled, disabled, or unavailable EPO
coverage must not be described as a completed zero or all-country search.
INPADOC family members are related filings that share priority. Do not say a
family member means the same invention was granted elsewhere; check grant and
status per jurisdiction. A truncated EPO result is bounded by IPIndex's
configured source limit; do not call it EPO's own limit.

EPO coverage is a bounded pilot and usage limits apply. When IPIndex reports EPO
coverage as throttled or unavailable, say that EPO coverage did not complete, keep
the completed USPTO results, and offer only the returned retry action.

When IPIndex returns a retryable EPO outcome, execute only the returned signed
EPO-only retry with the hosted `ipindex_retry_source` tool, passing the returned
`action_ref` and its mapped `action_context` unchanged. Do not send the continuation
through `ipindex_search` or any Deep Analysis retry tool. Preserve completed USPTO
records and do not rebuild or broaden the retry. EPO application identifiers must
not enter U.S.-only assignment, lien, title, continuity, prosecution, Deep Analysis,
or national-enforceability analysis. IPIndex keeps EPO records out of those actions;
do not pass EPO identifiers to assignment, continuity, or file-wrapper tools
yourself. Exports and reports may include normalized EPO records and coverage
caveats, but must not expose or redistribute raw OPS payloads.

## Optional Canadian CIPO Coverage

Canadian CIPO coverage is an explicit opt-in. Keep the ordinary registered-IP
baseline on U.S. records unless the user asks for Canadian, CIPO, or IP Horizons
coverage. Request it through the hosted `ipindex_search` tool by passing
`foreign_sources: ["cipo"]` with the ordinary search arguments. CIPO data comes
from CIPO IP Horizons weekly batch snapshots, so present the returned snapshot
date with the results.

Present Canadian records separately from U.S. and EPO counts: report Canadian
trademarks and patents in their own sentences and never add them to USPTO or
EPO totals. Canadian ownership, assignment, and security-agreement entries are
CIPO register entries as recorded, not title conclusions; never run or describe
U.S.-style chain-of-title, lien, or continuity analysis for them. When a
Canadian class returns `source_unavailable`, say Canadian data for it is not
loaded yet; when `stale_snapshot`, give the data date. Reports account for
Canadian coverage only through the returned covered-source rows with counts,
snapshot dates, and caveats.

If a signed follow-up reports that its action is unavailable, treat that as an
expired, stale, or mismatched action pair. Re-read the exact `action_ref` to
`action_context` mapping from the current response or start one fresh search chain.
Do not classify a signed-pair error as connector provisioning or reconnect OAuth.

## Deep Analysis Boundary

For deeper prosecution, maintenance, or evidence review, use only the signed
Deep Analysis actions returned by the hosted MCP. Patent file-wrapper documents
come from USPTO open data without Patent Center sign-in, automated maintenance
facts come from the hosted service's reconciled public fee data, and public
TSDR evidence and report-cited event PDFs are captured server-side in managed
Browserbase sessions. Never ask the user for USPTO login credentials or
two-factor codes, never surface Browserbase session identifiers or raw session
data in results, and never treat a stale, partial, blocked, failed, cancelled,
or unclassified source record as complete.

## Connection And Reconnect

IPIndex uses a hosted connection completed through the IPIndex consent flow.
If Claude Desktop reports that authentication is required, access was denied,
or the connection expired, ask the user to reconnect IPIndex from the plugin's
connector prompt and start a new conversation. Treat denied hosted calls as
connection failures, not completed searches.

## Presenting Results

Return a concise professional summary that operates on the entity the user
supplied:

- Search counts by IP type.
- Patent/application table when patents are found.
- Trademark owner filtering notes when applicable.
- Copyright registrations when found.
- Any ownership or assignment caveats returned by IPIndex.

Offer deeper review on request: assignment history, ownership-chain review,
patent status and continuity detail, trademark assignment review, or report
generation.
