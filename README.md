# HUENIT 컨베이어

## 실행 단계

1. **Phase 0** - 변 설정
2. **Phase 1** - 홈: 로봇을 대기 위치로 이동
3. **Phase 2** - 컨베이어 이동: 물체를 집어 컨베이어로 옮기기
4. **Phase 3** - 스캔: 물체를 카메라로 인식하기
5. **Phase 4** - 분류: 인식 결과에 따라 분류 위치로 이동

***

## 준비하기

### AI 카메라에 학습시키기

이 코드를 진행하기 전, AI카메라에 분류할 AprilTag를 학습시켜야 합니다.



### 학습시킨 모델 불러오기

PC와 AI 카메라를 연결시킨 후 **\[인공지능]**&#xD0ED;에서 **\[카메라 직접 학습 모델]**&#xC744; 눌러 학습시킨 **태그 인식** 모델을 불러와야 합니다.

<figure><img src=".gitbook/assets/image (6) (1) (1).png" alt=""><figcaption></figcaption></figure>

***

## 실행 영상

{% embed url="https://youtu.be/UvT1tSBQVKk" %}

***

***
