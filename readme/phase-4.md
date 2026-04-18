# Phase 4: 물체 분류

## 개요

물체를 인식하고 분류하는 단계입니다.

***

## Phase 4. 전체 블럭 설명&#x20;

{% hint style="info" %}
석션 켜기/끄기 후 완전히 흡착/놓을 수 있도록 약간 기다려 주는게 좋습니다.
{% endhint %}

<figure><img src="../.gitbook/assets/image (31).png" alt=""><figcaption></figcaption></figure>

* 물체가 인식 될 때 까지 스캔합니다.&#x20;
* 물체가 인식되면 변수 result에 그 물체의 중심 (x,y)좌표, 해당 물체의 id값을 리스트로 반환합니다.
* 변수 : 변환 좌표 리스트에 result에서 반환된 (x,y)좌표를 실제 로봇이 움직일 좌표로 변환해 리스트로 저장합니다.&#x20;
* 변환 좌표 리스트에 저장된 x, y값을 각각 변수: 변환 x좌표, 변환 y좌표 에 저장합니다.
* 해당 x,y좌표와 기본 z좌표로 이동한 후, z좌표를 물체의 위치에 맞춰 해당 물체를 집어올린 후, 다시 z좌표를 올려 이동할 준비를 합니다.
* result에 저장되어 있던 해당 물체의 id값을 변수 tag\_id 에 저장시킵니다.
* 해당 id에 해당하는 좌표값을 변수 분류 좌표 목록 에서 가져와 각 x,y,z값에 저장시킵니다.
* 현재 물체를 분류하는 위치로 가서 물체를 놓고 HOME의 x,y좌표로  안전하게 이동합니다.

***

## 블럭별 설명

### 물체 인식&#x20;

<div align="left"><figure><img src="../.gitbook/assets/image (33).png" alt=""><figcaption></figcaption></figure></div>

* 물체가 인식 될 때 까지 스캔합니다.&#x20;
* 물체가 인식되면 변수 result에 그 물체의 중심 (x,y)좌표, 해당 물체의 id값을 리스트로 반환합니다.

{% hint style="info" %}
속도를 선택하면 빠르게 인식되는 반면, 정확도를 선택하면 속도는 느리지만 현재 물체가 해당하는 위치를 더 정확하게 인식할 수 있습니다.
{% endhint %}



### 인식한 물체를 실제 좌표로 변환하기&#x20;

<div align="left"><figure><img src="../.gitbook/assets/image (32).png" alt=""><figcaption></figcaption></figure></div>

* 변수 : 변환 좌표 리스트에 result에서 반환된 (x,y)좌표를 실제 로봇이 움직일 좌표로 변환해 리스트로 저장합니다.&#x20;
* 실좌표로 변환 블럭은 왼쪽에는 카메라에서의 좌표(2차원 좌표), 오른쪽에는 물체의 높이를 넣습니다.&#x20;
* 실좌표로 변환 블럭에서는 물체가 카메라의 가운데에 올 때 까지 움직이다 카메라의 가운데에 물체가 포착되면 해당 좌표(3차원 좌표: 로봇이 움직이는 좌표)중 x,y좌표를 리스트로 반환합니다.
* 변환 좌표 리스트에 저장된 x, y값을 각각 변수: 변환 x좌표, 변환 y좌표 에 저장합니다.

### 컨베이어에서 로봇 집기&#x20;

<div align="left"><figure><img src="../.gitbook/assets/image (34).png" alt=""><figcaption></figcaption></figure></div>

* 컨베이어해당 x,y좌표와 기본 z좌표로 이동한 후, z좌표를 물체의 위치에 맞춰 해당 물체를 집어올린 후, 다시 z좌표를 올려 이동할 준비를 합니다.

### 현재 물체에 해당하는 위치로 좌표값 설정

<div align="left"><figure><img src="../.gitbook/assets/image (35).png" alt=""><figcaption></figcaption></figure></div>

* result에 저장되어 있던 해당 물체의 id값을 변수 tag\_id 에 저장시킵니다.
* 해당 id에 해당하는 좌표값을 변수 분류 좌표 목록 에서 가져와 각 x,y,z값에 저장시킵니다.

{% hint style="info" %}
리스트는 0번부터 시작, AI카메라로 인식한 태그의 id는 1번부터 시작하기 때문에 둘의 번호를 맞추고 싶다면 id에서 1을 빼줘야 합니다.
{% endhint %}

### 물체 분류&#x20;

<div align="left"><figure><img src="../.gitbook/assets/image (37).png" alt=""><figcaption></figcaption></figure></div>

* 현재 물체를 분류하는 위치로 가서 물체를 놓고 HOME의 x,y좌표로  안전하게 이동합니다.

***

## Phase 4 실행 영상

{% embed url="https://youtu.be/ifZQ_IuMOkY" %}

***
