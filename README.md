# Bill Import Gate

Review bill batches before ledger import.

**[Try the free local checker](https://bill-import-gate.mayasmile.workers.dev/)** — no sign-in; mapped JSON stays on your device.

**[Download the local toolkit and 34 tests](https://bill-import-gate.mayasmile.workers.dev/package.zip)** · [Input and API guide](https://bill-import-gate.mayasmile.workers.dev/guide.html)

## Reproduce the example

Unzip the toolkit, then run `node cli.mjs example.json`. Expected exit code2: one repeated bill identity, one similar-reference review candidate, and one different-vendor record left unflagged. Run `node --test test.mjs test-http.mjs` for34tests. No production credentials are included.

## Intended workflow

Combine exported history and incoming bill records from your intake sources, map stable company/vendor IDs and explicit fiscal periods, then review findings before importing into a ledger. Each row needs id, entityId, vendorId, invoiceNumber, fiscalPeriod, documentType, currency, amountMinor and billDate. Exact amount arithmetic uses integer minor units. Different vendors, entities, periods and credit notes are not merged.

**[Choose an API plan](https://rapidapi.com/didyouseethis212sys/api/bill-import-gate/pricing)** — BASIC25requests/month free, PRO$9/month for500requests, hard request limits; platform bandwidth fees and terms separate. Hosted POST /bills/preflight is live and verified with one owner test (not customer activity).

**[Free n8n local tutorial](https://bill-import-gate.mayasmile.workers.dev/workflow.json)**: native n8n import and two-case execution verified locally. No HTTP nodes, credentials or ledger writes. Not a published n8n template-library entry and not tested in n8n Cloud.

## Limitations and disclosure

Findings are review candidates, not proof of duplicate payment. No bank checks, tax validation, OCR/PDF, raw CSV mapping, fuzzy vendor matching, currency conversion, automatic deletion, payment or ledger writeback. A clean result is not payment approval. Operator mapping and relevant history completeness matter.

Existing accounting systems and free scripts may already solve your problem. The cross-source pre-import workflow is a value hypothesis; no paying users or financial savings are claimed. I maintain this tool, developed with AI assistance. Browser checks are local; a future hosted request transmits its supplied JSON.
