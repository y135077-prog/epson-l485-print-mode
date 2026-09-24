# Epson L485 維修排障紀錄

## 問題摘要
- **機型**：Epson L485（連續供墨，銷售區 ECC）
- **症狀**：開機後螢幕卡在「Printer mode」，無法操作；按電源鍵變紅畫面顯示 `Flag Check Inspection: ON / initial charge: OFF`，需長按電源鍵才能關機。
- **過程**：曾嘗試列印測試頁時出現 `fatal error code: 034008`（機械層級卡紙/進紙機構錯誤）。

## 診斷結論
- `Flag Check Inspection: ON` = 印表機卡在**原廠出廠檢測（Factory Inspection / Set Jig）模式**，EEPROM 的建置旗標未關閉。
- `initial charge: OFF` = 初始注墨未被標記完成。
- 034008 屬 034xxx 系列（CR 印字頭滑車 / APG 壓紙機構機械錯誤），與卡紙相關；處理機械卡阻後應先確認機構可正常動作。

## 最終解法（成功）
使用第三方調整/歸零程式 **Resetter.exe**（針對 L380/L383/L385/L485，搭配 apdadrv.dll），透過 USB 連線依序操作：

### 1. 進入程式
- USB 連接印表機 → 執行 `Resetter.exe` → Select **L485** → `Particular Adjustment Mode`。

### 2. 嘗試（未完全成功）步驟
- **Maintenance → Shipping setting**：僅「Cleaning flag set」可勾選，按 Write 顯示「The shipping setting value has been written properly.」→ 重開機後仍卡 Printer mode。
- **Maintenance → Ink charge → Initial ink charge**：顯示消耗 7g 黑/4g 每色、約 20 分鐘，執行後進度條卡死、印表機無動作 → 安全中斷。

### 3. 關鍵成功步驟：Adjustment → Initial setting
- 勾選 **`EEPROM data initial setting`**（＋ `ENetwork data initial setting`），不勾 Serial No./MAC。
- 按 **`Perform`** → 確認機型 `L485` / 銷售區 `ECC` 選「是」。
- 跳出「網路資訊初始化失敗，請由面板恢復預設」→ 依指示關機。
- 最終出現：**「The initial setting value has been written in EEPROM properly. Turn on power and keep adjusting it.」**
- 重新開機 → **成功進入正常主畫面，Wi-Fi 也恢復連線**。

## 後續處理
- **語言變簡體**：`Initial setting` 把語言還原成出廠預設 → 面板 `Setup → 語言/Language → 繁體中文` 改回。
- **校準建議**：EEPROM 重置後 Bi-D / PF / Head ID 等校準值已回出廠預設，若列印歪斜/品質差，進 `Maintenance → Head Alignment（噴頭校準）` 跑一次。
- **序號/MAC**：若被清空，可至 `Setup → System Administration → 產品資訊` 檢查補填。

## 參考工具與資源
- 歸零程式：`F:\epson\歸零程式\Epson_L380_L383_L385_L485_Reset`（含 Resetter.exe、apdadrv.dll、使用說明 .doc）
- 注意：此工具為第三方調整程式，用於維修用途；主要可作廢墨計數器重置與 EEPROM 初始化。
