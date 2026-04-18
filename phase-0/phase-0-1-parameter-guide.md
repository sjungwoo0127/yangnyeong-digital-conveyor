---
description: 원하는 위치의 좌표를 측정하여 각 변수에 저장하기 위한 상세 가이드 입니다. 로봇의 좌표 측정 방법은 다음장에서 확인할 수 있습니다.
---

# 변수 상세 가이드

#### 블록 다이어그램

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

***

## 1. 홈 좌표

아래의 사진처럼 전체 동작을 실행하기 전의 홈 좌표를 설정합니다.

<figure><img src="../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

## 2. 집기 좌표

컨베이어로 옮길 각 물체의 좌표를 설정합니다.

{% hint style="warning" %}
샘플 코드에서 현재 각 물체의 x,z좌표가 동일하기에 한 개의 변수에 모두 저장되어 있습니다.
{% endhint %}

<figure><img src="../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>

## 3. 물체 높이

컨베이어 위에서 집을 물체의 z좌표를 설정합니다.

{% hint style="warning" %}
* 로봇 팔에 석션 모듈을 장착시킨 후, 컨베이어에 물체를 올리고 그 위에 로봇팔을 올려 z값을 측정합니다.
* 좌표값이 너무 낮으면 동작중 석션 모듈이 분리될 수 있습니다.
* 좌표값이 너무 높으면 동작중 물체를 제대로 집지 못할 수 있습니다.
{% endhint %}

<figure><img src="../.gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>

## 4. 컨베이어 높이/대기

## 5. 분류 좌표

## 6. 기본 z좌표
