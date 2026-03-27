
[__SOURCE](README.md)
# ${cont_model} Controller Function Manual - NTP client time synchronization

[__SOURCE](0-about-this-manual/precautions.md)
# Precautions

{% include url="https://hrcontentsrelay-bmgae5hdbzapc4bc.koreacentral-01.azurewebsites.net/api/proxy?path=doc-common-pages/en/precautions.md" %}

[__SOURCE](1-overview/README.md)
# 1. Overview

{% hint style="info" %}
This feature is supported in V60.30-00 and later versions.
{% endhint %}


[__SOURCE](1-overview/1-description.md)
# 1.1 What is NTP time synchronization?

NTP(Network Time Protocol) is a protocol used to synchronize time across all devices in the network. By default, UDP port 123 is used.

<p align="center">
 <img src="../_assets/ntp-structure.png"></img>
 <em><p align="center">Figure 1.1 NTP time synchronization on ${cont_model} robot controller</p></em>
</p>

---

The definition of NTP can be found in [RFC 5905: Network Time Protocol Version 4: Protocol and Algorithm Specification](https://datatracker.ietf.org/doc/html/rfc5905).


[__SOURCE](1-overview/2-requirement.md)
# 1.2 Requirement

To use the NTP client time synchronization feature, you need an NTP server that can be directly connected to the ${cont_model} robot controller by LAN.

For information on how to use your host PC as an NTP server, see '[2.NTP server setting](../2-ntp-server-setting/README.md)' in the next chapter.


[__SOURCE](2-ntp-server-setting/README.md)
# 2. NTP server setting

Describes how to use the host PC that connects to the ${cont_model} robot controller as an NTP server.


[__SOURCE](2-ntp-server-setting/1-window-pc.md)
# 2.1 Set Windows PC as an NTP server

To use a Windows PC(Windows 10) as an NTP server, you must follow the steps below.

1. Enable NTP server feature in Windows.
    * Use w32time(Windows Time Service)
    1. Open 'Registry Editor'
    2. Go to the path 'HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\W32Time\Config'
        * Set the value of the 'AnnounceFlags' entry to 5(NTP server) - default may be 10
        <p align="center">
         <img src="../_assets/reg-announceflags.png"></img>
         <em><p align="center">Figure 2.1 NTP Server Setting(Registry Editor)</p></em>
        </p>
    3. Go to the path 'HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\W32Time\TimeProviders\NtpServer'
        * Set the value of 'Enabled' entry to 1(enabled)
        <p align="center">
         <img src="../_assets/reg-enabled.png"></img>
         <em><p align="center">Figure 2.2 NTP Server Setting(Registry Editor)</p></em>
        </p>
2. Restart the Windows Time service
    * In 'Command Prompt', enter the following command with administrator privileges.
    ```
        net stop w32time
        net start w32time
    ```
3. Windows Firewall setting
    * NTP uses UDP port 123 by default. Therefore, the port must be open to act as an NTP server
    1. Open 'Control Panel'
    2. Select 'Windows Defender Firewall'
    3. Select 'Advanced Settings'
    4. Select 'Inbound Rules' in 'Windows Defender Firewall with Advanced Security'
        <p align="center">
         <img src="../_assets/defender.png"></img>
         <em><p align="center">Figure 2.3 NTP Server Settings(Firewall)</p></em>
        </p>
    5. Select 'New Rule...'
        * The 'New Inbound Rule Wizard' window opens
        1. Rule Type: Port
            <p align="center">
             <img src="../_assets/defender-setting-1.png"></img>
             <em><p align="center">Figure 2.4 NTP Server Settings(Firewall)</p></em>
            </p>
        2. Protocol and Port
            * UDP
            * Specific local ports: 123
            <p align="center">
             <img src="../_assets/defender-setting-2.png"></img>
             <em><p align="center">Figure 2.5 NTP Server Settings(Firewall)</p></em>
            </p>
        3. Task: Allow connection
            <p align="center">
             <img src="../_assets/defender-setting-3.png"></img>
             <em><p align="center">Figure 2.6 NTP Server Settings(Firewall)</p></em>
            </p>
        4. Profile: Domain, Personal, Public
            <p align="center">
             <img src="../_assets/defender-setting-4.png"></img>
             <em><p align="center">Figure 2.7 NTP Server Settings(Firewall)</p></em>
            </p>
        5. Name: Write a name and description (optional)
            <p align="center">
             <img src="../_assets/defender-setting-5.png"></img>
             <em><p align="center">Figure 2.8 NTP Server Settings(Firewall)</p></em>
            </p>
        6. Finish


[__SOURCE](3-use-ntp-client/README.md)
# 3. Execute NTP time synchronization

Describes how to set up NTP time synchronization in the Teach Pendant and Execute now.


[__SOURCE](3-use-ntp-client/1-setting.md)
# 3.1 Setting

1. Touch the menu `[F2: system] - 2: Control parameters - 9: Network - 2: Service - 3: NTP client`

2. Sets each parameter required for NTP time synchronization.

3. You can perform NTP time synchronization by touching the 'Execute now' button.

* Whether to use NTP client : 'Disable'
<p align="center">
 <img src="../_assets/ntp-client-disable.png"></img>
 <em><p align="center">Figure 3.1 NTP Client Screen(Disable)</p></em>
</p>

* Whether to use NTP client : 'Enable'
<p align="center">
 <img src="../_assets/ntp-client-enable.png"></img>
 <em><p align="center">Figure 3.2 NTP Client Screen(Enable)</p></em>
</p>

<table>
 <thead>
  <tr>
   <th style="text-align:left">Number</th>
   <th stype="text-align:left">Description</th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td style="text-align:left">
    <img src="../_assets/n1.png" alt/>
   </td>
   <td style="text-align:left">
    This screen is displayed when 'Disable' is selected as whether to use the NTP client.
   </td>
  </tr>
  <tr>
   <td style="text-align:left">
    <img src="../_assets/n2.png" alt/>
   </td>
   <td style="text-align:left">
    This screen is displayed when 'Enable' is selected as whether to use the NTP client.
   </td>
  </tr>
  <tr>
   <td style="text-align:left">
    <img src="../_assets/n3.png" alt/>
   </td>
   <td style="text-align:left">
    Set values for NTP time synchronization.
     <li><b>NTP server IP Address : </b>Enter the IP address(IPv4) of the NTP server.</li>
     <li><b>NTP port number : </b>Enter the port number to be used by NTP. NTP uses port 123 as the standard port.</li>
     <li><b>Timezone offset : </b>Enter the time zone offset for the current location.</li>
     <li><b>Update interval : </b>Enter the update interval in hours for periodic time synchronization. If you do not want to perform periodic time synchronization, enter 0.</li>
     <li><b>Remaining time : </b>Shows the time remaining in seconds until the next time synchronization.</li>
   </td>
  </tr>
  <tr>
   <td style="text-align:left">
    <img src="../_assets/n4.png" alt/>
   </td>
   <td style="text-align:left">
    Execute NTP time synchronization
   </td>
  </tr>
  <tr>
   <td style="text-align:left">
    <img src="../_assets/n5.png" alt/>
   </td>
   <td style="text-align:left">
    Save settings. To apply the changed settings for NTP time synchronization, touch the 'Execute now' button.
   </td>
  </tr>
 </tbody>
</table>


[__SOURCE](3-use-ntp-client/2-execution.md)
# 3.2 Execute now

Touch the 'Execute now' button to perform NTP time synchronization.

If you use a port number other than 123 as the NTP port number, a message box as shown below will appear. Touch 'Enter' to perform NTP time synchronization to that port, otherwise touch 'Cancel'.

<p align="center">
 <img src="../_assets/ntp-change-port-no.png"></img>
 <em><p align="center">Figure 3.3 Use a value other than 123 as the NTP port number</p></em>
</p>

Depending on the results of executing NTP time synchronization, a message box as shown below will appear.

<p align="center">
 <img src="../_assets/ntp-complete.png"></img>
 <em><p align="center">Figure 3.4 Results of NTP Time Synchronization(Success)</p></em>
</p>

NTP time synchronization was performed successfully.

<p align="center">
 <img src="../_assets/ntp-fail.png"></img>
 <em><p align="center">Figure 3.5 Results of NTP Time Synchronization(Fail)</p></em>
</p>

NTP time synchronization failed.

{% hint style="info" %}
* Be careful not to enter a port number that is in use elsewhere as the NTP port number. We recommend using NTP standard port 123.
{% endhint %}

