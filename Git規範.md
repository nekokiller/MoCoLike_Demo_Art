# Git 規範

> 本文件只規範 commit 訊息與提交自檢。

---

## Commit Message 格式

```text
<type>(scope): <繁中說明>
```

| type | 用途 |
| --- | --- |
| `asset` | 新增、替換、更新、移除或整理美術資產 |
| `fix` | 修正資產內容、檔名、路徑或匯入設定等問題 |
| `docs` | 純文件變更 |
| `chore` | Git 設定、資料夾結構或其他不屬於資產內容的雜務 |

- **scope** 為選填；使用 `asset` 時，建議以 scope 標示資產種類，例如 `model`、`texture`、`material`、`animation`、`vfx`、`ui`、`character` 或 `environment`。
- 範例：`asset(model): 新增冒險者角色模型`、`asset(texture): 更新森林地表貼圖`、`fix(animation): 修正角色待機動畫`。
- 同一批次若包含多種密切相關的資產，可省略 scope，例如 `asset: 新增森林場景資產`。
- 主旨與正文說明一律使用繁體中文；主旨應聚焦變更目的，正文補充範圍、原因與檢查結果即可。

## 共同作者署名（每則必填）

每則 commit message 的結尾必須與正文空一行，再附上當次 session 實際模型的 trailer；`<email>` 不可省略：

```text
Co-Authored-By: <當前 session 模型顯示名> <供應商 noreply email>
```

不要照抄範例模型名稱；email 依供應商（如 Codex 用 `<noreply@openai.com>`）；不確定目前模型顯示名或 email 時，先詢問使用者。工具自動附加、但與當次實際模型不符的署名，不得保留。

## 提交與自檢方式

1. **多行 message 一律使用暫存檔搭配 `git commit -F <路徑>`**；避免 PowerShell here-string 與 Bash heredoc 混用而在 message 首尾留下 `@`。
2. 單行 message 可用 `git commit -m "..."`；若直接輸入多行訊息，shell 與語法必須一致。
3. commit 後執行：
   ```bash
   git log -1 --format=%B
   ```
   確認開頭／結尾無多餘字元、最後一行有正確 `Co-Authored-By`（含 email）。若遺漏，未 push 前以 `git commit --amend` 補正；已 push 時不得自行改寫遠端歷史，須先取得使用者明確授權。

## Push

commit 後應主動詢問使用者是否授權 `git push`；未獲明確授權不得推送。
