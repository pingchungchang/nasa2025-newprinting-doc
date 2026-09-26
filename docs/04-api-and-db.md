# APIs & Database Schema
## Database Schema

> 有哪些 Table
> 每個 Table 的欄位名稱、資料型態（INT, VARCHAR）、是否必填、⋯⋯

## API Specifications

> 條列 API（可以參考 mail 或 CSpace 的 API 文件）

### `POST /login/`

登入並取得 session cookie 。

**Request body:**
```json
{ "username": "b14902003", "password": "pw123" }
```

**Response body `200_OK`:** （登入成功）
```json
{ "status": "success" }
```

> Set-Cookie: todo

**Response body `401_UNAUTHORIZED`:** （登入失敗）
```json
{ "status": "failed", "errorReason": "Invalid credentials" }
```

### `GET /me/`

查詢目前使用者的名稱與餘額，要求 session cookie 。

**Response body `200_OK`:** （有登入）
```json
{ "username": "b14902003", "balance": "437" }
```

**Response body `HTTP_401_UNAUTHORIZED`:** （沒登入）
```json
{ "message": "Not logged in" }
```

### `POST /print/`

送出列印工作，要求 session cookie 。

**Serializer:**
```python
class PdfUploadSerializer(serializers.Serializer[PdfUploadData]):
    # files = serializers.ListField(child=serializers.FileField(), allow_empty=False)
    files = serializers.ListField(
        child=serializers.FileField(allow_empty_file=False, use_url=False),
        allow_empty=False,
    )
    duplex: serializers.BooleanField = serializers.BooleanField(
        default=False, label="雙面列印"
    )
```

**Response body `202_ACCEPTED`:** （送出成功）
```json
{ "jobId": "10", "balance": "432" }
```

**Response body `402_PAYMENT_REQUIRED`:** （餘額不足）
```json
{ "message": "Not enough balance" }
```

**Response body `403_FORBIDDEN`:** （沒登入）
```json
{ "message": "Not logged in" }
```

**Response body `403_FORBIDDEN`:** （序列化失敗）
```json
{ "message": "Serializer error" }
```

**Response body `500_INTERNAL_SERVER_ERROR`:** （排程器出錯）
```json
{ "message": "Database error during submission" }
```

**Response body `500_INTERNAL_SERVER_ERROR`:** （寫檔案出錯）
```json
{ "message": "File system error: `error message`" }
```

> todo: `GET /jobs/`
> todo: `GET /jobs/<str:jobId>/`
> todo: `GET /admin/me`
> todo: `GET /admin/jobs`
> todo: `GET /admin/jobs/<str:jobId>/`
> todo: `POST /admin/transfer/`
> todo: `POST /admin/adduser/`
> todo: `POST /admin/removeuser/`
> todo: `GET /admin/user/`

## Global Standards & Error Codes

> 請定義 Error Response 格式（如 400, 401, 403, 429, 500 JSON 結構），並說明有哪些 API 具備 Rate Limit 限制。  
> 請註明全站統一的資料格式，特別是 Date 與 Datetime 的 ISO 格式與時區（例：YYYY-MM-DDTHH:mm:ssZ / UTC+8）。

## Authentication & RBAC Spec

> 請寫出系統認證方式（Session Cookie / JWT / CSRF）以及 RBAC 角色權限對照表（例：Admin、User 的權限差異與 DRF Permission Class）。