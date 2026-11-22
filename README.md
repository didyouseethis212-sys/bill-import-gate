# Bill Import Gate: duplicate invoice CSV preflight

Review incoming bill exports against imported history before a ledger import.

**[Try the free CSV checker](https://bill-import-gate.mayasmile.workers.dev/#csv-check)** — no sign-in, API key or upload. Click **Load CSV example**, review and confirm the scope, then **Check CSV files locally**. The three-row synthetic incoming batch returns two review findings; its different-vendor record stays unflagged.

## Start from spreadsheets

Download the [history CSV example](https://bill-import-gate.mayasmile.workers.dev/history-template.csv) and [incoming CSV example](https://bill-import-gate.mayasmile.workers.dev/incoming-template.csv). Map each export to:

```csv
id,entityId,vendorId,invoiceNumber,fiscalPeriod,documentType,currency,amountMinor,billDate
```

Use stable company/vendor IDs and explicit fiscal periods. Preserve leading zeroes in invoice references. `documentType` is `bill` or `credit_note`; `billDate` is a real ISO date; currency uses an uppercase three-letter code; `amountMinor` is a nonnegative integer in currency minor units, not a decimal amount. Arbitrary accounting-export headers are not auto-mapped.

The CSV checker supports quoted commas and rejects missing/duplicate headers, malformed CSV, decimal amounts and invalid records. Up to 5,000 rows per file, 2 MiB per CSV and 4 MiB combined mapped JSON in the local browser. Input edits hide stale results. Review findings against source documents before importing or paying anything.

## Manual checks or recurring API?

| Need | Path | Cost / data handling |
|---|---|---|
| Occasional manual review | Browser-local CSV or JSON checker | Free; input stays in your browser |
| Your own local automation | [Offline toolkit](https://bill-import-gate.mayasmile.workers.dev/package.zip) or [local n8n tutorial](https://bill-import-gate.mayasmile.workers.dev/workflow.json) | Free; no hosted API required |
| A hosted check inside recurring jobs | [RapidAPI plans](https://rapidapi.com/didyouseethis212sys/api/bill-import-gate/pricing) | BASIC 25 requests/month free; PRO $9/month for 500. Hard request limits; separate platform bandwidth fees/terms |

The hosted API accepts mapped JSON, **not raw CSV**. After a successful browser check, **Download mapped API request** exports the mapping; inspect it and follow the [API integration guide](https://bill-import-gate.mayasmile.workers.dev/guide.html). Hosted calls transmit the supplied JSON to the API. Start with a synthetic BASIC request and check the response before scheduling real intake. PRO is optional when the existing allowance no longer fits your recurring usage; no payment is required for the local tools.

## Reproduce without credentials

The original offline toolkit includes the pure module, CLI, synthetic JSON input and 34 module/HTTP tests:

```sh
node cli.mjs example.json
node --test test.mjs test-http.mjs
```

The flagged CLI example exits 2 with one repeated bill identity and one similar-reference candidate. The different-vendor row stays unflagged. The CSV release adds the browser parser and synthetic CSV fixtures; its 26 parser/router checks and live browser flagged/clean cases were verified separately. These are owner QA, not customer results.

The free n8n tutorial was actually imported and executed locally with two synthetic cases and no HTTP nodes, credentials, ledger writes or payments. It is not an official template-library entry or a claim of n8n Cloud verification.

## Scope and limitations

Exact matching uses company + vendor + document type + fiscal period + invoice reference. Different vendors, companies, periods and credit notes are not merged. Similar references are review candidates only when the documented scope/date/currency/amount checks also match. A clean report is not payment approval or proof that history is complete.

No OCR/PDF parsing, fuzzy vendor matching, bank/tax checks, currency conversion, automatic deletion, payment or ledger writeback. Existing accounting controls or a free script may already meet your needs. This is a cross-source pre-import review hypothesis; paying demand and savings are not validated. Maintained with AI assistance. No customer data or credentials belong in public issues.
