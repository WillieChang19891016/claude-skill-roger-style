# roger-style

讓 Claude 用台灣 Twitch 實況主羅傑（[roger9527](https://www.twitch.tv/roger9527)）
的口氣回話。靈感來自 [stop-slop](https://github.com/hardikpandya/stop-slop)，
但方向相反——這個 skill 是 **加風格**，不是消風格。

## 用法

skill 已經放在 `~/.claude/skills/roger-style/`，Claude Code 啟動時會自動掃到。

### 一次性觸發

擇一：

1. **顯式呼叫**：直接打 `/roger-style`，後面接你的問題
2. **隱式觸發**：訊息中包含「羅傑風」「用羅傑的口氣」「Roger 風格」等字樣

### Session 內持續開關（toggle）

需要先安裝 `commands/` 內的兩個 slash command（見下方〔安裝 toggle commands〕段）。

- `/roger-on` — 開啟，本 session 所有後續回答都用羅傑風
- `/roger-off` — 關閉，回到一般風格

⚠️ **限制**：toggle 是「session 內持久」不是「跨 session 持久」。新開對話要重打 `/roger-on`。
跨 session 持久需要用 settings.json hook，本 skill 目前不提供（之後可擴充）。

## 範圍

**會做**：
- 在回答的開頭、結尾、轉折、強調位置塞入口頭禪（確實、全對、真假、亂講、冷靜、
  弟弟、大中計 等，完整清單見下方「語料一覽」）
- 偶爾用整句名言收束（感謝訂閱、同行非敵國 船大不爭海 等）
- 保留所有技術內容的正確性（code、SQL、API 名、數字一字不改）

**不會做**：
- 全篇 cosplay 改寫
- 動到 code block 內容

## 語料一覽

### 短口頭禪（11 個）

| 分類 | 口頭禪 |
|---|---|
| 同意 / 證實 | 確實、全對、有料 |
| 質疑 / 驚訝 | 真假 |
| 否定對方 | 亂講 |
| 安撫情緒 | 冷靜、心態不能崩 |
| 踩雷 / 吐槽 | 大中計、超級可悲、神經病是不是 |
| 開場 / 轉折 | 來 |
| 稱呼使用者 | 弟弟 |

### 整句名言（7 句）

- 感謝訂閱
- 來 我們來聊乾淨
- 我這個人不說謊 都是身不由己
- 我知道聊天室都是愛之深責之切
- 同行非敵國 船大不爭海
- 我用思念來代替
- 就說沒有要抽狗狗肉

每個語料的使用情境、強度、注入時機詳見 [`references/phrases.md`](references/phrases.md) 與 [`references/quotes.md`](references/quotes.md)。

## 檔案結構

```
roger-style/
├── SKILL.md              # 主規則、四條核心原則、工作流程
├── references/
│   ├── phrases.md        # 短口頭禪清單（A~F 區，分情境）
│   ├── quotes.md         # 整句名言（依情境分 A 結尾 / B 自嘲）
│   └── examples.md       # 改寫前後對照 + 反例
├── commands/
│   ├── roger-on.md       # /roger-on toggle command
│   └── roger-off.md      # /roger-off toggle command
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

## 擴充語料

如果之後想加新名言：

- 短口頭禪 → 編 `references/phrases.md`，依情境塞進 A~F 表
- 整句名言 → 編 `references/quotes.md`，依情境分 A（結尾）/ B（自嘲）區
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

### 安裝 toggle commands（可選）

如果要用 `/roger-on` / `/roger-off` 開關，把 repo 內 `commands/` 的兩個檔複製到使用者層級的 commands 目錄：

**macOS / Linux**

```bash
cp ~/.claude/skills/roger-style/commands/*.md ~/.claude/commands/
```

**Windows (PowerShell)**

```powershell
Copy-Item "$env:USERPROFILE\.claude\skills\roger-style\commands\*.md" `
  "$env:USERPROFILE\.claude\commands\"
```

裝完重啟 Claude Code，就能用 `/roger-on` 跟 `/roger-off`。

## License

MIT — 詳見 [LICENSE](LICENSE)。歡迎 fork、改、加自己喜歡的實況主梗。
