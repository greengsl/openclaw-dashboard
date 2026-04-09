# Personal Dashboard Template

純前端視覺化看板，JSON 為唯一資料介面。

## 快速開始

1. Fork 此 repo
2. 修改 `data/` 下的 JSON 檔案（格式見下方）
3. 部署到 Cloudflare Pages（接入 GitHub repo，branch = main）
4. 完成

## JSON Schema

### `data/projects.json`
```json
{
  "projects": [
    {
      "id": "唯一 ID",
      "title": "專案名稱",
      "description": "描述",
      "status": "active | planning | completed",
      "progress": 0-100,
      "tags": ["tag1", "tag2"],
      "lastUpdated": "YYYY-MM-DD",
      "completed": ["已完成項目"],
      "pending": ["待完成項目"]
    }
  ]
}
```

### `data/files.json`
```json
{
  "files": [
    {
      "id": "唯一 ID",
      "title": "檔案名稱",
      "description": "說明",
      "path": "路徑或連結",
      "tags": ["tag1"],
      "lastUpdated": "YYYY-MM-DD",
      "count": "數量或大小"
    }
  ]
}
```

### `data/memory.json`
```json
{
  "memory": [
    {
      "id": "唯一 ID",
      "title": "標題",
      "summary": "摘要",
      "tags": ["tag1"],
      "date": "YYYY-MM-DD"
    }
  ]
}
```

### `data/research.json`
```json
{
  "research": [
    {
      "id": "唯一 ID",
      "topic": "研究主題",
      "status": "completed | ongoing | planning",
      "summary": "結論摘要",
      "tags": ["tag1"],
      "date": "YYYY-MM-DD",
      "links": ["相關連結"]
    }
  ]
}
```

### `data/jobs.json`
```json
{
  "jobs": [
    {
      "id": "唯一 ID",
      "name": "作業名稱",
      "type": "cron | heartbeat | launchctl",
      "description": "說明",
      "schedule": "排程描述",
      "nextRun": "下次執行時間",
      "lastRun": "上次執行時間",
      "lastStatus": "ok | error | running",
      "lastResult": "執行結果描述"
    }
  ]
}
```

### `data/data.json` (整合總覽)

整合所有資料的單一檔案，適合一次性載入所有資訊，減少 HTTP 請求。

```json
{
  "meta": {
    "generated": "2026-04-09T07:56:00.000Z",
    "workspace": "/path/to/workspace"
  },
  "projects": [
    {
      "id": "唯一 ID",
      "title": "專案名稱",
      "status": "active | planning | completed",
      "progress": 0-100,
      "description": "描述",
      "tags": ["tag1", "tag2"],
      "lastUpdated": "YYYY-MM-DD",
      "completed": ["已完成項目"],
      "pending": ["待完成項目"]
    }
  ],
  "memory": [
    {
      "id": "唯一 ID",
      "title": "標題",
      "description": "詳細描述",
      "tags": ["tag1"],
      "date": "YYYY-MM-DD"
    }
  ],
  "jobs": {
    "items": [
      {
        "id": "唯一 ID",
        "name": "作業名稱",
        "type": "cron | heartbeat | launchctl",
        "description": "說明",
        "schedule": "排程描述",
        "nextRun": "下次執行時間",
        "lastRun": "上次執行時間",
        "lastStatus": "ok | error | running",
        "lastResult": "執行結果描述"
      }
    ],
    "heartbeat": null,
    "cron": {
      "items": [],
      "history": []
    },
    "launchctl": {
      "items": [],
      "history": []
    }
  }
}
```

**注意**：`data.json` 包含 `projects`, `memory`, `jobs` 三大區塊的完整資料，適合前端一次性載入。分類檔案（如 `projects.json`）仍可保留，供細部查詢使用。

## 部署

```bash
# Cloudflare Pages
npx wrangler pages deploy . --project-name=your-dashboard
```

或直接在 Cloudflare Dashboard 接入 GitHub repo，設定 branch = main。
