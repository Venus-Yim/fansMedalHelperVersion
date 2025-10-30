---
sidebar:
    - /guide/
    - /guide/ali-cloud-simple/
    - /guide/ali-cloud/
    - /guide/tx-cloud/
    - /guide/docker/
    - /guide/qinglong/
    - /guide/location/
---

# 开始

当前版本：0.4.0

## 目前已实现功能

| 功能                                    | 奖励                                    |
| --------------------------------------- | --------------------------------------- |
| 每日弹幕 5/10 条(开播不发)              | 5 亲密度(大航海)/维持灯牌点亮(非大航海) |
| 每日点赞 5/30 次直播间                  | 5 亲密度(大航海)/维持灯牌点亮(非大航海) |
| 每日观看 25 分钟                        | 5\*6\=30 亲密度                         |
| 多账号支持                              |                                         |
| 微信推送通知                            |                                         |

## 配置文件说明 users.yaml

```yaml
USERS:
    - access_key: xxxxxxxxxx # 注意冒号后的空格 否则会读取失败 英文冒号
      white_uid: # 换行，必须另起一行
        - 3493141164329470  # 貔小貅
        - 1945855008  # 良人
        - 3493081957534067  # 弥绘貘貘
        - 3546928038022021  # 钻宝
        # 白名单用户UID, 为直播间主播对应的UID（不是直播间房间号！！！）, 以逗号分隔, 填写后只会对这些直播间执行任务（点赞、发弹幕、观看）, 黑名单失效, 不用就留为空白
        # 对于粉丝牌较多 或者 希望按一定优先顺序执行任务的用户, 建议使用白名单。使用白名单时，在同等优先级下，建议将轮播直播间放在靠前位置。
      banned_uid:  # 黑名单UID 格式同白名单, 填了后将不会打对这些直播间执行任务, 用英文逗号分隔。不填则不限制,两个都不填则对该用户有粉丝牌的所有直播间执行任务
    - access_key:
      white_uid: 
      banned_uid: 
    # 注意对齐，必须使用空格对齐，不要用tab等其他占位符对齐！会报错！
    # 多用户以上格式添加
    # 使用文本编辑器编辑时可能有显示问题,如遇报错请关闭此文件重新打开,检查格式
    # 井号后为注释 井号前后必须有空格！井号前后必须有空格！井号前后必须有空格！
    # 冒号后面也要有空格！冒号后面也要有空格！冒号后面也要有空格！
    # 英文冒号, 英文冒号！英文逗号, 英文逗号！
CRON: # 2 0 * * *
# 如启用，请手动删除"CRON: "后面的井号
# 这里是 cron 表达式, 第一个参数是分钟, 第二个参数是小时
# 例如每天凌晨0点2分执行一次为 2 0 * * *
# 如果不填, 则不使用内置定时器; 填写正确后要保持该进程一直运行, 即关闭进程/重启系统等行为都会导致其无法自动运行，需重新手动启动

SENDKEY: # Server酱微信推送 可选 获取地址：https://sct.ftqq.com/
MOREPUSH: # 更多种类的推送 详细配置见文档

PROXY: # 推送代理地址,如：http://1.2.3.4:5678 支持 http/socks4/socks5 不支持 https 不用代理的不用填
#########以下为自定义配置#########

LIKE_CD: 0.3 # 点赞间隔时间,单位秒,默认（留空不填）0.3秒,设置为0则不点赞

DANMAKU_CD: 3 # 弹幕间隔时间,单位秒,默认3秒,设置为0则不发弹幕

WATCH_TARGET: 25 # 每直播间满亲密度所需有效观看时长,单位 min ,设置为0则不进行观看, 默认 25 分钟

WATCH_MAX_ATTEMPTS: 50 # 单次执行,每直播间允许的最多尝试观看的时长,单位 min ,数值不能小于WATCH_TARGET,默认 50 分钟

WEARMEDAL: 0 # 是否弹幕打卡时自动带上当前房间的粉丝牌,避免房间有粉丝牌等级禁言,默认关闭,设置为1则开启


```
::: tip 提示
B 站 `access_key` 获取工具：[Release B 站 access_key 获取工具 · Venus-Yim/fansMedalHelper (github.com)](https://github.com/Venus-Yim/fansMedalHelper/releases/tag/logintool)
:::

::: warning 警告
请务必严格填写，否则程序将读取失败，可以在这里 [YAML、YML 在线编辑器(格式化校验)-BeJSON.com](https://www.bejson.com/validators/yaml_editor/) 验证你填的 yaml 是否正确。
:::



## 多种推送方式配置 MOREPUSH 参数 （可选）

| 推送方式                                                                             | 参数                                                                                                               |
| ------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------ |
| [bark](https://apps.apple.com/us/app/bark-customed-notifications/id1403753865)       | {"notifier":"bark","params":{"markdown":false,"key":"xxxxxx"}}                                                     |
| [dingtalk](https://open.dingtalk.com/document/group/custom-robot-access) 钉钉机器人  | {"notifier":"dingtalk","params":{"markdown":false,"token":"xxxxxx"}}                                               |
| [discord](https://support.discord.com/hc/en-us/articles/228383668-Intro-to-Webhooks) | {"notifier":"discord","params":{"markdown":false,"webhook":"https://discord.com/api/webhooks/xxxxxx"}}             |
| [pushplus](https://www.pushplus.plus/)                                               | {"notifier":"pushplus","params":{"markdown":false,"token":"xxxxxx"}}                                               |
| [qmsg](https://qmsg.zendee.cn/)                                                      | {"notifier":"qmsg","params":{"markdown":false,"key":"xxxxxx"}}                                                     |
| [telegram](https://core.telegram.org/bots)                                           | {"notifier":"telegram","params":{"markdown":false,"token":"xxxxxx","userid":"xxxxxx"}}                             |
| [wechatworkapp](https://developer.work.weixin.qq.com/document/path/90236) 企业微信   | {"notifier":"wechatworkapp","params":{"markdown":true,"corpid":"xxxxxx","corpsecret":"xxxxxx","agentid":"xxxxxx"}} |
| [wechatworkbot ](https://developer.work.weixin.qq.com/document/path/91770) 企业微信  | {"notifier":"wechatworkbot","params":{"markdown":false,"key":"xxxxxx"}}                                            |
| [lark](https://open.feishu.cn/document/ukTMukTMukTM/ucTM5YjL3ETO24yNxkjN) 飞书       | {"notifier": "lark", "params": {"webhook": "xxxxxx", "keyword": "", "sign": ""}}                                   |

::: tip 例如

我想用 `pushplus` 推送消息，在官方申请到的 `token` 为： `abcabcacb` ，配置文件中的 `MOREPUSH` 就如下填写

```yaml
MOREPUSH: { "notifier": "pushplus", "params": { "markdown": false, "token": "abcabcacb" } }
```

`markdown` 建议都设为 false，因为可能会出现推送格式异常。

:::
