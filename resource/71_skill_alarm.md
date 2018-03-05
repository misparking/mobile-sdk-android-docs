# 技能模块 Skill
## 闹钟 Alarm
### 1、获取闹钟列表
请求获取设备上的闹钟列表：

```Java
RokidMobileSDK.skill.alarm().getList(deviceId)
```

接收到Event：

```Java
@Subscribe(threadMode = ThreadMode.MAIN)
public void onAlarmEvent(EventAlarmBean eventAlarm) {
    // ...
}
```

EventAlarmBean 字段说明：

| 参数 | 类型 | 必要？ | 说明 |
| --- | --- | --- | --- |
| topic | int | 是 | 闹钟主题标志符 |
| topicName | String | 是 | 闹钟主题名称 |
| alarmList | List<AlarmContentBean> | 否 | 闹钟列表 |

AlarmContentBean 字段说明：

| 参数 | 类型 | 必要？ | 说明 |
| --- | --- | --- | --- |
| id |  int| 是 | 闹钟Id |
| year | int | 是 | 年 |
| month | int | 是 |  月|
| day | int | 是 | 日 |
| hour | int | 是 | 小时 |
| minute | int | 是 | 分钟 |
| date | String | 是 | 重复模式的文案 |
| ext | Map<String, String> | 是 | 扩展字段，根据自己业务进行扩展 |

<font color='red'>
注：目前只有Lua版Linux系统支持该字段
    ext字段是手机App与系统通信特有的字段，添加或修改时传入，获取列表时原样返回，以下划线_开始的key是预定义key。
    ext字段可以为空；因为暂时没有删除字段的接口，所以修改时(SpecificTime)需要传入所有的key和value。
  系统不支持时间完全相同的闹钟，所以更新和删除时不会校验ext是否匹配。
  
| 名称 | 类型 | 描述 |
| --- | --- | --- |
| _ringtone | string | 闹钟铃声地址，会覆盖全局的闹钟主题 |
    
第三方需求可以由他们自定义字段，比如小雅小雅的标签需求
</font>

---

### 2、添加闹钟
添加一个闹钟。

示例代码：

```Java
AlarmContentBean alarmContentBean = new AlarmContentBean()
alarmContentBean.year = 2018
alarmContentBean.month = 3
alarmContentBean.day = 3
alarmContentBean.hour = 14
alarmContentBean.minute = 30

RokidMobileSDK.skill.alarm().add(deviceId, alarmContentBean , repeatType);
```

AlarmContentBean 字段说明：

| 参数 | 类型 | 必要？ | 说明 |
| --- | --- | --- | --- |
| id |  int| 是 | 闹钟Id |
| year | int | 是 | 年 |
| month | int | 是 |  月|
| day | int | 是 | 日 |
| hour | int | 是 | 小时 |
| minute | int | 是 | 分钟 |
| date | String | 是 | 重复模式的文案 |
| ext | Map<String, String> | 是 | 扩展字段，根据自己业务进行扩展 |

repeatType 解释：

```
"" : 仅此一次 (注：空字符串)
DAY : 每天
WEEKDAY : 工作日
WEEKEND : 每周末
D1 : 每周一
D2 : 每周二
D3 : 每周三
D4 : 每周四
D5 : 每周五
D6 : 每周六
D7 : 每周日
```

---

### 3、删除一个闹钟
删除一个闹钟：
 
```Java
RokidMobileSDK.skill.alarm().delete(deviceId, alarmContentBean);
```
 
注：字段说明 请参考上面 6.1.1
 
---

### 4、更新闹钟
更新一个闹钟：

```Java
RokidMobileSDK.skill.alarm().update(deviceId, alarmContentBean, updateHour, updateMinute, repeatType);
```
 
注：字段说明 请参考上面 1 和 2
 
---

