
[__SOURCE](README.md)
# ${cont_model} 控制器功能手册 - NTP 客户端时间同步
[__SOURCE](0-about-this-manual/README.md)
# 关于手册
[__SOURCE](0-about-this-manual/precautions.md)
# 注意事项

{% include file="zh/precautions.md" %}
[__SOURCE](0-about-this-manual/safety-notice.md)
# 安全注意事项

{% include file="zh/safety-notice.md" %}
[__SOURCE](1-overview/README.md)
# 1. 概述

{% hint style="info" %}
此功能在 V60.30-00 及更高版本中受支持。
{% endhint %}
[__SOURCE](1-overview/1-description.md)
# 1.1 NTP时间同步是什么？

NTP（网络时间协议）是一种用于在网络中的所有设备之间同步时间的协议。默认情况下，使用UDP端口123。

<p align="center">
 <img src="../_assets/ntp-structure.png"></img>
 <em><p align="center">图1.1 ${cont_model}机器人控制器上的NTP时间同步</p></em>
</p>

---

NTP的定义可以在[RFC 5905：网络时间协议版本4：协议和算法规范](https://datatracker.ietf.org/doc/html/rfc5905)中找到。
[__SOURCE](1-overview/2-requirement.md)
# 1.2 需求

要使用 NTP 客户端时间同步功能，您需要一个可以通过 LAN 直接连接到 ${cont_model} 机器人控制器的 NTP 服务器。

有关如何使用您的主机 PC 作为 NTP 服务器的信息，请参见下一章中的 '[2.NTP 服务器设置](../2-ntp-server-setting/README.md)'。
[__SOURCE](2-ntp-server-setting/README.md)
# 2. NTP 服务器设置

描述了如何使用连接到 ${cont_model} 机器人控制器的主机 PC 作为 NTP 服务器。
[__SOURCE](2-ntp-server-setting/1-window-pc.md)
# 2.1 设置 Windows PC 为 NTP 服务器

要将 Windows PC（Windows 10）用作 NTP 服务器，必须按照以下步骤操作。

1. 在 Windows 中启用 NTP 服务器功能。
    * 使用 w32time（Windows 时间服务）
    1. 打开“注册表编辑器”
    2. 前往路径 'HKEY_LOCAL_MACHINE/SYSTEM/CurrentControlSet/Services/W32Time'
        * 在 'Config' 中，将 'AnnounceFlags' 条目的值设置为 5（NTP 服务器） - 默认值可能为 10
        <p align="center">
         <img src="../_assets/reg-announceflags.png"></img>
         <em><p align="center">图 2.1 NTP 服务器设置（注册表编辑器）</p></em>
        </p>

        * 在 'TimeProviders/NtpServer' 中，将 'Enabled' 条目的值设置为 1（启用）
        <p align="center">
         <img src="../_assets/reg-enabled.png"></img>
         <em><p align="center">图 2.2 NTP 服务器设置（注册表编辑器）</p></em>
        </p>
2. 重新启动 Windows 时间服务
    * 在“命令提示符”中，以管理员权限输入以下命令。
    ```
        net stop w32time
        net start w32time
    ```
3. Windows 防火墙设置
    * NTP 默认使用 UDP 端口 123。因此，必须打开该端口以作为 NTP 服务器
    1. 打开“控制面板”
    2. 选择“Windows 防火墙”
    3. 选择“高级设置”
    4. 在“具有高级安全性的 Windows 防火墙”中选择“入站规则”
        <p align="center">
         <img src="../_assets/defender.png"></img>
         <em><p align="center">图 2.3 NTP 服务器设置（防火墙）</p></em>
        </p>
    5. 选择“新建规则...”
        * “新建入站规则向导”窗口打开
        1. 规则类型：端口
            <p align="center">
             <img src="../_assets/defender-setting-1.png"></img>
             <em><p align="center">图 2.4 NTP 服务器设置（防火墙）</p></em>
            </p>
        2. 协议和端口
            * UDP
            * 特定本地端口：123
            <p align="center">
             <img src="../_assets/defender-setting-2.png"></img>
             <em><p align="center">图 2.5 NTP 服务器设置（防火墙）</p></em>
            </p>
        3. 任务：允许连接
            <p align="center">
             <img src="../_assets/defender-setting-3.png"></img>
             <em><p align="center">图 2.6 NTP 服务器设置（防火墙）</p></em>
            </p>
        4. 配置文件：域、个人、公共
            <p align="center">
             <img src="../_assets/defender-setting-4.png"></img>
             <em><p align="center">图 2.7 NTP 服务器设置（防火墙）</p></em>
            </p>
        5. 名称：写一个名称和描述（可选）
            <p align="center">
             <img src="../_assets/defender-setting-5.png"></img>
             <em><p align="center">图 2.8 NTP 服务器设置（防火墙）</p></em>
            </p>
        6. 完成
[__SOURCE](3-use-ntp-client/README.md)
# 3. 执行 NTP 时间同步

描述如何在教学挂件中设置 NTP 时间同步并立即执行。
[__SOURCE](3-use-ntp-client/1-setting.md)
# 3.1 设置

1. 触摸菜单 `[F2: 系统] - 2: 控制参数 - 9: 网络 - 2: 服务 - 3: NTP 客户端 ([F2: system] - 2: Control parameters - 9: Network - 2: Service - 3: NTP client)`

2. 设置 NTP 时间同步所需的每个参数。

3. 您可以通过触摸“立即执行”按钮进行 NTP 时间同步。

* 是否使用 NTP 客户端 : '禁用'
<p align="center">
 <img src="../_assets/ntp-client-disable.png"></img>
 <em><p align="center">图 3.1 NTP 客户端屏幕（禁用）</p></em>
</p>

* 是否使用 NTP 客户端 : '启用'
<p align="center">
 <img src="../_assets/ntp-client-enable.png"></img>
 <em><p align="center">图 3.2 NTP 客户端屏幕（启用）</p></em>
</p>

<table>
 <thead>
  <tr>
   <th style="text-align:left">编号</th>
   <th stype="text-align:left">描述</th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td style="text-align:left">
    <img src="../_assets/n1.png" alt/>
   </td>
   <td style="text-align:left">
    当选择“禁用”作为是否使用 NTP 客户端时，将显示此屏幕。
   </td>
  </tr>
  <tr>
   <td style="text-align:left">
    <img src="../_assets/n2.png" alt/>
   </td>
   <td style="text-align:left">
    当选择“启用”作为是否使用 NTP 客户端时，将显示此屏幕。
   </td>
  </tr>
  <tr>
   <td style="text-align:left">
    <img src="../_assets/n3.png" alt/>
   </td>
   <td style="text-align:left">
    设置 NTP 时间同步的值。
     <li><b>NTP 服务器 IP 地址 : </b>输入 NTP 服务器的 IP 地址（IPv4）。</li>
     <li><b>NTP 端口号 : </b>输入 NTP 使用的端口号。NTP 使用端口 123 作为标准端口。</li>
     <li><b>时区偏移 : </b>输入当前地点的时区偏移。</li>
     <li><b>更新时间间隔 : </b>输入定期时间同步的小时更新时间间隔。如果您不想进行定期时间同步，请输入 0。</li>
     <li><b>剩余时间 : </b>显示到下次时间同步的剩余时间（以秒为单位）。</li>
   </td>
  </tr>
  <tr>
   <td style="text-align:left">
    <img src="../_assets/n4.png" alt/>
   </td>
   <td style="text-align:left">
    执行 NTP 时间同步
   </td>
  </tr>
  <tr>
   <td style="text-align:left">
    <img src="../_assets/n5.png" alt/>
   </td>
   <td style="text-align:left">
    保存设置。要应用更改的 NTP 时间同步设置，请触摸“立即执行”按钮。
   </td>
  </tr>
 </tbody>
</table>
[__SOURCE](3-use-ntp-client/2-execution.md)
# 3.2 立即执行

触摸“立即执行”按钮以执行 NTP 时间同步。

如果您使用端口号 123 以外的其他端口号作为 NTP 端口号，将出现如下所示的消息框。触摸“输入”以对该端口执行 NTP 时间同步，否则触摸“取消”。

<p align="center">
 <img src="../_assets/ntp-change-port-no.png"></img>
 <em><p align="center">图 3.3 使用除 123 以外的值作为 NTP 端口号</p></em>
</p>

根据执行 NTP 时间同步的结果，将出现如下所示的消息框。

<p align="center">
 <img src="../_assets/ntp-complete.png"></img>
 <em><p align="center">图 3.4 NTP 时间同步的结果（成功）</p></em>
</p>

NTP 时间同步成功完成。

<p align="center">
 <img src="../_assets/ntp-fail.png"></img>
 <em><p align="center">图 3.5 NTP 时间同步的结果（失败）</p></em>
</p>

NTP 时间同步失败。

{% hint style="info" %}
* 请小心不要输入在其他地方正在使用的端口号作为 NTP 端口号。我们建议使用 NTP 标准端口 123。
{% endhint %}