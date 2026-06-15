# Agent-to-Terminal Execution Protocol — Draft Spec

---

## 1. Task Format

All tasks are defined as structured JSON:

```json
{
  "task": "string",
  "steps": [
    {
      "id": 1,
      "command": "string",
      "depends_on": []
    }
  ]
}
