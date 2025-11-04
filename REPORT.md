# O 級報告輔助說明（摘要）

此檔為 O 級交付的說明檔，建議另存為 PDF（6-10 頁）並附上截圖。

## Workflow (`.github/workflows/activity-log.yml`) 逐行註解重點
- `workflow_dispatch`：允許手動觸發。
- `schedule: - cron: '0 */6 * * *'`：每 6 小時執行一次（UTC）。選擇理由：在示範時能在合理時間看到更新，但不會過度消耗 Actions 次數；若你要更即時可縮短間隔，但需注意資源限制。
- `push` -> `branches: main`：每次 push 到 main 也會觸發，方便開發測試。
- 使用 TheDanniCraft/activity-log action，並客製化：
  - `GITHUB_TOKEN: ${{ secrets.TOKEN }}`：此處應放置你在 GitHub 設定的 Personal Access Token（PAT），權限至少需有 `public_repo`（public repo）或 `repo`（private repo），以便 action 可以 commit 回 repo。
  - `USER_ID: ${{ github.repository_owner }}`：使用 repo 所有者帳號作為欲抓取活動的使用者。
  - `TYPES: 'PushEvent'`：只顯示 Push 事件，方便聚焦 code activity（示範客製化）。
  - `MAX_LINES: 3`：限制輸出為 3 筆（O 級說明你為何選 3）。
  - `COMMIT_MESSAGE`：自訂 bot 的 commit 訊息，讓 commit 歷史更清楚。

## Cron 說明（在報告中擴充）
- 範例 `0 */6 * * *`：含義為 "每 6 小時的第 0 分鐘"（例如 00:00、06:00、12:00、18:00，UTC 時區）。
- 為何選 6 小時：在課堂演示與驗證時頻率適中，能在短時間內觀察到更新；若選太頻繁，會浪費 Actions 配額；若選太稀少，更新會顯得不及時。

## Deliverables Checklist
- [ ] `index.md`（使用 `{% include_relative README.md %}`）
- [ ] `README.md` 含活動 placeholder
- [ ] `.github/workflows/activity-log.yml`（含 schedule 與客製化參數）
- [ ] Pages 已啟用並能看到 README 內容
- [ ] Action 成功執行並產生 bot commit（擷取 commit link 與 Actions log 截圖）

## 建議截圖清單
1. Actions 執行成功的畫面（包含 run id）
2. Commit 歷史中 bot commit 的那一筆（含 commit 訊息）
3. Pages 網頁顯示 README（帶活動清單）

---
請在最終報告中貼上 `activity-log.yml` 的完整內容並逐行註解（可直接使用本檔作為起點）。
