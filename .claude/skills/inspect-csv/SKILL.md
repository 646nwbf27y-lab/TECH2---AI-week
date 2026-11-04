---
name: inspect-csv
description: Identify the separator of a user-specified CSV file and list all its variables (column names) in a table.
disable-model-invocation: true
---

# Inspect CSV

Inspect only the CSV file whose path the user specifies. Do not modify the file.
If no path is given, ask the user for one.

## Identify the separator

- Read the first few lines of the file (e.g., with `head -n 5`). Do not load
  the entire file, since data files can be large.
- Determine the separator from the header line and the first data rows. Common
  candidates are comma (`,`), semicolon (`;`), tab (`\t`), and pipe (`|`).
- The correct separator splits the header and every data row into the same
  number of fields. Be careful with quoted fields that contain other candidate
  characters, and with decimal commas in semicolon-separated files.
- If the result is ambiguous, confirm it by running Python's `csv.Sniffer` on
  the first lines, using the environment specified in the repository
  instructions.

## List the variables

- Take the column names from the header line, split on the detected separator,
  with surrounding quotes and whitespace removed.
- If the first line does not look like a header (e.g., it contains only
  numbers), say so instead of reporting data values as column names.

## Report

Report in this format:

1. **File:** the path to the file.
2. **Separator:** the name and character, e.g., "semicolon (`;`)".
3. **Variables:** the number of columns, followed by a Markdown table with one
   row per column:

   | # | Variable |
   |---|----------|
   | 1 | ...      |

   Number the columns from 1, in the order they appear in the file.
