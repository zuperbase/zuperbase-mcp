<!-- Generated from the connector code by `npm run plugin:docs`. Do not edit by hand. -->

# Tools

The connector has 25 tools. An AI app sees only the ones its connection may use (`tools/list`), and Zuperbase checks every call again.

## Read only

Every connection has these, within the person's own access and the areas they allowed.

| Tool | What it does |
|---|---|
| `whoami_and_access` | **Who am I and what may this app do.** The organisation, the person this app acts for, the access level, the areas switched on, and whether the first-time setup window is open. Call this first, and use it to explain access to the person. |
| `get_setup_status` | **Set-up checklist.** The first-time set-up steps for these books and which are done. Use it to run the set-up interview one question at a time. |
| `get_report` | **Financial report.** Profit and loss for a period; the balance sheet, trial balance, receivables or payables ageing (who owes what, by how overdue) as at a date; or the books health check (what to fix before figures can be trusted). From the posted books; amounts are exact decimal strings in the base currency. <br>Inputs: `report`, `byDocument`, `from`, `to`, `asOf` |
| `list_accounts` | **Chart of accounts.** Every account with its code, name and type. Use the codes in draft_journal. <br>Inputs: `includeInactive` |
| `list_contacts` | **Customers or vendors.** Customers or vendors, optionally filtered by a search on name, email or tax ID. At most 100 per call. <br>Inputs: `kind`, `search`, `limit` |
| `find_transactions` | **Find posted entries.** Posted journal entries, newest first, filtered by dates, text in the description or reference, or an account code. Each entry lists its lines. At most 50 per call; use offset for more. <br>Inputs: `from`, `to`, `search`, `accountCode`, `limit`, `offset` |
| `list_tax_rates` | **Tax rates.** The active tax rates (GST, VAT or sales tax) with their ids, for draft_invoice, draft_bill and add_items. |
| `list_items` | **Goods and services.** The goods and services the business sells or buys, with price, tax rate and HSN/SAC code. At most 100 per call. <br>Inputs: `search`, `limit` |
| `list_unmatched_bank_lines` | **Bank lines to match.** Imported bank statement lines not yet matched or categorised, oldest first. Money in is positive, money out negative. At most 100 per call. <br>Inputs: `limit`, `offset` |
| `explain_account_balance` | **Explain an account balance.** An account's opening balance, every posting in the period and its closing balance (debit-positive: a negative balance is a credit). At most 200 postings are listed; the totals always cover the whole period. <br>Inputs: `accountCode`, `from`, `to` |
| `month_end_checklist` | **Month-end checklist.** Zuperbase's close checklist for a month: the automatic checks (periods locked, bank lines matched, returns, documents missing and the rest), each ok or warn with its detail, and the organisation's own month-end tasks with who marked them. Read only: a person marks tasks and locks the month in Zuperbase. <br>Inputs: `month` |
| `suggest_bank_matches` | **Suggested bank matches.** Open bank statement lines with what Zuperbase suggests for each: entries already in the books with the same amount to the paisa and a near date (journalLineIds for match_bank_line), or, when nothing matches, the organisation's bank rule or a bank charge / interest hint with the account to categorise to. Suggestions are Zuperbase's deterministic rule, not a decision; one suggestion with a document number or name in the bank text is the strongest. At most 50 lines per call. <br>Inputs: `bankAccount`, `limit` |

## Prepare drafts

At Prepare drafts and Bookkeeper. Nothing these save is posted.

