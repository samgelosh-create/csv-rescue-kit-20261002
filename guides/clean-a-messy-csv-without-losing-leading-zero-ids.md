# Clean a messy CSV without losing leading-zero IDs

CSV Rescue Kit — AI-created guide

A tidy CSV is useful only if it still means what the original meant. An identifier such as 00123 is a label, even when it looks like a number. Start with a reversible cleanup, then check how the destination application interprets the result.

### Keep the original and read the structure

Save an untouched copy and give the cleaned export a new filename. Confirm that the source is UTF-8 and choose its actual delimiter: comma, semicolon or tab. Preview the headings and several records before changing anything.

Use a CSV parser that understands quoting. A comma inside a quoted company name belongs to that cell; a quoted line break can belong to the same record. Splitting text at every comma or newline can turn valid data into extra columns or rows. Investigate parsing errors and uneven row widths instead of silently discarding them.

### Choose changes that preserve meaning

Trim surrounding whitespace only when those spaces are accidental. Spaces may be meaningful in codes or other text, including at the edges of quoted cells. Trimming every cell can also change headings, so inspect them too.

Remove rows only when every cell is empty after the chosen trimming. A record with an ID and an empty amount is not an all-empty row. Review exact whole-row duplicates after trimming: every cell, its position and the row width must match. This does not merge records by ID or choose between conflicting amounts. Identical rows may represent separate events; keep them when that is their meaning.

### Work through a small example

This input is entirely synthetic. It has four data rows, excluding the header:

```csv
id,company,amount
00123, Acme ,42
00123,Acme,42
00007,North Shop,-17
,,
```

With trimming, all-empty-row removal and exact whole-row deduplication enabled, the cleaned data is:

```csv
id,company,amount
00123,Acme,42
00007,North Shop,-17
```

Four data rows become two: one company cell was trimmed, one repeated row was removed and one all-empty row was removed. The two identifiers remain strings. Keep the original alongside this result so you can revisit those choices.

### Import identifiers deliberately

CSV text does not declare column types. The characters 00123 can survive cleanup and still become 123 when a spreadsheet guesses that the column contains numbers. Use the spreadsheet's import workflow and set identifier columns to Text before loading them. Check both sample IDs after import; direct opening may apply different defaults.

Choose exports deliberately too. Spreadsheet-safe CSV prefixes formula-prone values with an apostrophe. That changes the exported text: the negative value -17 becomes '-17. Review the result in your target application rather than assuming the prefix guarantees its behavior. The JSON export keeps cell values as strings, including "00123" and "-17"; missing cells become null rather than invented values.

Before replacing any working file, compare input and kept-row counts, removed empty rows, duplicates, trimmed cells and uneven rows. Inspect important identifiers, amounts and multiline cells. Save the cleanup report with the new export.

### Try the workflow

The account-free [CSV Rescue Kit demo](https://csv-rescue-kit-20261002.samgelosh.chatgpt.site/demo) accepts up to 100 data rows per import and UTF-8 input up to 5 MiB. CSV processing runs locally in the browser. The tool does not use AI at runtime; this guide was AI-created.

The optional [offline HTML/ZIP kit](https://csv-rescue-kit-20261002.samgelosh.chatgpt.site) costs $19 USD once. Its perpetual license permits personal and internal commercial use by a team, including employees and contractors; redistribution is not allowed.
