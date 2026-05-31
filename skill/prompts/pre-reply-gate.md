# Pre-reply Gate Prompt Structure

## Goal

Determine whether more information is needed and prepare copyable customer-facing text.

## Input

- Normalized description
- Attachment parse result
- Optional validated knowledge candidates

## Output

```json
{
  "need_more_information": true,
  "missing_information": [],
  "internal_basis": {
    "knowledge_match": "",
    "rule_match": "",
    "missing_information": []
  },
  "supplement_request": "",
  "external_draft_reply": ""
}
```

## Constraints

- Keep `internal_basis` limited to knowledge matches, rule matches, and missing information.
- Do not include model reasoning in `external_draft_reply`.
- If validated knowledge is not found, tell staff to make a manual judgment before sending.
- Do not make unverified capability claims.
