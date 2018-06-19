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
        "moving": [ true, false ],
        "headlight": [ true, false ],
        "size": [ true, false ],
        "wheel": [
            {
                "uid": "d1fac90b8415a7bd1500d8e53501c032575f2e1b",
                "name": "默认",
                "sign": {
                    "accesskey": "string",
                    "timestamp": "number",
                    "signature": "string"
                }
            },
            {
                "uid": "f409ba97cf02c2e24721556e2342d9c747e3859f",
                "name": "lunzi",
                "sign": {
                    "accesskey": "string",
                    "timestamp": "number",
                    "signature": "string"
                }
            }
        ],
        "interior": [
            { "uid": "399c7545bf2cef73c193c805a5f34842652b832a", "name": "默认" }
        ],
        "exterior": [
            { "uid": "399c7545bf2cef73c193c805a5f34842652b832a", "name": "默认" }
        ],
        "skybox": [
            { "uid": "0433a2c6c19a9198c6fa16be3a9f30a27a1b5bc8", "name": "展厅" },
            { "uid": "599a8dc00af00e2ce3d1bb59fa774eda922e6675", "name": "停机坪" },
            { "uid": "4ca6583062661f40f16aad364bbc8d2699cb4933", "name": "废弃船厂" }
        ],
        "differ": {
            "target": [ "uid", null ],
            "merge": [ true, false ],
            "measure": [ true, false ],
            "size": [ true, false ],
            "box": [ true, false ],
            "exterior": { "uid": "399c7545bf2cef73c193c805a5f34842652b832a", "name": "默认" },
            "interior": { "uid": "399c7545bf2cef73c193c805a5f34842652b832a", "name": "默认" },
            "sign": {
                "accesskey": "string",
                "timestamp": "number",
                "signature": "string"
            }
        }
    }
    ```

    - `annotations` 是否显示热点
    - `moving` 是否行使状态
    - `headlight` 是否开启车灯
    - `size` 是否显示车辆尺寸
    - `wheel` 可以切换的车胎列表, 需要传入签名信息
    - `interior` 可以切换的内饰列表
    - `exterior` 可以切换的外观列表
    - `skybox` 可以切换的天空盒列表
    - `differ` 两车对比，对比时需要传如签名信息
        - `target` 对比车辆的 `uid`，`null` 表示取消对比状态
        - `merge` 是否开启两车融合
        - `mersure` 是否开启测量尺寸差异
        - `size` 是否显示对比车辆的尺寸
        - `box` 是否显示车辆的包围盒
        - `exterior` 替换对比车辆的外观
        - `interior` 替换对比车辆的内饰


- `gh.getState(callback)` 获取当前状态

    ```js
    gh.getState(console.log);

    {
    "moving": false,
    "annotations": true,
    "headlight": true,
    "size": true,
    "differ": {
        "target": null,
        "merge": false,
        "measure": false,
        "box": false,
        "exterior": { "uid": "399c7545bf2cef73c193c805a5f34842652b832a", "name": "默认" },
        "interior": { "uid": "399c7545bf2cef73c193c805a5f34842652b832a", "name": "默认" }
    },
    "wheel": { "uid": "d1fac90b8415a7bd1500d8e53501c032575f2e1b", "name": "默认" },
    "exterior": { "uid": "399c7545bf2cef73c193c805a5f34842652b832a", "name": "默认" },
    "interior": { "uid": "399c7545bf2cef73c193c805a5f34842652b832a", "name": "默认" },
    "skybox": { "uid": "0433a2c6c19a9198c6fa16be3a9f30a27a1b5bc8", "name": "展厅" }
    }
    ```


- `gh.setState(data)` 设置当前状态, `data` 可以是选项中的任意一项或多项。

    ```js
    gh.setState({
        moving: true, // 进入行使状态
        annotations: true, // 显示热点
        headlight: true, // 显示车灯
        size: true, // 显示尺寸
        differ: {
            target: "2fedc563722c13790a7cea52b6a8fcaaac5ce96e", // 与该 uid 的车进行对比
            merge: false, // 两车不融合
            box: true, // 显示包围盒
            sign: {
                accesskey: "string",
                timestamp": "number",
                signature": "string"
            }

        },
        wheel: {
            uid: "d1fac90b8415a7bd1500d8e53501c032575f2e1b", // 切换车轮的uid
            name: "默认",
            sign: {
                "accesskey": "string",
                "timestamp": "number",
                "signature": "string"
            }
        }
        skybox: { uid: "4ca6583062661f40f16aad364bbc8d2699cb4933" }, // 切换天空盒
        interior: { "uid": "399c7545bf2cef73c193c805a5f34842652b832a" }, // 更换内饰的uid
        exterior: { "uid": "399c7545bf2cef73c193c805a5f34842652b832a" } // 更换外观的uid
    })
    ```


- `gh.on(event, callback)`监听事件。目前支持的事件有：
  - `gizmohub:preload:progress` app 预加载进度,
  - `gizmohub:postInitialize` app 准备启动
  - `gizmohub:start` app 启动
  - `gizmohub:model:<uid>:progress` 模型加载进度，`<uid>` 替换成真实的 `uid`


- `gh.start()` 手动启动 app。

  默认情况下，app 在预加载资源完成后会自动启动。如果需要手动启动 app，需要在访问
  页面的路径中添加查询字符串：`autoStart=false`。这时候，可以通过监听
  `gizmohub:postInigialize` 事件，在回调函数中调用 `gh.start()` 来启动 app。
