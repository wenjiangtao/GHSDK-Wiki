## 获取单个车辆基本信息
需要带上认证信息[(如何认证)](https://gitlab.com/gizmotech/Doc/wikis/signature)

### url
`GET /api/v2/contents/<string:content_uid>`

----

### 请求格式
JSON

----

### Query
无

----

### Response
返回字段        | 字段类型 |字段说明 | 
--------------|-----:| ----:|
uid   |string |标识符 |
name   | string |模型名字 |
created_at   | int |时间戳 |
description   | string |模型描述 |
status   | int |模型状态 |
thumbnail_url   | string |缩略图 |
categories   | int |类别，1008车，1016轮胎 |

-----

### 4. example
```python
GET: /api/v2/contents/content_uid

返回：
{
    "status":1,
    "name":"a",
    "description":"a",
    "created_at":1528982168000,
    "thumbnail_url":"a",
    "uid":"content_uid",
}

```
