---
name: report-design-system
description: 影像報告系統的設計系統。產生或修改報告系統的畫面、雛型或元件時使用，確保顏色、字級、狀態標籤與按鈕一致。
---

# 影像報告系統設計系統

產生或修改畫面時，依照以下規則。所有變數的實際數值見文末的 tokens.css，產生畫面時把它整段放進頁面的樣式中。

## 必須遵守

- 顏色、字級、間距一律使用 tokens.css 中的變數，不自行加入新顏色。畫面中不得直接寫色值、字級或間距。
- 報告狀態一律用狀態標籤呈現：顏色加上文字與符號，不只靠顏色。列底色只能輔助，不能單獨表達狀態。
- 主色 `--color-primary` 只能搭配深色文字（`--color-text`），不可用白字。主色系的文字與細框線用 `--color-primary-ink`。
- 「醫令已 DC」是醫令狀態，不是報告狀態，會和報告狀態同時出現：不使用列底色，以 4px 左側標記（`--status-marker-width`）加上標籤呈現。
- 錯誤訊息與危險操作用 `--color-danger`，不與「醫令已 DC」共用顏色。
- 每個畫面或區塊最多一個主要按鈕。打報告畫面的主要按鈕是「儲存並跳下一筆」，「認證」使用次要按鈕，不使用「已認證」的狀態色。
- 同一個動作在不同位置要用同一種按鈕，例如「返回工作清單」一律用次要按鈕。
- 同一個功能只放一組按鈕。
- 同一狀態在所有位置用相同文字，例如一律寫「醫令已DC」，不縮寫成「DC」。
- 不使用斜體：中文字型沒有真正的斜體，瀏覽器會用變形模擬。
- `--color-primary-soft` 不得用於報告狀態，也不可和「醫令已DC」標籤底色用在同一個元素上。
- 報告狀態只有未完成、已完成、已認證三種，加上醫令已 DC 標記。流程進度（例如雙人判讀「待裁決」）用「目前進度」文字或一般資訊提示框呈現，不新增狀態色。
- 頁面底色用 `--color-surface`，卡片用 `--color-bg`（灰底白卡）。

## 報告狀態

每個報告狀態各有四個變數：`--status-x`（文字與圖示）、`-bg`（清單列底色）、`-badge`（標籤底色）、`-border`（標籤框線）。

| 狀態 | 變數 | 標示 |
| --- | --- | --- |
| 未完成 | --status-pending | 空心圓圖示＋「未完成」；清單列底色、狀態標籤、未完成數量 |
| 已完成 | --status-done | 半實心圓圖示＋「已完成」；清單列底色、狀態標籤 |
| 已認證 | --status-certified | 實心圓勾圖示＋「已認證」；清單列底色、狀態標籤；報告唯讀 |
| 醫令已 DC | --status-dc | 圓形斜線圖示＋「醫令已DC」；只用列左側標記與標籤，不當列底色；`--status-dc-bg` 只用於標籤與提示框 |

## 字級與間距

| 變數 | 用途 |
| --- | --- |
| `--font-size-sm` | 欄位標籤、狀態標籤、片語、輔助說明 |
| `--font-size-md` | 內文、表格、輸入框、按鈕 |
| `--font-size-lg` | 頁面標題、區塊標題（h1、h2 同級） |
| `--font-size-xl` | 影像顯示區標題 |
| `--font-size-display` | 目前未使用（保留） |
| `--font-weight-regular` / `-medium` / `-bold` | 內文／標籤、表頭、按鈕／標題、數字 |
| `--line-height` / `-tight` | 內文／大數字 |
| `--space-1` | 圖示與文字、標籤內距 |
| `--space-2` | 同一組元件之間 |
| `--space-3` | 表格儲存格、按鈕水平內距 |
| `--space-4` | 卡片內距、區塊之間、頁面左右邊界 |
| `--space-6` | 大區塊之間、對話框內距 |
| `--control-height` | 輸入框、下拉選單、按鈕 |
| `--row-height` | 清單列最小高度 |
| `--radius` / `--radius-lg` / `--radius-pill` | 輸入框、提示框／卡片、影像區、對話框／按鈕、標籤、片語 |

## 元件

### 按鈕

膠囊形（`--radius-pill`），高度一律 `--control-height`，水平內距 `--space-4`，字級 `--font-size-md`，字重 700，字距 `--letter-spacing-button`，框線 `--border-width-strong` 深色（`--color-text`）。

| 類型 | 樣式 | 使用時機 |
| --- | --- | --- |
| 主要 | 主色底、深色字、深色粗框、錯位實心陰影 `--shadow-offset` | 每個畫面或區塊最多一個，例如「儲存並跳下一筆」 |
| 次要 | 白底、深色粗框、深色字，無陰影 | 其他一般操作，例如「上一筆」「下一筆」「重設條件」「返回工作清單」 |
| 危險 | 白底、`--color-danger` 粗框與文字；確認對話框中改為實心（危險色底、白字、深色粗框、錯位陰影） | 不易復原的操作，例如取消認證、退回重打 |

