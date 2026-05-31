# Attachment Parse Prompt Structure

## Goal

Extract evidence from an optional attachment without inventing content.

## Output

```json
{
  "status": "无附件 | 解析成功 | 格式不支持 | 解析失败",
  "summary": "",
  "structured_result": {},
  "error": ""
}
```

## Constraints

- Use `无附件` when no attachment exists.
- Use `格式不支持` when a supplied format cannot be parsed.
- Use `解析失败` when a supported format fails during parsing.
- Do not infer unreadable content.