| Tool | What it does |
|---|---|
| `save_contact` | **Add or update a customer or vendor.** Saves a customer or vendor master record (a draft-level change; nothing posts). Give contactId to update an existing one; fields left out are cleared, so send the full record when updating. <br>Inputs: `kind`, `contactId`, `name`, `email`, `phone`, `taxId`, `subdivision`, `billingAddress` |
| `draft_journal` | **Draft a journal.** Saves a manual journal as a DRAFT for a person to review and post in Zuperbase. It never posts. Lines use account codes from list_accounts; each line has exactly one of debit or credit as a decimal string, and the debits must equal the credits. Receivable and payable lines need a contactId. <br>Inputs: `entryDate`, `notes`, `reference`, `lines` |
| `draft_invoice` | **Draft a sales invoice.** Saves a sales invoice as a DRAFT for a person to review and approve in Zuperbase. It never approves or sends it. customerId from list_contacts; taxId from list_tax_rates; each line either names an itemId from list_items or gives an income accountCode. Quantity and rate are decimal strings. Zuperbase works out the tax. <br>Inputs: `customerId`, `invoiceDate`, `dueDate`, `placeOfSupply`, `taxInclusive`, `notes`, `lines` |
| `draft_bill` | **Draft a purchase bill.** Saves a vendor's bill as a DRAFT for a person to review and approve in Zuperbase. It never approves or pays it. vendorId from list_contacts; billNumber is the vendor's own invoice number; each line has an expense, asset or stock accountCode; taxId from list_tax_rates. India: set sourceOfSupply to the vendor's state code, reverseCharge when RCM applies, and itc 'blocked' for credit barred by section 17(5). <br>Inputs: `vendorId`, `billNumber`, `billDate`, `dueDate`, `sourceOfSupply`, `placeOfSupply`, `reverseCharge`, `taxInclusive`, `notes`, `documentId`, `lines` |
| `add_items` | **Add goods or services.** Adds up to 50 goods or services the business sells, each with a price, an income accountCode, a taxId from list_tax_rates and, in India, the HSN (goods) or SAC (services) code. Allowed at Prepare drafts, and in the first-time set-up window. <br>Inputs: `items` |
| `upload_document` | **Upload a document.** Keeps a vendor bill, receipt or statement the person gave you in Zuperbase's documents, so the entry has its source. PDF, JPEG, PNG, HEIC, Excel (.xlsx) or CSV, at most 10 MB, as base64. The same file uploaded twice is found, not stored again. Pass the documentId to draft_bill to attach it. Read the file yourself: Zuperbase does not read it for you here. <br>Inputs: `fileName`, `contentBase64`, `notes` |

## Bookkeeper

Only at Bookkeeper, chosen by an owner or admin, up to the connection's limit per document or bank line.

| Tool | What it does |
|---|---|
| `post_draft` | **Post a draft.** Bookkeeper level only: approves and posts a draft invoice, bill or journal to the books, up to this AI app's posting limit. Above the limit, or when the person's own approval limit or maker-checker needs someone else, it stays a draft and the answer says so. Check the draft with the person's instructions first; once posted, a correction is a new entry made by a person. <br>Inputs: `kind`, `id` |
| `match_bank_line` | **Match a bank line.** Bookkeeper level only: matches an open statement line to entries already in the books (journalLineIds from suggest_bank_matches). Zuperbase refuses unless the entries add up to the line's amount exactly. Above this AI app's posting limit the line stays open and the answer says so. <br>Inputs: `lineId`, `journalLineIds` |
| `categorise_bank_line` | **Categorise a bank line.** Bookkeeper level only: posts a new entry for an open statement line nothing in the books matches (a bank charge, interest, a small expense), against the account given by code. Use it only when suggest_bank_matches found no match, and the account is clear from a rule, a hint or the person. A charge that includes GST takes taxId (and interState for IGST). Above this AI app's posting limit the line stays open. <br>Inputs: `lineId`, `accountCode`, `contactId`, `memo`, `taxId`, `vendorId`, `interState` |

## First-time set-up

Only while the first-time set-up window is open: until the first entry is posted, and at most 7 days.

| Tool | What it does |
|---|---|
| `set_business_profile` | **Set the business profile.** First-time setup only: the address, phone, email, registered name, CIN and PAN printed on documents. Fields left out keep their current value. <br>Inputs: `address`, `phone`, `email`, `legalName`, `cin`, `pan` |
| `set_tax_registration` | **Set the tax registration.** First-time setup only: the business's tax registration (GSTIN in India; VAT number, TRN or EIN elsewhere) and its state or province code. Give an empty registration if the business is not registered. <br>Inputs: `taxRegistration`, `subdivision` |
| `add_bank_account` | **Add a bank or cash account.** First-time setup only: adds a bank or cash account. Never ask for the full account number: the last 4 digits are enough. <br>Inputs: `name`, `kind`, `bankName`, `accountLast4`, `ifsc` |
| `set_numbering` | **Set document numbering.** First-time setup only: how a kind of document is numbered, e.g. invoices as INV/{FY}/0001. Placeholders {FY}, {YYYY} and {YY} may be used in the prefix and suffix. India: an invoice number may have at most 16 characters (rule 46). <br>Inputs: `kind`, `prefix`, `suffix`, `padWidth`, `nextNumber`, `restartYearly`, `mode` |