各狀態：

- 滑過：主要按鈕改用 `--color-primary-hover`，並往右下移 2px、陰影縮為 `--shadow-offset-hover`；按下時陰影消失。次要按鈕改用 `--color-surface` 底，危險按鈕改用 `--color-danger-bg` 底。
- 停用：透明度 0.45，游標顯示禁止符號。
- 焦點：`--color-focus` 3px 外框。

### 表格列

| 狀態 | 樣式 |
| --- | --- |
| 一般 | 底色 `--status-x-bg`，最小高度 `--row-height`，分隔線 `--color-border` |
| 滑過 | 加上內框陰影 `inset 0 0 0 1px --color-border-input`，不改底色，以免與狀態色混淆 |
| 選取（或剛從打報告畫面返回的那筆） | 內框 `--border-width-strong` `--color-primary-ink`，不使用 `--color-primary-soft` 底色 |
| 鍵盤焦點 | 同選取，再加上 `--color-focus` 外框 |
| 不可開啟（未照影像） | `--color-surface` 底、次要文字色，加上「未照影像」標籤 |
| 醫令已 DC | 左側 4px `--status-dc` 標記，可與其他任何狀態並存 |
| 勾選（指派用） | 第一欄勾選框，顏色 `--color-primary-ink`；勾選的列使用「選取」樣式。只有未完成的報告可以勾選 |

### 狀態標籤

- 結構固定為「圖示＋文字」：圓角 `--radius-pill`，字級 `--font-size-sm`，字重 600，內距 0 `--space-2`。
- 顏色：文字與圖示用 `--status-x`，底色用 `--status-x-badge`，框線用 `--status-x-border`。
- 圖示使用內嵌 SVG，不使用 ○◐✓ 等文字符號，因為不同字型會讓符號變形。
- 同一狀態在所有位置用相同文字。

### 表單欄位

高度一律 `--control-height`（多行文字框除外），框線 `--color-border-input`，圓角 `--radius`。

| 狀態 | 樣式 |
| --- | --- |
| 一般 | 白底，框線 `--color-border-input`；標籤放在欄位上方，字級 `--font-size-sm`，次要文字色 |
| 聚焦 | 框線改為 `--color-primary-ink`，加 `--color-focus` 3px 外框 |
| 錯誤 | 框線 `--color-danger`；欄位下方用 `--color-danger` 文字說明原因，並加上 `aria-invalid="true"`。不能只用提示訊息（toast）告知 |

### 提示框與判讀對照

- 一般資訊提示框：`--color-surface` 底、`--color-text` 文字、`--color-border-input` 框線，搭配圖示。用於說明流程進度，例如「雙人判讀：等待醫師丙」。不使用任何報告狀態色。
- 判讀對照：兩張並排的卡片（`--color-bg` 底、`--color-border` 框線、`--radius-lg`），各自標示判讀醫師與 BI-RADS 分類；分類用中性標籤（`--color-surface` 底），不用狀態色。
- BI-RADS 分類使用表單欄位中的下拉選單，必填；未選擇時依「表單欄位」的錯誤狀態呈現。

## 需要新增狀態或元件時

先說明要新增什麼、為什麼，等我確認後再加入設計系統，不要直接在畫面上加新的樣式。

## tokens.css

