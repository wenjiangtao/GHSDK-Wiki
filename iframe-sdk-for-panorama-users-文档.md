# Viewer

## 依赖

- `GizmoHubSDK`


## 用法

### 初始化 SDK

```js
var iframe = document.getElementById('application');
var gh = new GizmohubSDK(iframe);
```

### API

- `gh.getOptions(callback)` 获取可选项

    ```js
    gh.getOptions(console.log);

    {
        "panorama": [
            [{ 
              "target": "xxxxxxxxxxxxx", 
              "anchor": [true, false],
              "annotation": [true, false],
            }],
            null
        ]
    }
    ```
    - `panorama` 可以切换全景图列表
      - `target` 全景图的uid
      - `anchors` 是否开启锚点
      - `annotations` 是否开启注释`


- `gh.getState(callback)` 获取当前状态

    ```js
    gh.getState(console.log);

    {
        "panorama": { 
            "target": "xxxxxxxxxxxxx", //当前全景图的uid
            "anchors": true, // 锚点为开启的状态
            "annotations": true, // 注释为开启的状态
          }
    }
    ```


- `gh.setState(data)` 设置当前状态, `data` 可以是选项中的任意一项或多项。
    
    ```js
    gh.setState({
        panorama: null // 退出全景图
    });

    gh.setState({
        "panorama": { 
            "target": "xxxxxxxxxxxxx", //全景图的uid
            "anchors": true, // 开启锚点
            "annotations": true, // 开启注释
          }
    });
    ```


- `gh.on(event, callback)`监听事件。目前支持的事件有：
  - `panorama:preload:progress` app 预加载进度
  - `panorama:postInitialize` app 准备启动
  - `gizmohub:start` app 启动   // 注意：app启动的事件监听仍是 gizmohub:start
  - `gizmohub:panorama:<uid>:progress` 全景图加载进度，`<uid>` 替换成真实的 `uid`
  
- `gh.start()` 手动启动 app。

  默认情况下，app 在预加载资源完成后会自动启动。如果需要手动启动 app，需要在访问
  页面的路径中添加查询字符串：`autoStart=false`。这时候，可以通过监听
  `panorama:postInigialize` 事件，在回调函数中调用 `gh.start()` 来启动 app。

- 注意事项
  - 当 `panorama` 设为 `null` 的时候，会退出全景图，进入模型渲染。
  - 模型渲染`API`可参考：
    - [Iframe sdk 文档](https://gitlab.com/gizmotech/Doc/wikis/Iframe-SDK%E6%96%87%E6%A1%A3)
      - [For Car Users](https://gitlab.com/gizmotech/Doc/wikis/iframe-sdk-for-car-users-%E6%96%87%E6%A1%A3)





