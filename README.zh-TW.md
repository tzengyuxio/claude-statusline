# Claude Code Status Line

給 [Claude Code](https://docs.anthropic.com/en/docs/claude-code) 用的雙行狀態列。只顯示有用的，其餘省略。

[English](README.md)

![screenshot](screenshot.png)

## 安裝

```sh
curl -fsSL https://raw.githubusercontent.com/tzengyuxio/claude-statusline/main/install.sh | bash
```

重啟 Claude Code 即可。需要 **bash** 4.0+、**jq**、**git**，以及 [Nerd Font](https://www.nerdfonts.com/) 字型。

<details>
<summary>手動安裝</summary>

**1. 下載腳本：**

```sh
curl -o ~/.claude/statusline-command.sh \
  https://raw.githubusercontent.com/tzengyuxio/claude-statusline/main/statusline-command.sh
chmod +x ~/.claude/statusline-command.sh
```

**2. 加入 `~/.claude/settings.json`：**

```json
{
  "statusLine": {
    "type": "command",
    "command": "~/.claude/statusline-command.sh",
    "padding": 1
  }
}
```

**3. 重啟 Claude Code。**

</details>

## 顯示內容

### 第一行 — AI 狀態與用量

```
Model │ Context Bar 28% │ $0.42 │ 5h 45% ↺ 4h27m │ 7d 12% ↺ 5d2h
```

模型名稱、Context 使用進度條（16 格）、本次費用、5 小時 / 7 天 API 配額與重置倒數。Context 用量超過 90% 時會出現紅底警示。

### 第二行 — 工作環境

```
my-project │ main +2 ~1 ?3 │ .venv (3.12) │ NORMAL
```

目錄名稱、Git 分支 + 檔案狀態數、Python 虛擬環境（偵測到時顯示）、Vim 模式（啟用時顯示）。

所有百分比採交通燈配色：綠色（0–49%）、黃色（50–79%）、紅色（80%+）。

## 設計理念

- **實用優先** — 不影響下一步操作的資訊，就不該出現在狀態列上
- **安靜克制** — 可選區段（venv、vim mode）只在相關時才顯示
- **一眼可讀** — 兩行、色彩編碼、不需要閱讀
- **高效渲染** — 單次 `jq` 解析、單次 `git status`、背景快取 API 呼叫，約 30ms 完成

## 自訂

編輯 `statusline-command.sh`：

- `BAR_SEGMENTS` — 進度條格數（預設 16）
- `CACHE_TTL` — API 配額更新頻率，單位秒（預設 60）
- `pct_color()` — 顏色閾值
- `ICON_*` — 替換為你偏好的 Nerd Font 圖示

## 致謝

靈感來自 [claude-powerline](https://github.com/Owloops/claude-powerline)、[steipete](https://gist.github.com/steipete/8396e512171d31e934f0013e5651691e)、[keremkesgin](https://gist.github.com/keremkesgin/1d2cb7278d3d7a0f0202cfa343162b1d)、[coffeewhistle](https://gist.github.com/coffeewhistle/8acee2d946a0c3e90a542e0f3930a4e3) 及 [Freek Van der Herten](https://freek.dev/3028-adding-a-custom-status-line-to-claude-code)。

## 授權

MIT
