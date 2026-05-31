# Changelog

## 1.0.0 - 2026-05-31

### Added

- Added an end-to-end customer question workflow: submit, normalize, parse attachments, generate a draft, review, confirm copy, manually send, and retain the confirmed version.
- Added minimal description rewriting that preserves links, paths, IDs, error codes, file names, and version numbers.
- Added four fixed attachment states: `无附件`, `解析成功`, `格式不支持`, and `解析失败`.
- Added a missing-information gate that generates either a supplement request or a copy-ready external draft reply.
- Added mandatory employee review and confirm-copy handling. AI never sends messages automatically.
- Added public field semantics, a fixed state machine, a trigger matrix, prompt structures, JSON Schemas, and sanitized validation examples.
- Added optional knowledge base and phrasebook examples. The MVP can run without a knowledge base.

### Rules

- Fixed workflow states: `待分析`, `待补充信息`, `待发送确认`, and `已完成`.
- Draft generation starts only after description normalization and attachment parsing are both complete.
- Internal decision basis is separated from external copy-ready replies.
- Unknown knowledge base requests do not receive unverified capability claims and must be reviewed by an employee.

### Boundaries

- No automatic outbound messaging.
- No internal automation IDs, field IDs, accounts, tokens, private addresses, real customer data, or proprietary prompts.
- No enterprise-scale permission system or high-concurrency architecture.