```css
/* 影像報告撰寫系統｜設計 tokens
   以起始範本為基礎整理，規則說明見 design-system.md。
   標示「新增」的變數是範本沒有、由雛型盤點整理出來的。
   報告狀態色採用 B 組「色覺友善色相」（2026-11-03 決定）。
   介面風格：粉色主色＋深色粗框＋錯位實心陰影（2026-11-04 改版）。 */

:root {
  /* ── 色彩：基本 ── */
  --color-primary: #e1bfce;          /* 主要按鈕底色、身分標籤；只能搭配深色文字（--color-text 8.8:1），不可用白字 */
  --color-primary-hover: #d4aabf;    /* 新增：主要按鈕滑過 */
  --color-primary-soft: #f6ebf0;     /* 新增：選取狀態底色（目前這筆、片語滑過） */
  --color-primary-ink: #7a3d5c;      /* 新增：主色系文字、表格列選取框線（對白底 7.9:1） */
  --color-bg: #ffffff;               /* 卡片、表格、輸入框底色 */
  --color-surface: #f3f3f3;          /* 頁面底色、表頭、次要區塊 */
  --color-text: #1f2933;             /* 主要文字 */
  --color-text-muted: #5f6b7a;       /* 次要文字、欄位標籤 */
  --color-border: #d5dbe3;           /* 卡片與表格分隔線（裝飾用） */
  --color-border-input: #7b8594;     /* 新增：輸入框、勾選框、提示框框線（對白底 3.7:1） */
  --color-danger: #b42318;           /* 新增：錯誤訊息、危險操作（不與醫令已 DC 共用） */
  --color-danger-bg: #fdeceb;        /* 新增：錯誤訊息底色 */
  --color-focus: #7a3d5c;            /* 新增：鍵盤焦點框 */
  --color-image-bg: #2f343c;         /* 新增：影像顯示區底色 */
  --color-image-text: #c8cdd5;       /* 新增：影像顯示區文字 */
  --color-overlay: rgba(20, 25, 35, .45); /* 新增：對話框遮罩 */

  /* ── 色彩：報告狀態（B 組：色覺友善色相，以 Okabe-Ito 色盤調深） ──
     橘＝未完成、天藍＝已完成、藍綠＝已認證、洋紅紅＝醫令已 DC。
     三種報告狀態都有列底色；標籤底色與列底色相同。
     每個狀態四個變數：
     --status-x         文字、圖示、左側標記
     --status-x-bg      清單列底色
     --status-x-badge   狀態標籤底色
     --status-x-border  狀態標籤框線 */
  --status-pending: #8f4500;   --status-pending-bg: #fdecd8;   --status-pending-badge: #fdecd8;   --status-pending-border: #e7a76a;   /* 未完成 */
  --status-done: #0d5a80;      --status-done-bg: #e0f1fa;      --status-done-badge: #e0f1fa;      --status-done-border: #86c2e2;      /* 已完成 */
  --status-certified: #00624a; --status-certified-bg: #d9f2ea; --status-certified-badge: #d9f2ea; --status-certified-border: #7fc8b2; /* 已認證 */
  --status-dc: #b0204a;        --status-dc-bg: #fbe5ec;        --status-dc-border: #e79ab2;       /* 醫令已 DC：左側標記＋標籤，不當列底色；-bg 只用於標籤與提示框 */

  /* ── 字級 ── */
  --font-family: "Noto Sans TC", "Microsoft JhengHei", "PingFang TC", sans-serif;
  --font-family-mono: ui-monospace, "Cascadia Mono", Consolas, monospace; /* 新增：僅用於快捷鍵提示 */
  --font-size-sm: 13px;        /* 欄位標籤、狀態標籤、片語、輔助說明 */
  --font-size-md: 15px;        /* 內文、表格、輸入框、按鈕 */
  --font-size-lg: 18px;        /* 區塊標題、頁面標題 */
  --font-size-xl: 22px;        /* 影像顯示區標題 */
  --font-size-display: 40px;   /* 新增：目前未使用（保留） */
  --font-weight-regular: 400;  /* 新增 */
  --font-weight-medium: 600;   /* 新增：標籤、表頭、按鈕 */
  --font-weight-bold: 700;     /* 新增：標題、數字 */
  --line-height: 1.5;          /* 新增 */
  --line-height-tight: 1.2;    /* 新增：大數字 */

  /* ── 間距 ── */
  --space-1: 4px;   /* 圖示與文字、標籤內距 */
  --space-2: 8px;   /* 同組元件之間 */
  --space-3: 12px;  /* 表格儲存格、按鈕水平內距 */
  --space-4: 16px;  /* 卡片內距、區塊之間、頁面左右邊界 */
  --space-6: 24px;  /* 大區塊之間、對話框內距 */

  /* ── 尺寸（新增） ── */
  --control-height: 36px;      /* 輸入框、下拉選單、按鈕統一高度 */
  --row-height: 44px;          /* 清單列最小高度 */
  --status-marker-width: 4px;  /* 醫令已 DC 左側標記寬度 */

  /* ── 圓角 ── */
  --radius: 6px;          /* 輸入框、提示框（按鈕改用 --radius-pill） */
  --radius-lg: 8px;       /* 新增：卡片、影像區、對話框 */
  --radius-pill: 999px;   /* 新增：按鈕、狀態標籤、片語 */

  /* ── 框線與按鈕風格（新增，2026-11-04） ── */
  --border-width-strong: 2px;                       /* 按鈕、選取列、目前這筆的粗框 */
  --shadow-offset: 3px 3px 0 var(--color-text);     /* 主要按鈕：錯位實心陰影 */
  --shadow-offset-hover: 1px 1px 0 var(--color-text); /* 滑過時陰影縮短，按鈕往右下移 */
  --letter-spacing-button: .06em;                   /* 按鈕文字字距 */

  /* ── 陰影（新增） ── */
  --shadow-overlay: 0 12px 40px rgba(0, 0, 0, .25); /* 對話框、提示訊息 */
}
```
