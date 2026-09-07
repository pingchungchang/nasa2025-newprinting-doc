# Integration Guide
## Containerization (Docker)

> 打包指令什麼的

## CI/CD & Release Workflow

> 請說明本專案的 CI/CD 觸發規則以及測試策略

## Production Configurations

> 搬到正式環境要做哪些配置的變更  
> 請區分測試環境與系上正式環境的部署方式、Docker Compose 配置差異與環境變數對照

## Production Database Migration

> 怎麼建立 DB 與初始預設資料

## Logging & Monitoring Setup

> 請說明系統 Log 的輸出格式（JSON/Syslog）、紀錄路徑、除錯指令（例：docker logs 或 journalctl）。

## Disaster Recovery / Rollback SOP

> 請說明當正式環境部署失敗或系統崩潰時的緊急應變步驟：如何快速復原資料庫（DB Rollback/Backup 備份還原）以及將 Docker Image 降級至前一個穩定版本。

## Known Issues & TODOs

> 尚未修復的 Bug、對接系上 API 時可能踩到的坑、或是未來效能優化的 TODO