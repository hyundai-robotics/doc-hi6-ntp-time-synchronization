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