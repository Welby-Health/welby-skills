---
name: validate
description: Answer a question or check a claim using only real evidence, with a source for every number. Use when the user types /validate, or asks to "validate this number", "is this number right", "double-check this", "prove it", "where did this come from", or "show your sources". Works on files, spreadsheets, Google Sheets, databases, connectors, email, Slack and documents.
argument-hint: <question or claim to check>
---

# Validate

The user wants an answer they can trust and show to others: $ARGUMENTS

Think of a board deck where every number has a footnote saying where it came from. Hold every answer to that standard.

## Rules

1. **Evidence only.** Every number and every claim in your answer needs a source you actually opened or ran in this session. Memory, earlier chat, "common knowledge" and estimates are not sources.
2. **Never guess or fill gaps.** If you can't prove something, mark it **Not verified**. Say what is missing and where it would come from (which file, system, report or person). Never round, extrapolate, or assume a missing month, row or field.
3. **Let code do the math.** Compute every sum, count, average or percent with code, a query, or a spreadsheet formula. Never add numbers in your head. Keep the code or query so you can cite it.
4. **Check twice.** Before you reply, re-read each source or re-run each query a second time and compare the results.
   - Same result: say "re-checked, matches".
   - Different result: say "the number changed between reads", show both values, and don't pick one silently.
5. **Note when you read it.** Data changes day to day. Record the date and time you read each source, and the file's last-modified time when you can see it.
6. **Answer only what was asked.** If the data covers a different period, scope or definition than the question, say so plainly instead of stretching it.

## What a good source looks like

| Kind of source | Cite it as |
|---|---|
| File or spreadsheet | file name, tab, cell or row range (e.g. `invoices.xlsx`, tab `Oct`, rows 2 to 41, column D) |
| Google Sheet | sheet name + link, tab, range |
| Database or connector | the exact query or call you ran, and how many rows came back |
| Email or Slack | permalink, sender, date |
| Document or PDF | document name, page or section |
| Calculation | the code or formula used, and the inputs it used |

A source the user can't open or re-run doesn't count. If a tool gives you no link or location, say that in the source line.

## Steps

1. Restate the question in one line. List each number or claim you need to prove.
2. Find the sources. Look in the working folder and any connected tools. If nothing relevant exists, stop looking and mark it **Not verified**.
3. Pull the data and compute with code. Watch for duplicates, blanks, refunds or credits, mixed date formats and the wrong period. Mention any you find.
4. Re-check: run it again and compare (rule 4).
5. Write the reply with the template below.

## Reply template

Use plain language for a finance reader. No jargon, no unexplained abbreviations. Keep it short.

```
**Answer:** <1 to 3 lines. The answer first, each number tagged with its source number like [1].>

**Sources**
1. <what it proves>: <where: file/tab/range, or query + row count, or link>. Read <date time>. Re-checked, matches.
2. ...

**Not verified**
- <claim>: <what is missing> <where it would come from>.
```

Leave out "Not verified" if everything is proven. If nothing could be proven, say so in the answer line and don't give a number.

## Example

Request: `/validate what was total revenue for October, and did we beat $50k?`

```
**Answer:** October revenue was $48,210.00 [1]. That is $1,790.00 short of $50,000 [2].

**Sources**
1. October revenue: invoices.csv, rows 2 to 41 (40 invoices dated Oct 1 to Oct 31), column "amount", summed with Python. Read Nov 5, 10:42 AM. Re-checked, matches.
2. Gap to $50,000: 50,000.00 minus 48,210.00, computed in Python.

**Not verified**
- Whether $50k was the official target: no budget or target file found. It would come from the budget sheet or whoever owns the plan.
```
