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

