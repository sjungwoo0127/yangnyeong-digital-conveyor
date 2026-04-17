# Phase 4: 물체 분류 (Object Classification)

## 🤖 개요

카메라로 **물체를 인식**하고, 인식 결과에 따라 **분류 위치**로 이동시킵니다.  
이 단계에서는 AI 알고리즘이 물체의 위치를 계산하고, 로봇이 자동으로 적절한 분류 위치로 물체를 옮깁니다.

---

## 🎯 목표

1. 카메라로 물체 위치 인식
2. 인식된 위치를 로봇 좌표로 변환
3. 물체를 분류 위치로 이동
4. 홈으로 돌아가기

---

## 🔄 동작 과정

### 1단계: 물체 감지 루프
카메라가 물체를 안정적으로 감지할 때까지 반복합니다.

```
🎥 물체 감지 중...
  ├─ 1프레임 촬영
  ├─ AI로 물체 인식
  ├─ 위치 저장
  ├─ 안정성 검사
  └─ 안정적 ✓ → 다음 단계
```

### 2단계: 픽셀 좌표 → 로봇 좌표 변환
카메라 이미지의 픽셀 좌표를 로봇이 이해할 수 있는 공간 좌표로 변환합니다.

```
카메라 이미지 (픽셀)          로봇 공간 (mm)
┌─────────┐                ┌─────────┐
│    ●    │  변환 함수      │    ●    │
│         │  ────────→      │         │
│         │                 │         │
└─────────┘                └─────────┘
(320×240)                  (x, y, z)
```

### 3단계: 물체 집기
로봇이 변환된 좌표로 이동하여 물체를 집습니다.

```
[스캔 위치]
  ↓
[변환된 좌표] ← 물체 위치
  ↓
🤖 [흡입 ON]
```

### 4단계: 분류 위치로 이동
인식된 물체 종류(tag_id)에 따라 해당하는 분류 위치로 이동합니다.

```
tag_id = 1 → 분류_y[0] = 80   위치로 이동
tag_id = 2 → 분류_y[1] = 5    위치로 이동
tag_id = 3 → 분류_y[2] = -70  위치로 이동
```

### 5단계: 물체 놓기
분류 위치에서 물체를 놓습니다.

```
[분류 위치]
  ↓
🤖 [흡입 OFF] ← 물체 떨어짐 ✓
```

### 6단계: 홈으로 돌아가기
다음 사이클을 위해 홈 위치로 이동합니다.

```
[분류 위치]
  ↓
[홈] ← 다음 Phase 2 시작 준비 ✓
```

---

## 🖥️ Phase 4 코드

