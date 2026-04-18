# Phase 2: 컨베이어 이동

## 개요

물체를 집어 컨베이어에 올리고 컨베이어를 동작시키는 단계입니다.

***

## Phase 2. 전체 블럭 설명&#x20;

{% hint style="info" %}
석션 켜기/끄기 후 완전히 흡착/놓을 수 있도록 약간 기다려 주는게 좋습니다.
{% endhint %}

<figure><img src="../.gitbook/assets/image (22).png" alt=""><figcaption></figcaption></figure>



* 집기 좌표 목록에서 i번째 에 해당하는 좌표를 각 (x,y,z) 좌표에 할당합니다.
* 물체를 집으러 가기전 물체의 좌표에 x,y좌표를 맞춥니다. (바로 물체를 집으러 가면 로봇이 물체를 쳐서, 물체가 안전하지 않을 수 있습니다.)
* z좌표를 내려 물체에 맞춘 후 석션 모듈을 켜서 물체를 잡고, 다시 z좌표를 올려 물체를 이동시키기 위한 준비를 합니다.
* 물체를 컨베이어\_대기 -> 컨베이어\_놓기 좌표로 이동하여 석션을 끄고 다시 컨베이어\_대기 위치로 이동한 후, 컨베이어를 움직입니다.

***

## 블럭별 설명

### 각 집기(x,y,z)좌표에 해당하는 좌표 할

<div align="left"><figure><img src="../.gitbook/assets/image (23).png" alt=""><figcaption></figcaption></figure></div>

* 이 집기 좌표 목록에서 i번째 에 해당하는 좌표를 각 (x,y,z) 좌표에 할당합니다.

### 물체 집어 올리

<div align="left"><figure><img src="../.gitbook/assets/image (24).png" alt=""><figcaption></figcaption></figure></div>

* 물체를 집으러 가기전 물체의 좌표에 x,y좌표를 맞춥니다. (바로 물체를 집으러 가면 로봇이 물체를 쳐, 물체가 안전하지 않을 수 있습니다.)
* z좌표를 내려 물체에 맞춘 후 석션 모듈을 켜서 물체를 잡고, 다시 z좌표를 올려 물체를 이동시키기 위한 준비를 합니다.

### 컨베이어에 물체 내려놓

<div align="left"><figure><img src="../.gitbook/assets/image (25).png" alt=""><figcaption></figcaption></figure></div>

* 물체를 컨베이어\_대기 -> 컨베이어\_놓기 좌표로 이동하여 석션을 끄고 다시 컨베이어\_대기 위치로 이동합니다.

### 컨베이어 움직이기

<div align="left"><figure><img src="../.gitbook/assets/image (26).png" alt=""><figcaption></figcaption></figure></div>

* 컨베이어를 43만큼 이동시킵니다.

***
