# APIs & Database Schema
## Database Schema

> 有哪些 Table
> 每個 Table 的欄位名稱、資料型態（INT, VARCHAR）、是否必填、⋯⋯

## API Specifications

> 條列 API（可以參考 mail 或 CSpace 的 API 文件）

## Global Standards & Error Codes

> 請定義 Error Response 格式（如 400, 401, 403, 429, 500 JSON 結構），並說明有哪些 API 具備 Rate Limit 限制。  
> 請註明全站統一的資料格式，特別是 Date 與 Datetime 的 ISO 格式與時區（例：YYYY-MM-DDTHH:mm:ssZ / UTC+8）。

## Authentication & RBAC Spec

> 請寫出系統認證方式（Session Cookie / JWT / CSRF）以及 RBAC 角色權限對照表（例：Admin、User 的權限差異與 DRF Permission Class）。