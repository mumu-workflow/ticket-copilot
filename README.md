[English](README.md) | [简体中文](README.zh-CN.md)

# Ticket Copilot

**Turn vague customer questions into human-reviewed, copy-ready replies.**

Ticket Copilot is a lightweight, reusable workflow template for teams handling customer requests. It normalizes vague questions, parses optional attachments, identifies missing information, drafts reply suggestions, and records the final employee-confirmed version.

It is intentionally human-in-the-loop: AI prepares the draft, but employees always review, copy, and send the final message manually. It does not automate outbound messaging.

## Why Ticket Copilot?

Teams repeatedly spend time clarifying incomplete questions and rewriting similar answers. Ticket Copilot provides a practical MVP for:

- Standardizing vague customer questions without inventing facts
- Requesting the right missing information
- Producing copy-ready draft replies for human review
- Separating internal decision basis from customer-facing text
- Preserving the final confirmed reply for future reuse

Use it as a starting point for helpdesk workflows, customer request triage, internal knowledge base integration, standard phrasebooks, AI reply assistants, and human-in-the-loop automation.

## What You Get

| Capability | Included in v1.0.0 |
|---|---|
| Description normalization | Minimal rewrite while preserving links, IDs, paths, and error codes |
| Attachment parsing | Four fixed states: no attachment, parsed, unsupported format, failed |
| Missing-information gate | Distinguishes supplement requests from formal draft replies |
| Human review workflow | Employees review, revise, confirm copy, and send manually |
| Structured public template | Field schema, state machine, trigger matrix, prompt structures, and sanitized examples |
| Optional knowledge base | The MVP runs without one; sample entries are included for extension |

## Core Principles

1. AI draft replies are never sent automatically.
2. Every reply must be reviewed by an employee.
3. “Confirm copy” only copies and records the approved reply.
4. Employees manually paste and send messages through existing tools.
5. Customer-facing replies never include model reasoning.
6. Rules take priority over AI-generated text.

## Workflow

```mermaid
flowchart TB
    A["Customer question<br/>Text + optional attachment"] --> S0["待分析"]

    subgraph P1["1. AI-assisted intake · Standardize inputs"]
        S0 --> B["Normalize description<br/>Preserve facts and identifiers"]
        S0 --> C["Parse attachments<br/>无附件 · 解析成功 · 格式不支持 · 解析失败"]
        B --> D{"Description and attachment<br/>parsing both complete?"}
        C --> D
        D -->|No| W0["Wait for complete inputs<br/>Do not generate a draft"]
        W0 -.-> D
    end

    subgraph P2["2. Rules-first triage · Improve reply quality"]
        D -->|Yes| E{"Missing key information?"}
        E -->|Yes| F["Draft supplement request"]
        E -->|No| J["Match verified knowledge + phrasebook<br/>Optional enhancement"]
        J --> K["Generate copy-ready draft reply"]
    end

    subgraph P3["3. Employee review · Keep outbound communication controlled"]
        F --> R1["Employee reviews and confirms copy"]
        K --> S1["待发送确认"]
        S1 --> R2["Employee reviews, revises,<br/>and confirms copy"]
        R1 --> M1["Employee sends manually"]
        R2 --> M2["Employee sends manually"]
    end

    M1 --> S2["待补充信息<br/>Collect missing context"]
    S2 -. "Customer adds details" .-> S0
    M2 --> S3["已完成<br/>Retain employee-confirmed reply"]

    classDef state fill:#FFF7ED,stroke:#EA580C,color:#7C2D12,stroke-width:2px
    classDef ai fill:#EFF6FF,stroke:#2563EB,color:#1E3A8A
    classDef guard fill:#F5F3FF,stroke:#7C3AED,color:#4C1D95
    classDef human fill:#ECFDF5,stroke:#059669,color:#064E3B
    classDef outcome fill:#F0FDFA,stroke:#0F766E,color:#134E4A,stroke-width:2px

    class S0,S1,S2 state
    class B,C,F,J,K ai
    class D,E,W0 guard
    class R1,R2,M1,M2 human
    class S3 outcome
```

## Fixed States

```text
待分析 / 待补充信息 / 待发送确认 / 已完成
```

## Fixed Attachment States

```text
无附件 / 解析成功 / 格式不支持 / 解析失败
```

## Quick Start

1. Read the [project overview](docs/01-project-overview.md) and [workflow](docs/02-workflow.md).
2. Create the minimum fields defined in the [field specification](docs/04-field-spec.md).
3. Configure your workflow using the [trigger matrix](docs/05-trigger-matrix.md).
4. Adapt the public [prompt structures](docs/06-prompt-structure.md) to your model provider.
5. Validate your setup with the [sanitized demo cases](docs/09-demo-cases.md).
6. Use the reusable [Agent Skill](skill/SKILL.md) when asking an AI coding agent to design or review the workflow.

## Included Examples

| Example | Purpose |
|---|---|
| [Sufficient information](examples/cases/case-202605310014.md) | Generate a formal draft reply |
| [Missing information](examples/cases/case-202605310015.md) | Generate a supplement request |
| [Feature availability limitation](examples/cases/case-202605310013.md) | Avoid unverified capability claims |
| [Knowledge base minimum set](examples/kb/kb-minimum-10.json) | 10 sanitized knowledge entries |
| [Phrasebook minimum set](examples/phrasebook/phrasebook-minimum-6.json) | 6 reusable customer-facing phrases |
| [No-hit acceptance cases](examples/validation/no-kb-hit-acceptance-3.json) | 3 tests for unknown requests |

## Repository Layout

```text
docs/       Workflow documentation and public specifications
examples/   Sanitized cases, knowledge entries, and acceptance examples
skill/      Reusable Agent Skill, public prompt structures, and JSON Schemas
```

## Use Cases

- Customer request triage
- Helpdesk reply standardization
- AI-assisted reply drafting
- Missing-information collection
- Knowledge base and phrasebook extension
- Human-in-the-loop workflow design

## Safety Boundary

This public repository does **not** include:

- Automatic message sending
- Internal automation IDs or field IDs
- Accounts, tokens, keys, or private network addresses
- Real customer data or attachments
- Proprietary internal prompts

Read the full [release boundary](docs/10-release-boundary.md).

## Roadmap

### v1.0.0: MVP

- Description normalization
- Attachment parsing state model
- Missing-information gate
- Copy-ready draft replies
- Mandatory human review and confirm-copy workflow
- Structured fields, prompts, schemas, and sanitized validation examples

### v1.1.0: Knowledge Base Enhancement

- Internal knowledge base integration
- Standard phrasebook integration
- Knowledge match records
- Tutorial references
- Confirmed-answer retention rules

## Search Keywords

`ticket copilot` · `customer request triage` · `helpdesk workflow` · `AI reply assistant` · `human-in-the-loop` · `knowledge base` · `prompt engineering` · `workflow automation`

## License

[MIT](LICENSE)
