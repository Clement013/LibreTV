# MacCMS V10 VOD API Parameters (JSON Format)

This document details the request parameters for the MacCMS V10 `vod` API endpoint (`{your_domain}/index.php/api/provide/vod`) for developers integrating video-on-demand (VOD) data retrieval in JSON format. JSON is the default response format (omit `at` parameter or set to non-`xml`).

## Request Parameters

| Parameter         | Type   | Required | Description                                                                 |
|-------------------|--------|----------|-----------------------------------------------------------------------------|
| `ac`              | string | Optional | Operation type: `list` (video list), `videolist` (detailed list), `detail` (video details). Default: `list`. |
| `t`               | int    | Optional | Category ID to filter videos by category.                                    |
| `pg`              | int    | Optional | Page number for pagination. Default: 1.                                     |
| `pagesize`        | int    | Optional | Records per page, maximum 100. Default: server-defined.                      |
| `wd`              | string | Optional | Search keyword for partial match on video names.                            |
| `ids`             | string | Optional | Comma-separated video IDs for fetching details.   |
| `h`               | int    | Optional | Time range in hours to filter videos updated within the specified period.    |
| `year`            | string | Optional | Year filter: single year (e.g., `2023`) or range (e.g., `2020-2023`).       |
| `from`            | string | Optional | Playback source filter (e.g., `heimuer`) or (e.g., `youku,iqiyi,qq`)to limit playback sources.            |
| `sort_direction`  | string | Optional | Sort order for video update time: `asc` (ascending) or `desc` (descending, default). |

## Example Request
```bash
GET /index.php/api/provide/vod?ac=list&t=1&pg=1&pagesize=20&wd=hero&isend=1&year=2023&from=heimuer&sort_direction=asc
```

## Implementation Notes
- **Encoding**: URL-encode all parameter values to ensure proper request handling.
- **Authentication**: The API may require IP-based authorization. Contact the server administrator if you receive an `api/auth_err` response.
- **Response Structure**: JSON responses include `code` (status), `msg` (message), `page`, `pagecount`, `limit`, `total`, `list` (video data), and `class` (category data, only for `ac=list`).
- **Security**: Input parameters are sanitized server-side to prevent XSS. Developers should validate inputs to ensure secure integration.

## Response Format
- **Success**: `{ "code": 1, "msg": "success", ... }` with video data in `list` and optional `class` for categories.
- **Error**: `{ "code": >1, "msg": "error description" }` or `closed` if the API is disabled.