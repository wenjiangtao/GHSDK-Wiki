## 获取模型列表
需要带上认证信息[(如何认证)](http://git.gizmotech.cn/Gizmo/gizmohub/wikis/signature)

### URL
`GET /api/v2/contents/search?name=123&limit=20&offset=0`

-----

### 请求格式
JSON

-----

### Query
返回字段  |必选| 字段类型 |字段说明 | 
-------|-----:| ----:|-----:|
name   | 否|string |要搜索的名字 |
category|否|int|1008车，1016轮胎
limit   | 否|int |每页个数，默认20 |
offset   | 否|int |偏移量，默认0 |

-----

### Response
返回字段        | 字段类型 |字段说明 | 
--------------|-----:| ----:|
data   | object array |[car object](http://git.gizmotech.cn/Gizmo/gizmohub/wikis/structs#car) |
limit   | int |当前每页个数 |
offset   | int |当前偏移量 |
total   | int |总数 |

-----

### Example
```python
GET /api/v2/contents/search?name=奔驰&limit=20&offset=0

返回：
{
    "data": [
        {
            "created_at": 1522218398000, 
            "description": "asdfasdf", 
            "name": "奔驰C200L", 
            "status": 1, 
            "thumbnail_url": "gizmohub.oss-aliyun.com/t123/m123/c123/thumbnails/addm8q4.png", 
            "uid": "46d2e56dd6293117823a34b5c1e75b81f4932ca9"
        }, 
    ], 
    "limit": 20, 
    "offset": 0, 
    "total": 1
}
```

#### 注意事项

- 请求第n页数据，发送的`offset`的值为`n*limit`