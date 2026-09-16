# PortSwigger — SQL injection

## Lab 1 (Apprentice) — retrieve hidden data via WHERE clause — SOLVED
16 Sep 2026

Target built its query by pasting user input straight into the SQL string:
  WHERE category = 'Gifts' AND released = 1

- Sent `category=Gifts'` → Internal Server Error. The stray quote broke the
  query grammar = proof my input reaches the query as CODE, not data.
- Sent `category=Gifts'--` → the `'` closes the string, `--` comments out the
  rest (`AND released = 1`), so the released filter is ignored. Hidden products
  shown. Solved.

## Why this matters for AI security
SQL injection and prompt injection are the same disease: user input escaping
the data channel and being read as instructions. SQLi is SOLVED — parameterized
queries enforce code/data separation. There is NO equivalent for prompt
injection, which is why it stays #1 on the OWASP LLM list. Today I saw the
solved ancestor of the problem I'm specializing in.