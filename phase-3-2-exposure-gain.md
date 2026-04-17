# 노출 및 게인 조절 (Exposure & Gain)

## 🎯 개요

카메라의 노출(밝기)과 게인(증폭)을 자동으로 조절하여 최적의 이미지를 만듭니다.

---

## 📊 노출 (Exposure)

### 노출값이란?
카메라 센서가 빛을 받는 시간. 길수록 밝은 이미지.

### 노출 스케일 (`exp_scale`)
```python
exp_scale = 0.70  # 기본값 (level 2)
```

| exp_scale | 특징 | 사용 환경 |
|-----------|------|---------|
| 0.55 | 어두움 | 조명 없는 실내 |
| 0.70 | 보통 | 일반 실내 |
| 0.85 | 밝음 | 창가 |
| 1.00 | 매우 밝음 | 실외 |

---

## 📊 게인 (Gain)

### 게인이란?
신호를 얼마나 증폭할지를 정하는 값. 높을수록 밝지만 노이즈 증가.

### 최대 게인 (`gain_ceiling`)
```python
gain_ceiling = 4  # 기본값 (level 2)
```

| gain_ceiling | 밝기 | 노이즈 |
|--------------|------|-------|
| 2 | 어두움 | 적음 |
| 4 | 보통 | 적음 |
| 8 | 밝음 | 중간 |
| 16 | 매우 밝음 | 많음 |

---

## 🖥️ 자동 조절 코드

```python
sensor.set_auto_exposure(True)   # 자동 노출 활성화
sensor.set_auto_gain(True)       # 자동 게인 활성화
sensor.set_gainceiling(4)        # 최대 게인 제한
```

---

## ⚙️ 수동 조절

원하는 값으로 고정하려면:

```python
# 노출값 고정
locked_exp = 5000  # 마이크로초
sensor.set_auto_exposure(False, locked_exp)

# 게인 고정 (비활성화)
sensor.set_auto_gain(False)
```

---

## 💡 조정 팁

| 문제 | 해결 방법 |
|------|---------|
| 이미지 너무 어두움 | `exp_scale` 증가 또는 `gain_ceiling` 증가 |
| 이미지 너무 밝음 | `exp_scale` 감소 또는 `gain_ceiling` 감소 |
| 물체 경계가 흐림 | `exp_scale` 감소 (노출 줄이기) |
| 노이즈 많음 | `gain_ceiling` 감소 |

---

**뒤로**: [Phase 3: 스캔 준비](phase-3-scan.md)
