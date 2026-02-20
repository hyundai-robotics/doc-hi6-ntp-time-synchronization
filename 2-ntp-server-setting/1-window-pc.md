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