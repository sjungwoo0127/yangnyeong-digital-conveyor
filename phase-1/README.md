# Phase 1: 홈

## 개요

이후 동작을 진행하기 전 로봇 팔을 대기 위치(홈)으로 이동시키는 단계입니다.

***

## Phase 1. 전체 블럭 설명&#x20;

<figure><img src="../.gitbook/assets/image (2).png" alt="" width="563"><figcaption></figcaption></figure>

* 최초 실행에서 로봇이 HOME 좌표로 이동 후, 버튼을 누르지 않고 있는다면 계속 그 자리에 가만히 있습니다.
* 버튼을 누르면, phase2부터 4까지의 동작이 세 번 실행됩니다.
* 세번의 동작이 끝나면 다시 HOME 위치로 와, 다시 버튼 누르기를 기다립니다.

***

## 블럭별 설명

### 반복 블럭

<div align="left"><figure><img src="../.gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure></div>

* 이 블럭은 안에 있는 코드들을 무한 반복하는 블럭입니다.

### 로봇 움직이기

<div align="left"><figure><img src="../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure></div>

* 이 블럭은 로봇의 위치를 변수 HOME에 저장된 위치 움직이는 블럭입니다.

### 버튼 값 읽어오기&#x20;

<div align="left"><figure><img src="../.gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure></div>

* 이 블럭은 버튼값이 0이면 이 다음 블록을 실행하고 0이 아니라면 계속 반복 블럭의 내용을 반복합니다.

{% hint style="info" %}
- 다음 반복 블럭은 반복 블럭 내에서만 쓸 수 있습니다.
- 버튼값: 0 이 의미하는 것은 버튼을 눌렀을 때를 의미합니다.
{% endhint %}

### 세 번 반복 블럭&#x20;

<div align="left"><figure><img src="../.gitbook/assets/image (2) (1).png" alt=""><figcaption></figcaption></figure></div>

* i 값이 0일때 한번, 1일때 한번, 2일때 한번 진행되며 각 진행이 끝났을때 i에 1을 더합니다.
* phase 2부터 4까지의 동작이 총 세 번 반복합니다.

***

