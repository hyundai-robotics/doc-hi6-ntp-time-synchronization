# Hi6 로봇제어기 기능설명서 - NTP 클라이언트 시간 동기화

{% hint style="warning" %}
본 제품 설명서에서 제공되는 정보는 HD현대로보틱스의 자산입니다.

HD현대로보틱스의 서면에 의한 동의 없이 전부 또는 일부를 무단 전재 및 재배포할 수 없으며, 제3자에게 제공되거나 다른 목적에 사용할 수 없습니다.



본 설명서는 사전 예고 없이 변경될 수 있습니다.



**Copyright ⓒ 2024 by HD Hyundai Robotics**
{% endhint %}

# 1. 개요

{% hint style="info" %}
이 기능은 V60.30-00 및 이후 버전부터 지원됩니다.
{% endhint %}

# 1.1 NTP 시간 동기화란?

NTP(Network Time Protocol)는 네트워크의 모든 디바이스에서 시간을 동기화하는 데 사용되는 프로토콜입니다. 기본적으로 UDP의 123번 포트를 사용합니다.

<p align="center">
 <img src="../_assets/ntp-structure.png"></img>
 <em><p align="center">그림 1.1 Hi6 로봇제어기에서 NTP 시간 동기화</p></em>
</p>

---

NTP의 정의는 [RFC 5905: Network Time Protocol Version 4: Protocol and Algorithm Specification](https://datatracker.ietf.org/doc/html/rfc5905)에서 확인할 수 있습니다.

# 1.2 요구사항

NTP 클라이언트 시간 동기화 기능을 사용하기 위해서는 Hi6 로봇제어기와 LAN으로 직접 연결 가능한 NTP 서버가 필요합니다.

호스트 PC를 NTP 서버로 사용하기 위한 방법은 다음 장의 '[2. NTP 서버 설정](../2-ntp-server-setting/README.md)'을 참고하십시오.

# 2. NTP 서버 설정

Hi6 로봇제어기에 연결하는 호스트 PC를 NTP 서버로 사용하는 방법을 설명합니다.

# 2.1 윈도우 PC를 NTP 서버로 설정

윈도우 PC(Windows 10)를 NTP 서버로 사용하기 위해서는 아래의 단계를 수행해야 합니다.

1. Windows에서 NTP 서버 기능 활성화
    * w32time(Windows Time Service) 사용
    1. '레지스트리 편집기' 열기
    2. 'HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\W32Time\Config' 경로로 이동
        * 'AnnounceFlags' 항목의 값을 5(NTP 서버)로 설정 - 기본값은 10일 수 있음
        <p align="center">
         <img src="../_assets/reg-announceflags.png"></img>
         <em><p align="center">그림 2.1 NTP 서버 설정(레지스트리 편집기)</p></em>
        </p>
    3. 'HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\W32Time\TimeProviders\NtpServer' 경로로 이동
        * 'Enabled' 항목의 값을 1(활성화)로 설정
        <p align="center">
         <img src="../_assets/reg-enabled.png"></img>
         <em><p align="center">그림 2.2 NTP 서버 설정(레지스트리 편집기)</p></em>
        </p>
2. Windows Time 서비스 재시작
    * '명령 프롬프트'에서 관리자 권한으로 다음 명령을 입력
    ```
        net stop w32time
        net start w32time
    ```
3. Windows 방화벽 설정
    * NTP는 기본적으로 UDP 123번 포트를 사용. 따라서 NTP 서버 역할을 하려면 해당 포트가 열려 있어야 함
    1. '제어판' 열기
    2. 'Windows Defender 방화벽' 선택
    3. '고급 설정' 선택
    4. '로컬 컴퓨터의 고급 보안이 포함된 Windows Defender 방화벽'의 '인바운드 규칙' 선택
        <p align="center">
         <img src="../_assets/defender.png"></img>
         <em><p align="center">그림 2.3 NTP 서버 설정(방화벽)</p></em>
        </p>
    5. '새 규칙...' 선택
        * '새 인바운드 규칙 마법사' 창이 열림
        1. 규칙 종류: 포트(O)
            <p align="center">
             <img src="../_assets/defender-setting-1.png"></img>
             <em><p align="center">그림 2.4 NTP 서버 설정(방화벽)</p></em>
            </p>
        2. 프로토콜 및 포트
            * UDP(U)
            * 특정 로컬 포트(S): 123
            <p align="center">
             <img src="../_assets/defender-setting-2.png"></img>
             <em><p align="center">그림 2.5 NTP 서버 설정(방화벽)</p></em>
            </p>
        3. 작업: 연결 허용(A)
            <p align="center">
             <img src="../_assets/defender-setting-3.png"></img>
             <em><p align="center">그림 2.6 NTP 서버 설정(방화벽)</p></em>
            </p>
        4. 프로필: 도메인(D), 개인(P), 공용(U)
            <p align="center">
             <img src="../_assets/defender-setting-4.png"></img>
             <em><p align="center">그림 2.7 NTP 서버 설정(방화벽)</p></em>
            </p>
        5. 이름: 이름(N)과 설명(옵션)(D) 작성
            <p align="center">
             <img src="../_assets/defender-setting-5.png"></img>
             <em><p align="center">그림 2.8 NTP 서버 설정(방화벽)</p></em>
            </p>
        6. 마침(F)

# 3. NTP 시간 동기화 실행

티치 펜던트에서 NTP 시간 동기화 설정 방법과 지금 실행에 대하여 설명합니다.

# 3.1 설정

1. \[시스템 &gt; 2: 제어 파라미터 &gt; 9: 네트워크 &gt; 2: 서비스 &gt; 3: NTP 클라이언트\] 메뉴를 터치하십시오.

2. NTP 시간 동기화에 필요한 각 파라미터를 설정합니다.

3. '지금 실행' 버튼을 터치해 NTP 시간 동기화를 수행할 수 있습니다.

* NTP 클라이언트 사용 여부 : '무효'
<p align="center">
 <img src="../_assets/ntp-client-disable.png"></img>
 <em><p align="center">그림 3.1 NTP 클라이언트 화면(무효)</p></em>
</p>

* NTP 클라이언트 사용 여부 : '유효'
<p align="center">
 <img src="../_assets/ntp-client-enable.png"></img>
 <em><p align="center">그림 3.2 NTP 클라이언트 화면(유효)</p></em>
</p>

<table>
 <thead>
  <tr>
   <th style="text-align:left">번호</th>
   <th stype="text-align:left">설명</th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td style="text-align:left">
    <img src="../_assets/n1.png" alt/>
   </td>
   <td style="text-align:left">
    NTP 클라이언트 사용 여부로 '무효'를 선택했을 때 화면입니다.
   </td>
  </tr>
  <tr>
   <td style="text-align:left">
    <img src="../_assets/n2.png" alt/>
   </td>
   <td style="text-align:left">
    NTP 클라이언트 사용 여부로 '유효'를 선택했을 때 화면입니다.
   </td>
  </tr>
  <tr>
   <td style="text-align:left">
    <img src="../_assets/n3.png" alt/>
   </td>
   <td style="text-align:left">
    NTP 시간 동기화를 위한 값을 설정합니다.
     <li><b>NTP 서버 주소 : </b>NTP 서버의 IP 주소(IPv4)를 입력하십시오.</li>
     <li><b>NTP 포트 번호 : </b>NTP에서 사용할 포트 번호를 입력하십시오. NTP는 표준 포트로 123번 포트를 사용합니다.</li>
     <li><b>타임존 오프셋 : </b>현재 지역의 타임존 오프셋을 입력하십시오.</li>
     <li><b>갱신 간격 : </b>주기적인 시간 동기화를 위한 갱신 간격을 시(hour) 단위로 입력하십시오. 주기적인 시간 동기화를 수행하고 싶지 않은 경우, 0을 입력하십시오.</li>
     <li><b>남은 시간 : </b>다음 시간 동기화까지 남은 시간을 초(sec) 단위로 보여줍니다.</li>
   </td>
  </tr>
  <tr>
   <td style="text-align:left">
    <img src="../_assets/n4.png" alt/>
   </td>
   <td style="text-align:left">
    NTP 시간 동기화를 수행합니다.
   </td>
  </tr>
  <tr>
   <td style="text-align:left">
    <img src="../_assets/n5.png" alt/>
   </td>
   <td style="text-align:left">
    설정을 저장합니다. NTP 시간 동기화에 변경된 설정값을 적용하기 위해서는 '지금 실행' 버튼을 터치하십시오.
   </td>
  </tr>
 </tbody>
</table>

# 3.2 지금 실행

'지금 실행' 버튼을 터치해 NTP 시간 동기화를 수행합니다.

NTP 포트 번호로 123번이 아닌 다른 포트 번호를 사용하는 경우, 아래 그림과 같은 메시지 박스가 나타납니다. 해당 포트로 NTP 시간 동기화를 수행하려면 '확인'을 터치하시고, 그렇지 않다면 '취소'를 터치하십시오.

<p align="center">
 <img src="../_assets/ntp-change-port-no.png"></img>
 <em><p align="center">그림 3.3 NTP 포트 번호로 123번 이외의 값을 사용</p></em>
</p>

NTP 시간 동기화 수행 결과에 따라 아래 그림과 같은 메시지 박스가 나타납니다.

<p align="center">
 <img src="../_assets/ntp-complete.png"></img>
 <em><p align="center">그림 3.4 NTP 시간 동기화 수행 결과(성공)</p></em>
</p>

NTP 시간 동기화가 성공적으로 수행되었습니다.

<p align="center">
 <img src="../_assets/ntp-fail.png"></img>
 <em><p align="center">그림 3.5 NTP 시간 동기화 수행 결과(실패)</p></em>
</p>

NTP 시간 동기화에 실패하였습니다.

{% hint style="info" %}
* NTP 포트 번호로 다른 곳에서 사용 중인 포트 번호를 입력하지 않도록 주의하십시오. NTP 표준 포트인 123번을 사용하는 것을 권장합니다.
{% endhint %}

