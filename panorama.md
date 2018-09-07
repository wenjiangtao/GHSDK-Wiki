## 获取单个模型的所有全景图
需要带上认证信息[(如何认证)](https://gitlab.com/gizmotech/Doc/wikis/signature)

### URL
`GET /api/v2/contents/<string:panorama_uid>/panoramas`

-----

### 请求格式
JSON

-----

### Query
返回字段  |必选| 字段类型 |字段说明 | 
-------|-----:| ----:|-----:|


-----

### Response
返回字段        | 字段类型 |字段说明 | 
--------------|-----:| ----:|
uid   | string | |
name   | string ||


-----

### Example
```python
GET /api/v2/contents/46d2e56dd6293117823a34b5c1e75b81f4932ca9/panoramas

返回：
{
    [
        {
            "uid": "46d2e56dd6293117823a34b5c1e75b81f4932ca9", 
            "name": "全景图1"
        }, 
    ], 
}
```
