## 获取集合信息
需要带上认证信息[(如何认证)](https://gitlab.com/gizmotech/Doc/wikis/signature)

### url
`GET /api/v2/contents/<string:content_uid>/configuration_info`

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
CarExterior   | object |外饰 |
CarInterior   | object |内饰 |
CarView   | object |视角 |
CarWheels   | object |车轮 |

-----

### 4. example
```python
GET: /api/v2/contents/content_uid123/configuration_info

返回：
{
    "CarExterior": [
        {
            "category": 2, 
            "name": "SKU-2", 
            "uid": "fc9f735b50402e6bdd4e9dfbbb72e2659a6997e5"
        }
    ], 
    "CarInterior": [
        {
            "category": 1, 
            "name": "SKU-1", 
            "uid": "744f41943910dc5ca0b0b0d00f238f32a5f970cb"
        }
    ], 
    "CarView": [], 
    "CarWheels": [
        
        {
            "name": "\u8f6e\u80ceA", 
            "uid": "b7ec15a9f73cc0b524064a3c08a6154841fc46e2"
        }, 
        {
            "name": "\u8f6e\u80ceA2", 
            "uid": "0f5277515117177f2b3fea2cf6402ec7171620b8"
        }
    ]
}

```
