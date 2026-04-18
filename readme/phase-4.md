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
* 해당 id에 해당하는 좌표값을 변수 분류 좌표 목록 에서 가져와 각 x,y,z값에 저장 시킵니다.
* 분류하는 위치로 가 물체를 놓고 HOME의 x,y좌표로  안전하게 이동합니다.

***

## 블럭별 설명

### 각 집기(x,y,z)좌표에 해당하는 좌표 할당&#x20;

* 이 집기 좌표 목록에서 i번째 에 해당하는 좌표를 각 (x,y,z) 좌표에 할당합니다.

### 물체 집어 올리기&#x20;

<div align="left"><figure><img src="../.gitbook/assets/image (32).png" alt=""><figcaption></figcaption></figure></div>

<div align="left"><figure><img src="../.gitbook/assets/image (24).png" alt=""><figcaption></figcaption></figure></div>

* 물체를 집으러 가기전 물체의 좌표에 x,y좌표를 맞춥니다. (바로 물체를 집으러 가면 로봇이 물체를 쳐, 물체가 안전하지 않을 수 있습니다.)
* z좌표를 내려 물체에 맞춘 후 석션 모듈을 켜서 물체를 잡고, 다시 z좌표를 올려 물체를 이동시키기 위한 준비를 합니다.

### 컨베이어에 물체 내려놓기

<div align="left"><figure><img src="../.gitbook/assets/image (25).png" alt=""><figcaption></figcaption></figure></div>

* 물체를 컨베이어\_대기 -> 컨베이어\_놓기 좌표로 이동하여 석션을 끄고 다시 컨베이어\_대기 위치로 이동합니다.

### 컨베이어 움직이기&#x20;

<div align="left"><figure><img src="../.gitbook/assets/image (26).png" alt=""><figcaption></figcaption></figure></div>

* 컨베이어를 43만큼 이동시킵니다.

***