```python
def phase_4():
    global 변환__좌표__리스트, 기본_Z__좌표, 분류_Y__좌표
    
    # Step 1: 루프 시작 - 물체 감지 대기
    while True:
        time.sleep(0.000001)  # CPU 과부하 방지
        
        # Step 2: 안정적인 물체 감지
        result = _stable_check(1, 10, 3)
        
        if result != None:  # 물체 감지됨
            # 결과 언팩: (pixel_x, pixel_y, tag_id)
            pixel_x, pixel_y, tag_id = result[0], result[1], result[2]
            
            # Step 3: 픽셀 좌표를 로봇 좌표로 변환
            변환__좌표__리스트 = pixel_to_suction_movement(
                pixel_x, 
                pixel_y, 
                집기__높이
            )
            
            # 변환된 좌표 추출
            변환_X__좌표 = 변환__좌표__리스트[0]
            변환_Y__좌표 = 변환__좌표__리스트[1]
            
            # Step 4: 변환된 위치로 이동 (상단)
            robot.moveG0(변환_X__좌표, 변환_Y__좌표, 기본_Z__좌표)
            
            # Step 5: 물체 위치까지 내려가기
            robot.moveG0(변환_X__좌표, 변환_Y__좌표, 집기__높이)
            
            # Step 6: 물체 흡입
            robot.suctionOn()
            time.sleep(1)
            
            # Step 7: 안전 높이로 올리기
            robot.moveG0(변환_X__좌표, 변환_Y__좌표, 기본_Z__좌표)
            
            # Step 8: 분류 위치 Y좌표 선택 (tag_id 기반)
            분류_Y__좌표 = 분류_y_좌표__목록[int(tag_id - 1)]
            
            # Step 9: 분류 위치로 이동 (상단)
            robot.moveG0(분류_X__좌표, 분류_Y__좌표, 기본_Z__좌표)
            
            # Step 10: 분류 위치까지 내려가기
            robot.moveG0(분류_X__좌표, 분류_Y__좌표, 분류_Z__좌표)
            
            # Step 11: 물체 놓기
            robot.suctionOff()
            time.sleep(2)
            
            # Step 12: 분류 위치에서 안전 높이로 올리기
            robot.moveG0(분류_X__좌표, 분류_Y__좌표, 기본_Z__좌표)
            
            # Step 13: 홈으로 이동
            robot.moveG0(HOME_X__좌표, HOME_Y__좌표, 기본_Z__좌표)
            
            # Step 14: 루프 종료 (한 사이클 완료)
            break


def _stable_check(threshold, stable_range, miss_tol):
    """
    물체 감지 안정성 확인
    
    threshold: 연속 감지 프레임 수 (1 = 즉시)
    stable_range: 안정성 범위 (픽셀, 작을수록 엄격)
    miss_tol: 미감지 허용 횟수 (3 = 3프레임 연속 미감지 시 리셋)
    """
    
    global 변환__좌표__리스트
    
    _img = cam.snapshot()  # 카메라 이미지 촬영
    cam.compute(_img)      # AI 물체 인식
    _output = cam.get_output()  # 결과 읽기
    
    if _output.rect is not None:  # 물체 감지됨
        _r = _output.rect
        _stable_tag_id = _output.idx  # 물체 ID
        _stable_miss = 0
        
        # 물체 중심 좌표 계산
        center_x = _r[0] + _r[2] / 2
        center_y = _r[1] + _r[3] / 2
        _stable_points.append((center_x, center_y))
        
        # 최근 N개 프레임만 유지
        if len(_stable_points) > threshold:
            _stable_points.pop(0)
        
        # 안정성 검사
        if len(_stable_points) == threshold:
            _xs = [p[0] for p in _stable_points]
            _ys = [p[1] for p in _stable_points]
            
            if max(_xs) - min(_xs) <= stable_range and \
               max(_ys) - min(_ys) <= stable_range:
                # 안정적 ✓
                _avg_x = sum(_xs) / threshold
                _avg_y = sum(_ys) / threshold
                _stable_points.clear()
                lcd.display(_img)
                return (_avg_x, _avg_y, _stable_tag_id)
        
        # 디버그: 화면에 표시
        cam.draw_rectangle(_img, _r, color=(255, 64, 64), thickness=2)
        cam.draw_string(_img, (10, 20), str(_stable_tag_id), scale=1)
    else:
        # 물체 미감지
        _stable_miss += 1
        if _stable_miss > miss_tol:
            _stable_points.clear()
            _stable_miss = 0
    
    lcd.display(_img)
    return None


def pixel_to_suction_movement(pixel_x, pixel_y, object_height=22, 
                             camera_height=93.7, suction_height=40):
    """
    카메라 픽셀 좌표 → 로봇 좌표 변환
    
    매개변수:
    - pixel_x, pixel_y: 카메라 이미지의 픽셀 좌표
    - object_height: 물체의 높이 (mm)
    - camera_height: 카메라 높이 (mm)
    - suction_height: 흡입기 높이 (mm)
    
    반환값:
    - (robot_x, robot_y): 로봇이 이동할 좌표
    """
    
    # 복잡한 수학적 변환 (카메라 캘리브레이션 포함)
    # - 픽셀 좌표를 mm 단위로 변환
    # - 로봇 각도에 따른 보정
    # - 높이에 따른 드리프트 보정
    # → 최종적으로 로봇이 정확히 물체를 집을 수 있는 좌표 계산
    
    return robot_x, robot_y
```

### 코드 블록별 설명

| 블록 | 설명 |
|------|------|
| `_stable_check()` | 카메라 물체 감지 & 안정성 확인 |
| `pixel_to_suction_movement()` | 픽셀 좌표 → 로봇 좌표 변환 |
| `tag_id` | 인식된 물체 ID (1, 2, 3 등) |
| `분류_y_좌표__목록[tag_id-1]` | 물체 종류별 분류 위치 선택 |

---

## 📊 주요 파라미터

| 파라미터 | 현재값 | 설명 |
|---------|-------|------|
| `threshold` | 1 | 안정성 확인 프레임 수 |
| `stable_range` | 10 | 안정성 범위 (픽셀) |
| `miss_tol` | 3 | 미감지 허용 횟수 |
| `tag_id` | 1~3 | 인식된 물체 ID |
| `분류_y_좌표__목록` | [80, 5, -70] | 분류 위치 3개 |

---

## ⚙️ 물체 분류 규칙

물체는 `tag_id`에 따라 자동으로 분류됩니다:

```
tag_id = 1 → Y = 80   (분류 위치 1)
tag_id = 2 → Y = 5    (분류 위치 2)
tag_id = 3 → Y = -70  (분류 위치 3)
```

더 많은 물체 종류를 추가하려면:
```python
분류_y_좌표__목록 = [80, 5, -70, 50, ...]  # 원하는 개수만큼 추가
```

---

## ✅ Phase 4 완료 조건

- ✓ 물체가 카메라로 감지됨
- ✓ 좌표 변환 성공
- ✓ 물체를 올바른 분류 위치에 놓음
- ✓ 로봇이 홈으로 돌아감

---

## 🔗 전체 워크플로우

```
[Phase 1: 홈]
  ↓
반복 (i = 0, 1, 2)
  ├─ [Phase 2: 컨베이어 이동]
  ├─ [Phase 3: 스캔 준비]
  └─ [Phase 4: 물체 분류]
  ↓
[홈으로 돌아가기]
  ↓
대기 중... (버튼 입력 대기)
```

---

**완료**: 한 사이클이 끝났습니다! 다시 Phase 1부터 시작됩니다.
