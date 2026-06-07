
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
此功能在 V60.30-00 及更高版本中支持。
{% endhint %}
[__SOURCE](1-overview/1-description.md)
# 1.1 什么是NTP时间同步？

NTP（网络时间协议）是一种用于同步网络中所有设备时间的协议。默认情况下，使用UDP端口123。

<p align="center">
 <img src="../_assets/ntp-structure.png"></img>
 <em><p align="center">图1.1 ${cont_model}机器人控制器上的NTP时间同步</p></em>
</p>

---

NTP的定义可以在 [RFC 5905: 网络时间协议第4版：协议和算法规范](https://datatracker.ietf.org/doc/html/rfc5905) 中找到。
[__SOURCE](1-overview/2-requirement.md)
# 1.2 需求

要使用NTP客户端时间同步功能，您需要一个可以通过LAN直接连接到${cont_model}机器人控制器的NTP服务器。

有关如何将您的主机PC用作NTP服务器的信息，请参阅下一章节中的 '[2.NTP服务器设置](../2-ntp-server-setting/README.md)'。
[__SOURCE](2-ntp-server-setting/README.md)
# 2. NTP 服务器设置

描述如何将连接到 ${cont_model} 机器人控制器的主机 PC 用作 NTP 服务器。
[__SOURCE](2-ntp-server-setting/1-window-pc.md)
# 2.1 将 Windows PC 设置为 NTP 服务器

要将 Windows PC（Windows 10）用作 NTP 服务器，必须遵循以下步骤。

1. 在 Windows 中启用 NTP 服务器功能。
    * 使用 w32time（Windows 时间服务）
    1. 打开“注册表编辑器”
    2. 转到路径 'HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\W32Time\Config'
        * 将 'AnnounceFlags' 条目的值设置为 5（NTP 服务器） - 默认值可能是 10
        <p align="center">
         <img src="../_assets/reg-announceflags.png"></img>
         <em><p align="center">图 2.1 NTP 服务器设置（注册表编辑器）</p></em>
        </p>
    3. 转到路径 'HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\W32Time\TimeProviders\NtpServer'
        * 将 'Enabled' 条目的值设置为 1（启用）
        <p align="center">
         <img src="../_assets/reg-enabled.png"></img>
         <em><p align="center">图 2.2 NTP 服务器设置（注册表编辑器）</p></em>
        </p>
2. 重启 Windows 时间服务
    * 在“命令提示符”中，以管理员权限输入以下命令。
    ```
        net stop w32time
        net start w32time
    ```
3. Windows 防火墙设置
    * NTP 默认使用 UDP 端口 123。因此，该端口必须打开以充当 NTP 服务器
    1. 打开“控制面板”
    2. 选择“Windows Defender 防火墙”
    3. 选择“高级设置”
    4. 在“Windows Defender 防火墙与高级安全”中选择“入站规则”
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
        4. 配置文件：域、个人、公用
            <p align="center">
             <img src="../_assets/defender-setting-4.png"></img>
             <em><p align="center">图 2.7 NTP 服务器设置（防火墙）</p></em>
            </p>
        5. 名称：输入名称和描述（可选）
            <p align="center">
             <img src="../_assets/defender-setting-5.png"></img>
             <em><p align="center">图 2.8 NTP 服务器设置（防火墙）</p></em>
            </p>
        6. 完成
[__SOURCE](3-use-ntp-client/README.md)
# 3. 执行NTP时间同步

描述如何在教导挂件中设置NTP时间同步并立即执行。
[__SOURCE](3-use-ntp-client/1-setting.md)
# 3.1 设置

1. 点击菜单 \[system &gt; 2: 控制参数 &gt; 9: 网络 &gt; 2: 服务 &gt; 3: NTP 客户端\]

2. 设置 NTP 时间同步所需的每个参数。

3. 您可以通过点击“立即执行”按钮来执行 NTP 时间同步。

* 是否使用 NTP 客户端 : '禁用'
<p align="center">
 <img src="../_assets/ntp-client-disable.png"></img>
 <em><p align="center">图 3.1 NTP 客户端屏幕(禁用)</p></em>
</p>

* 是否使用 NTP 客户端 : '启用'
<p align="center">
 <img src="../_assets/ntp-client-enable.png"></img>
 <em><p align="center">图 3.2 NTP 客户端屏幕(启用)</p></em>
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
    当选择“禁用”作为是否使用 NTP 客户端时，显示此屏幕。
   </td>
  </tr>
  <tr>
   <td style="text-align:left">
    <img src="../_assets/n2.png" alt/>
   </td>
   <td style="text-align:left">
    当选择“启用”作为是否使用 NTP 客户端时，显示此屏幕。
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
<li><b>更新时间间隔 : </b>输入定期时间同步的更新时间间隔（以小时为单位）。如果您不想执行定期时间同步，请输入 0。</li>
<li><b>剩余时间 : </b>显示下次时间同步前剩余的时间（以秒为单位）。</li>
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

点击“立即执行”按钮以进行NTP时间同步。

如果您使用的NTP端口号不是123，将会出现如下所示的消息框。点击“确定”以对该端口进行NTP时间同步，否则点击“取消”。

<p align="center">
 <img src="../_assets/ntp-change-port-no.png"></img>
 <em><p align="center">图3.3 使用123以外的值作为NTP端口号</p></em>
</p>

根据执行NTP时间同步的结果，将会出现如下所示的消息框。

<p align="center">
 <img src="../_assets/ntp-complete.png"></img>
 <em><p align="center">图3.4 NTP时间同步结果（成功）</p></em>
</p>

NTP时间同步成功完成。

<p align="center">
 <img src="../_assets/ntp-fail.png"></img>
 <em><p align="center">图3.5 NTP时间同步结果（失败）</p></em>
</p>

NTP时间同步失败。

{% hint style="info" %}
* 请注意不要输入正在其他地方使用的端口号作为NTP端口号。我们建议使用NTP标准端口123。
{% endhint %}