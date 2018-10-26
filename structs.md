### carExterior 和 carInterior
返回字段        | 字段类型 |字段说明 | 
--------------|-----:| ----:|
uid   | string |标识uid |
name   | string |名字 |
category   | int |类别,1是内饰，2是外饰,0是默认 |

---------------
### carView
返回字段        | 字段类型 |字段说明 | 
--------------|-----:| ----:|
title   | string |标题 |
id   | string |uuid |

------------
### carWheel
返回字段        | 字段类型 |字段说明 | 
--------------|-----:| ----:|
tire_group_name   | string |轮胎组名字 |
tire_group_uid   | string |轮胎组uid |
tires   | object array |[轮胎](http://git.gizmotech.cn/Gizmo/gizmohub/wikis/structs#tire) |

-----------

### tire
返回字段        | 字段类型 |字段说明 | 
--------------|-----:| ----:|
name   | string |轮胎名字 |
uid   | string |轮胎uid |

---------------

### car
返回字段        | 字段类型 |字段说明 | 
--------------|-----:| ----:|
name   | string | 名字|
uid   | string |uid |
status   | int |状态，1为正常 |
created_at| int |创建时间 |
thumbnail_url|string|缩略图|
description|string|描述|
categories|int|类别，1008车，1016轮胎

### screenshot
返回字段        | 字段类型 |字段说明 | 
--------------|-----:| ----:|
imgaes   | string |截图列表|
uid   | string |uid |
num   | int |张数 |

### speed
返回字段        | 字段类型 |字段说明 | 
--------------|-----:| ----:|
type   |int |0:time 1:distance|
data   | object |{time,speed},{distance,speed}|

