# Epson L485 Printer Mode 排障紀錄

Epson L485 開機後卡在 **Printer mode**，並出現 `Flag Check Inspection: ON / initial charge: OFF` 的實際維修排障紀錄。

## 問題

- 機型：Epson L485（連續供墨，銷售區 ECC）
- 開機後卡在「Printer mode」，無法正常操作。
- 電源關機畫面顯示 `Flag Check Inspection: ON / initial charge: OFF`。
- 曾出現 `fatal error code: 034008`。

## 成功解法

實際成功恢復的方法是使用第三方 **Resetter.exe**，進入：

**Adjustment → Initial setting**

勾選：

- `EEPROM data initial setting`
- `ENetwork data initial setting`

不勾選 Serial No./MAC，執行後依畫面確認：

- Model：L485
- Sales Area：ECC

完成 EEPROM 初始化後重新開機，印表機恢復正常主畫面，Wi-Fi 也恢復連線。

## 後續

EEPROM 初始化可能會將部分設定與校準值恢復為出廠狀態，因此：

1. 將面板語言改回繁體中文。
2. 視實際列印狀況重新執行 Head Alignment。
3. 檢查序號、MAC 等產品資訊是否仍存在。

完整排障過程請參閱：

- [繁體中文完整紀錄](docs/Epson-L485-排障紀錄.md)
- [English Troubleshooting Record](README_EN.md)

> 注意：Resetter.exe 為第三方維修工具。本紀錄只整理實際測試成功的方法，不代表工具適用於所有 L485 個案。進行 EEPROM 初始化前應確認機型與銷售區域，並自行承擔操作風險。
