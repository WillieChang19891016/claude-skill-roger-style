# roger-style

讓 Claude 用台灣 Twitch 實況主羅傑（[roger9527](https://www.twitch.tv/roger9527)）
的口氣回話。靈感來自 [stop-slop](https://github.com/hardikpandya/stop-slop)，
但方向相反——這個 skill 是 **加風格**，不是消風格。

## 用法

skill 已經放在 `~/.claude/skills/roger-style/`，Claude Code 啟動時會自動掃到。

觸發方式擇一：

1. **顯式呼叫**：直接打 `/roger-style`，後面接你的問題
2. **隱式觸發**：訊息中包含「羅傑風」「用羅傑的口氣」「Roger 風格」等字樣
3. **session 內固定**：開頭跟 Claude 說「這整個 session 都用 roger-style 回我」

## 範圍

**會做**：
- 在回答的開頭、結尾、轉折、強調位置塞入口頭禪（確實、全對、真假、亂講、冷靜、
  弟弟、O-O OK 等）
- 偶爾用整句名言收束（感謝訂閱、來 我們來聊乾淨、同行非敵國 船大不爭海 等）
- 保留所有技術內容的正確性（code、SQL、API 名、數字一字不改）

**不會做**：
- 全篇 cosplay 改寫
- 動到 code block 內容
- 預設使用涉及私人事件的進階梗（紹安、狗狗肉、包莖等）

## 進階模式（hardcore）

預設關閉的 C 區個人化名言，可用以下方式臨時開啟：

- 訊息中包含「hardcore」「硬核」「全力放飛」
- 或直接說「給我硬核版的回答」

## 檔案結構

```
roger-style/
├── SKILL.md              # 主規則、五條核心原則、工作流程
├── references/
│   ├── phrases.md        # 短口頭禪清單（A~F 區，分情境）
│   ├── quotes.md         # 整句名言（A/B 預設啟用、C 為 hardcore）
│   └── examples.md       # 改寫前後對照 + 反例
└── README.md             # 本檔
```

## 驗證

裝好後試這 5 題確認 skill 行為：

1. 「為什麼 React `useEffect` 第二個參數空陣列會只跑一次？」
   → 技術內容正確、code 沒動，只在敘事段加風格
2. 「`async/await` 是不是比 `.then()` 容易讀？」
   → 應該以「確實 / 全對」開頭
3. 「我這段 code 改了三小時還是壞的」
   → 應該出現「冷靜」或「心態不能崩」
4. 連問 5 個雜題
   → 每則口頭禪數量落在 1~3 個之間
5. 預設情境不出現紹安 / 狗狗肉 / 包莖 / 周敦頤

## 擴充語料

如果之後想加新名言：

- 短口頭禪 → 編 `references/phrases.md`，依情境塞進 A~F 表
- 整句名言 → 編 `references/quotes.md`，注意 A/B（預設啟用）與 C（hardcore）分區
- 改寫範例 → 編 `references/examples.md`

擴充後不用重啟 Claude Code，下次觸發 skill 時會直接用新內容。

## 語料來源

初版語料整理自：
- [PTT Hearthstone 看板 羅杰語錄](https://www.ptt.cc/bbs/Hearthstone/M.1506460201.A.49B.html)
- [Disp BBS - 羅傑經典名言討論](https://disp.cc/b/ACG/ewM8)
- [4Gamers - 羅杰 Roger 專訪](https://www.4gamers.com.tw/news/detail/31378/9-things-of-joeman-roger)
- 使用者補充：「全對」「弟弟」

## 安裝

把 repo clone 到 Claude Code 的 skills 目錄即可。

**macOS / Linux**

```bash
git clone https://github.com/WillieChang19891016/claude-skill-roger-style.git \
  ~/.claude/skills/roger-style
```

**Windows (PowerShell)**

```powershell
git clone https://github.com/WillieChang19891016/claude-skill-roger-style.git `
  "$env:USERPROFILE\.claude\skills\roger-style"
```

或直接 [下載 zip](https://github.com/WillieChang19891016/claude-skill-roger-style/archive/refs/heads/main.zip)，解壓後把 `claude-skill-roger-style-main` 整個資料夾改名成 `roger-style`，丟到：

- macOS / Linux：`~/.claude/skills/`
- Windows：`%USERPROFILE%\.claude\skills\`

裝好後 Claude Code 重啟一次就能看到 `roger-style` 出現在 skill 列表，用 `/roger-style` 觸發。

## License

MIT — 詳見 [LICENSE](LICENSE)。歡迎 fork、改、加自己喜歡的實況主梗。
