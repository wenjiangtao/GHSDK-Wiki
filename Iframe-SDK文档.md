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
        "annotations": [ true, false ],
        "explode": [ true, false ],
        "size": [ true, false ],
        "visible": [ true, false ],
        "rotate:" {
            "enabled": [ true, false ],
            "speed": "number"
        },
        "exterior": [
            { "uid": "399c7545bf2cef73c193c805a5f34842652b832a", "name": "默认" }
        ],
        "skybox": [
            { "uid": "0433a2c6c19a9198c6fa16be3a9f30a27a1b5bc8", "name": "展厅" },
            { "uid": "599a8dc00af00e2ce3d1bb59fa774eda922e6675", "name": "停机坪" },
            { "uid": "4ca6583062661f40f16aad364bbc8d2699cb4933", "name": "废弃船厂" }
        ]
    }
    ```

    - `annotations` 是否显示热点
    - `explode` 是否进行模型拆解
    - `size` 是否显示模型尺寸
    - `exterior` 可以切换的外观列表
    - `skybox` 可以切换的天空盒列表
    - `visible` 是否显示模型
    - `rotate` 旋转设置
        - `enabled` 是否开启旋转
        - `speed` 设置旋转速度，默认为


- `gh.getState(callback)` 获取当前状态

    ```js
    gh.getState(console.log);

    {
        "annotations": {
            "items": 0, //annotation 的个数
            "enabled": true //annotation 为开启状态
        },
        "size": true,
        "explode": false,
        "visible": true,
        "rotate:" {
            "enabled": false,
            "speed": 4
        },
        "exterior": { "uid": "399c7545bf2cef73c193c805a5f34842652b832a", "name": "默认" },
        "skybox": { "uid": "0433a2c6c19a9198c6fa16be3a9f30a27a1b5bc8", "name": "展厅" },
    }
    ```


- `gh.setState(data)` 设置当前状态, `data` 可以是选项中的任意一项或多项。

    ```js
    gh.setState({
        annotations: true, // 显示热点
        explode: true, // 拆解模型
        size: true, // 显示尺寸
        visible: true, //显示模型
        rotate: {
            enabled: true, // 开启旋转
            speed: 4 // 旋转速度为4
        },
        skybox: { uid: "4ca6583062661f40f16aad364bbc8d2699cb4933" }, // 切换天空盒
        exterior: { uid: "399c7545bf2cef73c193c805a5f34842652b832a" }, // 更换外观的uid
    })
    ```


- `gh.on(event, callback)`监听事件。目前支持的事件有：
  - `gizmohub:preload:progress` app 预加载进度,
  - `gizmohub:postInitialize` app 准备启动
  - `gizmohub:start` app 启动
  - `gizmohub:model:<uid>:progress` 模型加载进度，`<uid>` 替换成真实的 `uid`
  - `gizmohub:annotation:dialog` 监听注释弹窗事件，返回 bool

- `gh.start()` 手动启动 app。

  默认情况下，app 在预加载资源完成后会自动启动。如果需要手动启动 app，需要在访问
  页面的路径中添加查询字符串：`autoStart=false`。这时候，可以通过监听
  `gizmohub:postInigialize` 事件，在回调函数中调用 `gh.start()` 来启动 app。

```
    import hex from 'crypto-js/enc-hex';
    import sha1 from 'crypto-js/sha1';

    const accesskey = API_ACCESS_KEY;
    const secretkey = API_SECRET_KEY;

    export function genSign() {
        const timestamp = Date.now() / 1000 | 0;
        const signature = btoa(sha1(accesskey + secretkey + timestamp).toString(hex));

        return {
            accesskey,
            timestamp,
            signature
        };
    }
```