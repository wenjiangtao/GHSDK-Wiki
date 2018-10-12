**请先阅读 [For Car Users](https://gitlab.com/gizmotech/Doc/wikis/iframe-sdk-for-car-users-%E6%96%87%E6%A1%A3)，如已阅读请忽略。**

# Speeder

本功能包含了加速测试和刹车测试，在单台车或两台车（对比模式）下均可使用。
**注意：用户需要先配置加速刹车的数据，才可正常使用本功能。**

## API

- `gh.getOptions(callback)`获取可选项

    ```js
    {
        speeder: {
            mode: [0, 1],
            action: [-1, 0, 1]
        }
    }
    ```

    - `mode` 加速刹车模式
      - `0` 加速模式
      - `1` 刹车模式

    - `action` 操作
      - `-1` 复位，两车位置变回初识状态
      - `0` 退出
      - `1` 开始


- `gh.getState(callback)` 获取当前状态

    ```js
    {
        speeder: {
            status: 0,
            mode: 0
        }
    }
    ```
    
    - `status` 当前运行状态
      - `0` 空闲状态
      - `1` 正在测试状态

    - `mode` 加速刹车模式
      - `0` 加速模式
      - `1` 刹车模式

- `gh.setState(options)` 设置当前状态

    ```js
    gh.setState({
        speeder: {
            mode: 0, // 加速模式
            action: 1 // 开始测试
        }
    });
    ```
    
    **注意: 在速度测试运行期间，用户不能重复设置 speeder。**


## Events

本功能运行过程中包含以下事件：

- `gizmohub:speeder:status:running` 速度测试开始
    - 回调参数：无
    - 触发时机：速度测试开始时，即传 `action` 为 1 的时候

- `gizmohub:speeder:status:idle` 速度测试结束
    - 回调参数：无
    - 触发时机：速度测试结束时，即速度测试动画播放结束的时候

- `gizmohub:model:<uid>:speeder:speed` 模型当前速度
    - 回调参数:
      - `time` 当前时间
      - `speed` 当前速度
    - 触发时机：速度测试开始到结束期间


## Examples

- 开启加速测试：

    ```js
    gh.setState({
        speeder: {
            mode: 0,
            action: 1
        }
    });
    ```

- 开启刹车测试：

    ```js
    gh.setState({
        speeder: {
            mode: 1,
            action: 1
        }
    });
    ```

- 退出速度测试：

    ```js
    gh.setState({
        speeder: { action: 0 }
    });
    ```

- 监听速度变化：

    ```js
    gh.on('gizmohub:model:<uid>:speeder:speed', function(data) {
        console.log(data.time, data.speed);
    });
    gh.setState({
       speeder: {
           mode: 0,
           action: 1
       } 
    });
    ```
