# 초기화 과정

## 🔧 시스템 시작 순서

### 1단계: 라이브러리 임포트

```python
import robot      # 로봇 제어
import time       # 시간 지연
import btn        # 버튼 입력
import sensor     # 카메라 센서
import cam        # AI 카메라
import lcd        # 화면 출력
import math       # 수학 함수
```

---

### 2단계: 하드웨어 초기화

```python
lcd.init()        # LCD 화면 시작
cam.ai_init(5)    # AI 모드 시작 (5개 물체 추적)
```

---

### 3단계: 파라미터 정의

```python
# 위치 좌표 설정 (Phase 0-1 참고)
집기_y_좌표__목록 = [-40, 0, 40]
집기_x__좌표 = 277
집기_z__좌표 = -60
# ... 기타 좌표 ...
```

---

### 4단계: 시작 대기

```python
while True:
    time.sleep(0.000001)  # CPU 과부하 방지
    robot.moveG0(HOME)    # 홈으로 이동
    if btn.value() != 0:
        continue          # 버튼 입력 대기
    # Phase 2부터 시작
```

---

## ✅ 체크리스트

- [ ] 모든 라이브러리 임포트됨
- [ ] LCD 화면 켜짐
- [ ] 카메라 초기화됨
- [ ] 파라미터 값 설정됨
- [ ] 로봇이 홈 위치로 이동됨
- [ ] 버튼 준비 완료

---

**뒤로**: [Phase 0: 파라미터 설정](phase-0-parameters.md)
