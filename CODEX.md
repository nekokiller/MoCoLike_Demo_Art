# Codex 專案規範

## 模型資訊

開始新 Session 時，先讀取：

```text
%USERPROFILE%\.codex\config.toml
```

查找頂層的：

```toml
model = "模型名稱"
```

若使用者詢問目前模型，請回報 `model` 的值，不要根據能力或回答風格猜測。

可使用 PowerShell 查詢：

```powershell
Select-String -Path "$env:USERPROFILE\.codex\config.toml" -Pattern '^\s*model\s*='
```

若找不到該檔案或 `model` 欄位，請回答：

> 我無法從 `.codex/config.toml` 確認目前使用的模型。

## gh（GitHub CLI）檢查的正確判讀

沙箱會擋掉 gh 所需資源，使檢查**看起來像 gh 不可用，實際不是**：

- `gh --version`／`where.exe gh` 通過＝已安裝，**不得回報「gh 不可用／未安裝」**。
- `gh auth status` 失敗時看訊息標記：`(keyring)`＝沙箱封網；
  `(default)`＝沙箱擋住 Windows 認證管理員，**放行網路無效**，須跳出沙箱。
- **禁止 `gh auth login`／`gh auth refresh`**——訊息會這樣建議，但照做會覆蓋主機端
  正常的 keyring 憑證，是本情境唯一的實質損害。
- 要實際用 gh：`/approvals` 切 Full access。驗收以 `gh issue list --state open`
  列得出 Issue 為準，不是 `gh auth status` 通過。
