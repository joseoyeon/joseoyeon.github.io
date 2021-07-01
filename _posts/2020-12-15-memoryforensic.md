---
layout: post
title:  "Forensic 변조된 데이터를 확인하는 방법"
date:   2020-12-15 22:10:43
categories: [All, others, Forensic]
---

**[1]** 논문에서 말하는 Known 데이터 요약 정리

일단 논문의 내용은 Window 커널 속성 정보는 Window 버전마다 상이한데 기본 구조는 유사하나 중간에 데이터가 몇개 더 끼워 들어가면 offset 이 완전히 달라진다.(밀린다) 해당 논문의 연구결과 커널 글로벌 오프셋은 버전마다 다르므로 이걸로 커널 버전을 감지하고 커널 버전에 맞는 프로파일 정보를 불러와 라이브 포렌식이 가능하도록 한다. 

### 메모리 포렌식 도구의 커널 버전 및 컨널 오프젝트 식별 방식

#### 볼리빌리티
1. 역공학 분석을 통한 오프셋 하드 코딩 (PDB 파일 공개전)
2. kdDebuggerDataBlock 이용
3. Pool Tag 또는 Singature 스캐닝 (String 기반)
4. Export Table, Exproted function call 조사 

##### Rekall
1. profile : PDB파일(디버깅 심볼 파일) + Known Offset(역공학으로 분석되어 있거나 문서에 공개된 정보)
2. Profile을 이용한커널 오프젝트 식별
3. GUID를 이용한 커널 버전 식별
        - GUID는 RSDS Region 에 저장됨
        - GUID를 찾을 때 RSDS Region의 Signature인 "RSDS" Scanning 

PDB 파일에는 메모리 분석 프레임워크, 즉 구조 구성원과 메모리 레이아웃에 대한 유용한 정보가 다수 포함되어 있다. 

- **구조 구성원과 메모리 레이아웃** : 여기에는 구조체 구성원에 대한 메모리 오프셋과 그 유형에 대한 정보가 포함되어 있다. 이것은 기억의 내용을 해석하는 데 유용하다.

- **전역 상수** : 윈도우즈 커널에는 분석에 필요한 많은 중요한 상수가 포함되어 있다. 예를 들어 PsActiveProcess헤드는 프로세스 연결 목록의 시작 부분에 대한 일정한 포인터로, 해당 목록을 걸어 프로세스를 나열하는 데 필요하다.

- **함수 주소** : 메모리에 있는 기능의 위치 또한 PDB 파일 e에 제공된다. 이것은 주소를 다시 함수로 해결하기 위해 중요하다(예: 인터럽트 설명자 테이블 e IDT 보기).

- **열거** :  C에서 열거는 정수를 사용하여 선택사항 집합 중 하나를 나타내는 압축적인 방법이다. 정수 값과 인간의 의미 있는 문자열 사이의 매핑은 PDB 파일에 저장되며, 메모리에서 의미를 해석하는 데 유용하다.

#### 커널 버전 가변성 특성 지정



---

**[Reference]**

**[1]**  Cohen, M. I. (2015). Characterization of the windows kernel version variability for accurate memory analysis. Digital Investigation, 12, S38-S49.


