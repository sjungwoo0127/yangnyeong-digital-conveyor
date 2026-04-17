# 카메라 초기화 과정 (Camera Initialization)

## 🔧 초기화 단계

```python
def prepare_camera_for_tag(level=2):
    """카메라를 물체 인식 모드로 설정"""
```

---

## 📋 초기화 순서

### 1단계: 레벨별 설정값 선택

```python
if level == 2:
    exp_scale = 0.70      # 노출 스케일
    gain_ceiling = 4      # 최대 게인
```

---

### 2단계: 자동 설정 시작

```python
sensor.run(0)                    # 카메라 중지
sensor.set_auto_gain(True)       # 자동 게인 활성화
sensor.set_auto_whitebal(True)   # 자동 화이트 밸런스
sensor.set_auto_exposure(True)   # 자동 노출
sensor.set_gainceiling(gain_ceiling)  # 게인 제한
sensor.run(1)                    # 카메라 시작
```

---

### 3단계: 초기 안정화 (800ms)

```python
sensor.skip_frames(time=800)  # 8프레임 스킵
```

**목표**: 자동 설정이 안정화될 때까지 대기

---

### 4단계: 노출값 고정

```python
exp_us = sensor.get_exposure_us()      # 현재 노출값 읽기
locked_exp = int(exp_us * exp_scale)   # 스케일 적용
```

---

### 5단계: 최종 설정

```python
sensor.run(0)  # 카메라 중지
sensor.set_auto_exposure(False, locked_exp)  # 노출 고정
sensor.set_auto_gain(True)        # 게인은 자동
sensor.set_gainceiling(gain_ceiling)
sensor.set_auto_whitebal(False)   # 화이트 밸런스 고정
sensor.set_brightness(0)          # 밝기: 기본값
sensor.set_contrast(0)            # 명도차: 기본값
sensor.set_saturation(0)          # 채도: 기본값
sensor.run(1)  # 카메라 재시작
```

---

### 6단계: 최종 안정화 (300ms)

```python
sensor.skip_frames(time=300)  # 3프레임 스킵
```

**목표**: 최종 설정이 안정화될 때까지 대기

---

## ✅ 초기화 완료 조건

- [ ] 카메라 시작됨
- [ ] 자동 설정 완료
- [ ] 노출값 고정됨
- [ ] 800ms + 300ms 대기 완료
- [ ] 물체 인식 준비 완료

---

## 💡 초기화 시간

- **전체 시간**: 약 1.1초 (800ms + 300ms)
- **목표**: 물체가 정확히 인식되도록 카메라 최적화

---

**뒤로**: [Phase 3: 스캔 준비](phase-3-scan.md)
