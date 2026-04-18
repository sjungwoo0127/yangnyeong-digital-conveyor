# Phase 0: 변수 설정

## 개요

&#x20;시스템을 시작하기 전에 각 단계에서 로봇이 움직일 위치(좌표)를 설정합니다. "변수" 블록들에 미리 값을 입력해 로봇에게 "어디로 갈 수 있는지"를 알려주는 단계입니다.

***

## 블럭 다이어그램

<figure><img src="../.gitbook/assets/image (1).png" alt="" width="563"><figcaption></figcaption></figure>

***

## 변수별 설명

{% hint style="info" %}
각 변수의 설정 방법은 다음장 : **변수 설정 상세 가이드**에 있습니다.
{% endhint %}

### HOME\_x\_좌표

<figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

&#x20;: 처음 실행시켰을 때 이동할 초기 위치의 x좌표를 저장하는 변수입니다.

### HOME\_y\_좌표

<figure><img src="../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

&#x20;: 처음 실행시켰을 때 이동할 초기 위치의 z좌표를 저장하는 변수입니다.

### HOME

<figure><img src="../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

&#x20;: 처음 실행시켰을 때 이동할 초기 위치의 (x,y,z)좌표를 저장하는 변수입니다.

### 집기\_y좌표\_목록

<figure><img src="../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

&#x20;: 컨베이어를 실행 시키기 전, 컨베이어로 가져갈 각 물체들의 y좌표를 리스트로 저장하는 변수입니다.

### 집기\_x좌표\_목록

<figure><img src="../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

&#x20;: 컨베이어를 실행 시키기 전, 컨베이어로 가져갈 물체의 x좌표를 리스트로 저장하는 변수입니다.

### 집기\_z좌표\_목록

<figure><img src="../.gitbook/assets/image (38).png" alt=""><figcaption></figcaption></figure>

&#x20;: 컨베이어를 실행 시키기 전, 컨베이어로 가져갈 물체의 z좌표를 리스트로 저장하는 변수입니다.

### 물체\_높이

<figure><img src="../.gitbook/assets/image (39).png" alt=""><figcaption></figcaption></figure>

&#x20;: 컨베이어 위에서 집을 물체의 높이(z좌표)를 저장하는 변수입니다.

### 컨베이어 놓기

<figure><img src="../.gitbook/assets/image (40).png" alt=""><figcaption></figcaption></figure>

&#x20;: 집기 좌표를 통해 집은 물체를 컨베이어에 놓을 좌표(x,y,z)를 저장하는 변수입니다.

### 컨베이어 대기

<figure><img src="../.gitbook/assets/image (41).png" alt=""><figcaption></figcaption></figure>

&#x20;: 컨베이어에 물체를 놓고, 컨베이어가 움직일동안 대기하고 있을 좌표(x,y,z)를 저장하는 변수입니다.

### 스캔 위치

<figure><img src="../.gitbook/assets/image (42).png" alt=""><figcaption></figcaption></figure>

&#x20;: 컨베이어가 움직인 후, AI 카메라로 물체를 스캔할 위치의 좌표(x,y,z)를 저장하는 변수입니다.

### 분류\_y좌표\_목록

<figure><img src="../.gitbook/assets/image (43).png" alt=""><figcaption></figcaption></figure>

&#x20;: 스캔한 물체를 분류시킬 위치의 y좌표를 리스트로 저장하는 변수입니다.

### 분류\_x좌표\_목록

<figure><img src="../.gitbook/assets/image (44).png" alt=""><figcaption></figcaption></figure>

&#x20;: 스캔한 물체를 분류시킬 위치의 x좌표를 리스트로 저장하는 변수입니다.

### 분류\_z좌표\_목록

<figure><img src="../.gitbook/assets/image (45).png" alt=""><figcaption></figcaption></figure>

&#x20;: 스캔한 물체를 분류시킬 위치의 z좌표를 리스트 저장하는 변수입니다.

### 기본\_z\_좌표

<figure><img src="../.gitbook/assets/image (46).png" alt=""><figcaption></figcaption></figure>

&#x20;: 여러 단계에서 쓰일 기본 z값을 저장하는 변수입니다.



***
