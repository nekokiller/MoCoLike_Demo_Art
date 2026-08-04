# Git 規範

> 本 repo 僅用於管理美術資源，因此採用簡單、容易執行的 Git 流程；不套用軟體開發專案的完整規範。

---

## 1. Commit 權限

- AI 可以檢查狀態、查看差異、建立或修改檔案，以及執行 `git add`。
- AI 只有在**回報變更內容並取得使用者確認後**，才可執行 `git commit`。
- AI 不得自行執行 `git merge` 或 `git push`；需要時必須先取得使用者明確授權。

## 2. Commit 時機

- 以「一組完整、相關的美術資源變更」為一次 commit。
- 新增、替換或刪除資源時，完成一個可辨識的變更批次後再提交，不需要每個檔案各自 commit。
- 文件或 Git 設定變更，與美術資源分開提交。

## 3. Commit Message

使用簡短的繁體中文即可，格式如下：

```text
<類型>: <變更說明>
```

常用類型：

| 類型 | 用途 |
| --- | --- |
| `asset` | 新增、替換或整理美術資源 |
| `docs` | 修改說明文件 |
| `chore` | 修改 Git 設定或其他雜務 |
| `fix` | 修正資源問題 |

範例：

```text
asset: 新增角色待機動畫
asset: 替換主選單背景圖
asset: 整理第一批怪物素材
fix: 修正圖示檔名
docs: 更新資源說明
```

- 不要求 Conventional Commits 的 `scope`。
- 不要求在主旨加入作者名稱。

## 4. Commit Message 署名

每則 commit message 必須在結尾加入 `Co-Authored-By`，並與正文空一行：

```text
Co-Authored-By: <當前 session 模型顯示名> <供應商 noreply email>
```

- `<當前 session 模型顯示名>` 必須填寫本次實際使用的模型名稱，不可直接照抄範例。
- email 必須使用對應供應商的 noreply email，例如 Codex 使用 `noreply@openai.com`。
- 不確定模型名稱或 email 時，先向使用者確認。

## 5. Branch

- 小幅、直接的資源更新可直接在目前分支完成。
- 大批資源或尚未完成的工作，可使用工作分支；完成後再由使用者決定是否合併。
- 不要求固定的分支命名格式，但名稱應能看懂用途，例如 `art/menu-background`。

## 6. Push 與檢查

- `git push` 由使用者自行執行，或由使用者明確授權 AI 後執行。
- Commit 前至少確認：
  1. 變更的檔案正確。
  2. 沒有誤加入暫存檔、個人檔案或不必要的大型檔案。
  3. 資源檔名與資料夾位置符合專案慣例。
- 不任意改寫已公開的 commit 歷史；若需 `reset`、`rebase` 或強制 push，必須先確認。


