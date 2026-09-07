# Dependencies & Hardware

## External Dependencies
- Windows VM + Ubuntu VM
- Windows VM 主要用途是由於 ariel 提供的 driver 只有 windows 可以安裝，Mac 以及 linux 無法使用，因此目前架構是將所有列印 request 送到後端執行

## Hardware Infrastructure
- Windows 與 Ubuntu 系統要可以互相連線到對方
- 目前由於 Ariel 上已經有綁定一套餘額系統，為了繞過此系統目前使用 admin 帳戶從 windows VM 送列印 request 到印表機，因此 **new printing 的餘額與 204 的餘額沒有相連**
- 在 windows 上按照 [這裡](https://nasalab.csie.ntu.edu.tw/service/new_printing_tutorial.html) 安裝 driver ，並在 `printer_scripts` 修改 PRINTER_NAME ，以保證可以成功連線
