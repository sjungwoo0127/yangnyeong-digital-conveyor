# Phase 3: 스캔 위치로 이동 (Scan Preparation)

## 📸 개요

로봇을 **스캔 카메라 위치**로 이동하고, **AI 카메라**를 물체 인식을 위해 준비합니다.  
이 단계에서는 조명과 노출 설정을 최적화하여 정확한 물체 인식을 준비합니다.

---

## 🎯 목표

1. 로봇을 스캔 위치로 이동
2. 카메라 설정 (조명, 노출, 게인)
3. 다음 Phase의 물체 인식을 위한 준비

---

## 🔄 동작 과정

### 1단계: 스캔 위치로 이동
로봇이 카메라 앞 정확한 위치로 이동합니다.

```
[컨베이어]
  ↓
[스캔 위치] ← 카메라 대면
```

### 2단계: 카메라 초기화
AI 카메라를 물체 인식 모드로 설정합니다.

```
🎥 카메라 초기화 중...
  ├─ 자동 게인 조절
  ├─ 자동 노출 조절
  ├─ 자동 화이트 밸런스 조절
  └─ 설정값 잠금 (안정화)
```

---

## 🖥️ Phase 3 코드

```python
def phase_3():
    # Step 1: 스캔 위치로 이동
    robot.moveG0(스캔__위치)
    
    # Step 2: 카메라 준비 (레벨 2 = 중간 밝기)
    prepare_camera_for_tag(2)


def prepare_camera_for_tag(level=2):
    """
    카메라를 물체 인식 모드로 준비
    
    level:
      1 = 어두운 환경 (exp_scale: 0.55)
      2 = 보통 환경 (exp_scale: 0.70) ← 기본값
      3 = 밝은 환경 (exp_scale: 0.85)
      4 = 매우 밝은 환경 (exp_scale: 1.00)
    """
    
    # 레벨별 카메라 설정값 선택
    if level == 1:
        exp_scale = 0.55      # 노출 스케일 (낮을수록 어두움)
        gain_ceiling = 2      # 최대 게인 (낮을수록 적음)
    elif level == 2:
        exp_scale = 0.70
        gain_ceiling = 4
    elif level == 3:
        exp_scale = 0.85
        gain_ceiling = 8
    elif level == 4:
        exp_scale = 1.00
        gain_ceiling = 16
    else:
        exp_scale = 0.70
        gain_ceiling = 4
    
    # 카메라 설정
    sensor.run(0)                           # 카메라 중지
    sensor.set_auto_gain(True)              # 자동 게인 활성화
    sensor.set_auto_whitebal(True)          # 자동 화이트 밸런스 활성화
    sensor.set_auto_exposure(True)          # 자동 노출 활성화
    sensor.set_gainceiling(gain_ceiling)    # 최대 게인 설정
    sensor.run(1)                           # 카메라 시작
    
    # 초기 설정 안정화 대기 (800ms)
    sensor.skip_frames(time=800)
    
    # 현재 노출값 읽고 스케일 적용
    exp_us = sensor.get_exposure_us()
    locked_exp = int(exp_us * exp_scale)
    
    # 최종 카메라 잠금 설정
    sensor.run(0)                           # 카메라 중지
    sensor.set_auto_exposure(False, locked_exp)  # 노출 고정
    sensor.set_auto_gain(True)              # 게인은 자동
    sensor.set_gainceiling(gain_ceiling)    # 최대 게인
    sensor.set_auto_whitebal(False)         # 화이트 밸런스 고정
    sensor.set_brightness(0)                # 밝기: 기본값
    sensor.set_contrast(0)                  # 명도차: 기본값
    sensor.set_saturation(0)                # 채도: 기본값
    sensor.run(1)                           # 카메라 재시작
    
    # 최종 안정화 대기 (300ms)
    sensor.skip_frames(time=300)
    
    return locked_exp, gain_ceiling
```

### 코드 블록별 설명

| 블록 | 설명 |
|------|------|
| `robot.moveG0(스캔__위치)` | 로봇을 스캔 위치로 이동 |
| `sensor.run(0/1)` | 카메라 정지(0) / 시작(1) |
| `sensor.set_auto_gain()` | 자동 게인 조절 활성화 |
| `sensor.set_auto_exposure()` | 자동 노출 조절 |
| `sensor.skip_frames()` | 안정화 대기 |
| `sensor.set_gainceiling()` | 최대 게인값 제한 |

---

## 📊 카메라 레벨 가이드

| 레벨 | 환경 | 노출값 | 게인 | 추천 사용 |
|------|------|--------|------|----------|
| **1** | 어두운 실내 | 0.55 | 2 | 조명 없는 실내 |
| **2** | 보통 실내 | 0.70 | 4 | 일반 실내 (기본값) |
| **3** | 밝은 실내 | 0.85 | 8 | 창가 근처 |
| **4** | 실외/매우 밝음 | 1.00 | 16 | 실외 작업 |

---

## ⚙️ 파라미터 조정 시 주의사항

- **카메라 레벨**: 물체가 검은색일 경우 레벨 3 이상 권장
- **노출값 (exp_scale)**: 낮을수록 더 빠른 응답, 높을수록 더 안정적
- **게인 (gain_ceiling)**: 높을수록 더 밝지만 노이즈 증가
- **환경 변화 시**: `prepare_camera_for_tag()` 호출 시 레벨 변경

```python
# 예: 매우 밝은 환경에서는
prepare_camera_for_tag(4)  # 레벨 4 사용
```

---

## ✅ Phase 3 완료 조건

- ✓ 로봇이 스캔 위치에 도달
- ✓ 카메라가 초기화 완료
- ✓ 노출 설정이 안정화됨
- ✓ 다음 물체 인식 준비 완료

---

## 🔗 워크플로우

```
[Phase 2: 컨베이어 이동]
  ↓
[Phase 3: 스캔 위치로 이동]
  ├─ 로봇 위치 이동
  ├─ 카메라 초기화
  └─ 노출/게인 설정
  ↓
[Phase 4: 물체 분류]
```

---

**다음 단계**: [Phase 4: 물체 분류](phase-4-classify.md)
