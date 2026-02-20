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