# 【无人机】鲁班猫Cat5V2与PX4飞控的通信篇

鲁班猫Cat5V2开发板，或者指鲁班猫Linux系列开发板40pin接口（树莓派同款接口），默认为**复用关闭**状态，所以要使用指定功能需要配置复用
<!--more-->

⛏ [官方链接](https://doc.embedfire.com/linux/rk356x/quick_start/zh/latest/quick_start/40pin/uart/uart.html)

其中串口的引脚关系如下表所示

|串口|引脚|功能|
|---|---|---|
|TXD|8|发送信号线|
|RXD|10|接受信号线|
对应实物的40pin接口

![](/assets/lubancat_px4uart/202506170939501.webp)

### 使能串口

```bash
#进入工具配置
sudo fire-config
```

移动到外设选项，我这里使用的串口将所有**uart**相关的都选择上，确认重启即可

### 额外修改

因为要与PX4飞控进行通信，飞控端设置的通信频率为**921600**，所以板载端也要同样修改。官方指定中没用我们的板子，可能太新未来的及更新？通过检查使用的是**S1**

> - LubanCat-Zero系列使用的是ttyS8  LubanCat-1系列和LubanCat-2系列使用的是ttyS3

为了保持频率相同，需要修改**ttyS1**频率

```bash
#在板卡的终端执行如下命令 查询频率
stty -F /dev/ttyS1
#设置通讯速率，其中ispeed为输入速率，ospeed为输出速率
stty -F /dev/ttyS1 ispeed 921600 ospeed 921600



```

使用cat命令检查是否有信息接收（虽然是乱码）

修改 `mavros` 下的 `px4. launch`, 将串口修改为 `/dev/ttyS1`

---

> 作者: 西塘  
> URL: https://sheetung.github.io/lubancat_px4uart/  

