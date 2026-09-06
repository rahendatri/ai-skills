# Explanation

## Input

A file containing interview transcripts (e.g. excel, text file, etc.).
Each file must contain:
- only one interview transcript if it is a text file
- or one transcript per line if it is in table format.

# Output

- A markdown table
- An actionable recommendation with execution steps

## How it works

This skill analyzes user interviews in the following steps:

1. Classify verbatims into "clear" and "messy guess" categories
2. Rank by frequency (according to distinct interviewee count) the concerned themes
3. Identify the most frequent + painful theme with supporting quotes
4. Provide actionable recommendation with scoped execution steps

