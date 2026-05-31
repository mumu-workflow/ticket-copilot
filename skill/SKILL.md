---
name: customer-support-reply-workflow
description: Design, document, review, or validate a customer support workflow that rewrites customer questions, parses attachments, requests missing information, prepares copyable replies, requires manual review, and records the confirmed version. Use when users need a reusable support ticket reply workflow, prompt structure, field schema, state machine, or sanitized public template. Never automate sending.
---

# Customer Support Reply Workflow

Use this Skill to design or review a customer support reply workflow with mandatory human review.

## Hard Rules

- Never send messages automatically.
- Require customer service staff to review every reply.
- Treat “confirm copy” as a copy-and-record action only.
- Keep external replies free of model reasoning.
- Store only knowledge matches, rule matches, and missing information in internal basis.
- Do not expose IDs, accounts, tokens, private addresses, customer data, or proprietary prompts.

## Fixed States

```text
待分析 / 待补充信息 / 待发送确认 / 已完成
```

## Fixed Attachment States

```text
无附件 / 解析成功 / 格式不支持 / 解析失败
```

## Workflow

1. Accept the customer description and optional attachments.
2. Rewrite the description only when necessary. Do not invent facts.
3. Parse attachments and set one fixed attachment state.
4. Wait until description rewrite and attachment parsing are both complete.
5. Determine whether required information is missing.
6. If information is missing, prepare a supplement request for manual review and copy.
7. If information is sufficient, prepare an external draft reply for manual review and copy.
8. Record the confirmed version, operator, time, and path-specific state.

## Path-Specific State Update

- Confirmed supplement request: set `待补充信息`.
- Confirmed formal reply: set `已完成`.

## References

- Read [field-schema.json](schemas/field-schema.json) when mapping fields.
- Read [state-schema.json](schemas/state-schema.json) when validating state transitions.
- Read [kb-schema.json](schemas/kb-schema.json) when adding a knowledge base.
- Read [description-rewrite.md](prompts/description-rewrite.md) for rewrite constraints.
- Read [attachment-parse.md](prompts/attachment-parse.md) for attachment parsing.
- Read [pre-reply-gate.md](prompts/pre-reply-gate.md) for missing-information and draft-reply structure.
- Read [final-reply-generate.md](prompts/final-reply-generate.md) for the confirmed reply structure.
- Read [attachment-support-policy.md](configs/attachment-support-policy.md) before making attachment capability claims.
- Read [model-capability-note.md](configs/model-capability-note.md) before describing model compatibility.
