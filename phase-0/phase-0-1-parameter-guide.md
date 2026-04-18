# 변수 상세 가이드

## 블록 다이어그램

<figure><img src="../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

***

## 로봇의 좌표 측정 방법

### 1. AI 카메라를 통한 측정

HUENIT OS의 세 번째 항목은 <mark style="background-color:purple;">\[티치 & 플레이]</mark>입니다.

<mark style="background-color:purple;">\[티치 & 플레이]</mark> 는 원하는 로봇의 동작을 직접 로봇에게 가르쳐주고, 제대로 동작하는지 확인할 수 있는 메뉴입니다.

<figure><img src="../.gitbook/assets/image (10).png" alt="" width="563"><figcaption><p>HUENIT OS - [로봇  조작]  > [티치 &#x26; 플레이]</p></figcaption></figure>

## 1. 기본 UI

\[티치 & 플레이] 항목을 선택하면 다음과 같은 메인화면이 나타납니다.&#x20;

초기에는 아무 동작도 저장되어 있지 않습니다.

<figure><img src="../.gitbook/assets/image (11).png" alt="" width="371"><figcaption><p>[티치 &#x26; 플레이] main화면</p></figcaption></figure>

## 2. 티치&플레이 사용방법

(1) \[추가] 버튼을 클릭하면, 원하는 로봇의 움직임을 저장할 수 있는 화면으로 이동합니다.

<figure><img src="../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

(2) <mark style="background-color:yellow;">\[모터 끄기]</mark> 버튼을 클릭하여 HUENIT 로봇팔의 모터를 모두 끕니다.

이후 <mark style="background-color:yellow;">\[모터 끄기]</mark> 버튼이 <mark style="background-color:yellow;">\[이동 추가]</mark> 버튼으로 바뀝니다. 모터가 꺼진 상태에서로봇팔을 원하는 위치로 이동시키고 <mark style="background-color:yellow;">\[이동 추가]</mark> 버튼을 클릭하면, 모터가다시 켜지면서 현재 로봇의 \[x, y, z] 좌표가 저장됩니다.

***

### 블록 2️⃣: 컨베이어 위치 파라미터 블록

**기능**: 컨베이어로 옮길 위치 2곳을 저장

* 대기 위치: 컨베이어 위쪽 안전 높이
* 놓기 위치: 물체를 실제로 떨어뜨리는 위치

**파라미터**:

* 컨베이어 대기: (230, 250, 80)
* 컨베이어 놓기: (230, 260, 22)

**주의사항**:

* 대기 위치의 Z(80)는 항상 놓기 위치의 Z(22)보다 높아야 충돌 없음

***

### 블록 3️⃣: 홈 위치 파라미터 블록

**기능**: 로봇이 대기하는 "홈" 좌표 저장

* 모든 사이클의 시작/종료 위치
* 다른 장비와 충돌하지 않는 안전한 지점

**파라미터**:

* HOME X: 280
* HOME Y: 0
* HOME 좌표: (280, 0, 0)

***

### 블록 4️⃣: 분류 위치 파라미터 블록

**기능**: 인식된 물체를 옮길 3개 위치 저장

* tag\_id(물체 종류)에 따라 선택
* X는 고정, Y는 3개 중 선택

**파라미터**:

* 분류 X 좌표: -270 (고정)
* 분류 Y 좌표 목록: \[80, 5, -70]
* 분류 Z 좌표: 0

**분류 규칙**:

* tag\_id = 1 → Y = 80
* tag\_id = 2 → Y = 5
* tag\_id = 3 → Y = -70

**주의사항**:

* 분류 위치 개수를 늘리면 Y 목록에 값을 추가해야 함
* 분류 위치끼리 서로 부딪히지 않게 간격 유지

***

**뒤로**: [Phase 0: 파라미터 설정](./)
