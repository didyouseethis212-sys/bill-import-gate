# Bill Import Gate

Review bill batches before ledger import.

**[Try the free local checker](https://bill-import-gate.mayasmile.workers.dev/)** — no sign-in; mapped JSON stays on your device.

**[Download the local toolkit and 34 tests](https://bill-import-gate.mayasmile.workers.dev/package.zip)** · [Input and API guide](https://bill-import-gate.mayasmile.workers.dev/guide.html)

## Reproduce the example

Unzip the toolkit, then run `node cli.mjs example.json`. Expected exit code2: one repeated bill identity, one similar-reference review candidate, and one different-vendor record left unflagged. Run `node --test test.mjs test-http.mjs` for34tests. No production credentials are included.

## Intended workflow

Combine exported history and incoming bill records from your intake sources, map stable company/vendor IDs and explicit fiscal periods, then review findings before importing into a ledger. Each row needs id, entityId, vendorId, invoiceNumber, fiscalPeriod, documentType, currency, amountMinor and billDate. Exact amount arithmetic uses integer minor units. Different vendors, entities, periods and credit notes are not merged.

Hosted API sales activation is pending. Do not treat the hosted adapter as a live paid product yet. The browser checker and local toolkit are available now.

## Limitations and disclosure

Findings are review candidates, not proof of duplicate payment. No bank checks, tax validation, OCR/PDF, raw CSV mapping, fuzzy vendor matching, currency conversion, automatic deletion, payment or ledger writeback. A clean result is not payment approval. Operator mapping and relevant history completeness matter.

Existing accounting systems and free scripts may already solve your problem. The cross-source pre-import workflow is a value hypothesis; no paying users or financial savings are claimed. I maintain this tool, developed with AI assistance. Browser checks are local; a future hosted request transmits its supplied JSON.
