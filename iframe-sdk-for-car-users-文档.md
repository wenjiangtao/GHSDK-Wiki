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
        "visible": [ true, false ],
        "rotate:" {
            "enabled": [ true, false ],
            "speed": "number"
        },
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
        "scene": [
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
            "headlight": [ true, false ],
            "distance": "number",
            "visible": [ true, false ],
            "exterior": { "uid": "399c7545bf2cef73c193c805a5f34842652b832a", "name": "默认" },
            "interior": { "uid": "399c7545bf2cef73c193c805a5f34842652b832a", "name": "默认" },
            "sign": {
                "accesskey": "string",
                "timestamp": "number",
                "signature": "string"
            }
        },
        "doors": {
            "status": [ [ true, false ], [ true, false ], [ true, false ], [ true, false ] ],
            "annotations": [ true, false ]
        },
        "panorama": [
            [{ "uid": "xxxxxxxxxxxxx", "name": "xxx" }],
            null
        ]
    }
    ```

    - `annotations` 是否显示热点
    - `moving` 是否行使状态
    - `headlight` 是否开启车灯
    - `size` 是否显示车辆尺寸
    - `wheel` 可以切换的车胎列表, 需要传入签名信息
    - `interior` 可以切换的内饰列表
    - `exterior` 可以切换的外观列表
    - `scene` 可以切换的场景列表
    - ~~`skybox` 可以切换的天空盒列表~~ (已弃用，用 `scene` 代替)
    - `visible` 是否显示一车辆
    - `rotate` 旋转设置
        - `enabled` 是否开启旋转
        - `speed` 设置旋转速度，默认为4
    - `differ` 两车对比，对比时需要传如签名信息
        - `target` 对比车辆的 `uid`，`null` 表示取消对比状态
        - `visible` 是否显示对比车辆，默认为显示
        - `merge` 是否开启两车融合
        - `mersure` 是否开启测量尺寸差异
        - `size` 是否显示对比车辆的尺寸
        - `box` 是否显示车辆的包围盒
        - `headlight` 是否显示对比车辆的车灯
        - `distance` 两车之间的车距，默认为4.4
        - `exterior` 替换对比车辆的外观
        - `interior` 替换对比车辆的内饰
    - `doors`
        - `status` 是否开关车门，默认都为关闭，值为[false, false, false, false]， 顺序： 左前、右前、左后、右后
        - `annotations` 是否显示车门按钮
    - `panorama` 可以切换全景图列表


- `gh.getState(callback)` 获取当前状态

    ```js
    gh.getState(console.log);

    {
        "moving": false,
        "annotations": true,
        "headlight": true,
        "size": true,
        "visible": true,
        "rotate:" {
            "enabled": false,
            "speed": 4
        },
        "differ": {
            "target": null,
            "merge": false,
            "measure": false,
            "box": false,
            "headlight": false,
            "visible": true,
            "distance": 4.4,
            "exterior": { "uid": "399c7545bf2cef73c193c805a5f34842652b832a", "name": "默认" },
            "interior": { "uid": "399c7545bf2cef73c193c805a5f34842652b832a", "name": "默认" }
        },
        "wheel": { "uid": "d1fac90b8415a7bd1500d8e53501c032575f2e1b", "name": "默认" },
        "exterior": { "uid": "399c7545bf2cef73c193c805a5f34842652b832a", "name": "默认" },
        "interior": { "uid": "399c7545bf2cef73c193c805a5f34842652b832a", "name": "默认" },
        "scene": { "uid": "0433a2c6c19a9198c6fa16be3a9f30a27a1b5bc8", "name": "展厅" },
        "doors": {
            "status": [false, false, false, false],
            "annotations": false
        },
        "panorama": { "uid": "xxxxxxxxxxxxx", "name": "xxx" }
    }
    ```


- `gh.setState(data)` 设置当前状态, `data` 可以是选项中的任意一项或多项。

    ```js
    gh.setState({
        moving: true, // 进入行使状态
        annotations: true, // 显示热点
        headlight: true, // 显示车灯
        size: true, // 显示尺寸
        visible: true, //显示一车辆
        rotate: {
            enabled: true, // 开启旋转
            speed: 4 // 旋转速度为4
        },
        differ: {
            target: "2fedc563722c13790a7cea52b6a8fcaaac5ce96e", // 与该 uid 的车进行对比
            merge: false, // 两车不融合
            box: true, // 显示包围盒
            measure: false,
            visible: true,
            distance: 4.4,
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
        scene: { uid: "4ca6583062661f40f16aad364bbc8d2699cb4933" }, // 切换场景
        interior: { "uid": "399c7545bf2cef73c193c805a5f34842652b832a" }, // 更换内饰的uid
        exterior: { "uid": "399c7545bf2cef73c193c805a5f34842652b832a" }, // 更换外观的uid
        doors: {
            status: [true, true, true, true], // 开车门
            annotations: true, // 是否显示开车门按钮
        },
        panorama: null // 退出全景图
    })
    ```


- `gh.on(event, callback)`监听事件。目前支持的事件有：
  - `gizmohub:error` 页面错误
  - `gizmohub:preload:progress` app 预加载进度
  - `gizmohub:postInitialize` app 准备启动
  - `gizmohub:start` app 启动
  - `gizmohub:model:<uid>:progress` 模型加载进度，`<uid>` 替换成真实的 `uid`
  - `gizmohub:model:<uid>:add` 模型添加到场景后触发
  - ~~`gizmohub:skybox:<uid>:progress`~~ *废弃使用*, 用 `gizmohub:scene` 代替
  - `gizmohub:scene:<uid>:progress` 场景加载进度，`<uid>` 替换成真实的 `uid`
  - `gizmohub:annotation:dialog` 监听注释弹窗事件，返回 bool
  
  // 当直接通过连接进入全景图时，会有以下事件
  - `panorama:preload:progress` app 预加载进度
  - `panorama:postInitialize` app 准备启动
  
  // 注意：app启动 仍是 gizmohub:start

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
