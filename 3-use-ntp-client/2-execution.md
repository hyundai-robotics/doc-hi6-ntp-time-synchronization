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

