# Epson L485 Printer Mode Troubleshooting

A real-world troubleshooting record for an Epson L485 that became stuck in **Printer mode** after startup and displayed:

`Flag Check Inspection: ON / initial charge: OFF`

## Problem

- Model: Epson L485, continuous ink supply system, sales area ECC
- The printer was stuck on “Printer mode” and could not be operated normally.
- Holding the power button was required to shut it down.
- A test-page attempt also produced `fatal error code: 034008`.

## Successful Recovery

The successful recovery method used a third-party **Resetter.exe** adjustment utility.

Connect the printer by USB, launch the utility, select **L485**, and enter:

**Adjustment → Initial setting**

Select:

- `EEPROM data initial setting`
- `ENetwork data initial setting`

Do **not** select Serial No./MAC.

Press **Perform**, confirm:

- Model: L485
- Sales Area: ECC

The utility may report that network information initialization failed and instruct you to restore network settings from the printer panel. After completing the operation and powering the printer off and on again, the printer successfully returned to the normal main screen and Wi-Fi connectivity was restored.

## Follow-up

EEPROM initialization can restore some settings and calibration values to factory defaults. After recovery:

1. Change the panel language back to Traditional Chinese if necessary.
2. If print quality or alignment is affected, run **Head Alignment**.
3. Check product information such as the serial number and MAC address.

For the original Traditional Chinese record, see:

- [繁體中文完整紀錄](docs/Epson-L485-排障紀錄.md)

> **Note:** Resetter.exe is a third-party service/adjustment utility. This document records one actual successful recovery procedure; it does not guarantee that the same procedure is appropriate for every Epson L485. Verify the model and sales area before performing EEPROM initialization and use the procedure at your own risk.
