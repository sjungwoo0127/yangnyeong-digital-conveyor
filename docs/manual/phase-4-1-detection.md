# 물체 감지 (Object Detection)

## 🎥 개요

카메라로 컨베이어 위의 물체를 감지합니다.

---

## 🔄 감지 과정

### 1단계: 이미지 촬영

```python
_img = cam.snapshot()  # 카메라로 사진 촬영
```

---

### 2단계: AI로 인식

```python
cam.compute(_img)      # AI가 물체 분석
_output = cam.get_output()  # 결과 읽기
```

**AI가 찾는 정보**:
- `_output.rect`: 물체 위치 (x, y, 너비, 높이)
- `_output.idx`: 물체 ID (tag_id)

---

### 3단계: 안정성 확인

```python
result = _stable_check(1, 10, 3)
```

**파라미터 의미**:
- `1`: 1프레임 연속 감지 (즉시)
- `10`: 픽셀 범위 10 이내 (안정성 기준)
- `3`: 3프레임 연속 미감지 시 리셋

---

## 🖥️ 감지 함수

```python
def _stable_check(threshold, stable_range, miss_tol):
    """
    안정적인 물체 감지
    
    threshold: 연속 감지 프레임 수
    stable_range: 위치 변동 허용 범위 (픽셀)
    miss_tol: 미감지 허용 횟수
    """
    
    # 이미지 촬영 & 분석
    _img = cam.snapshot()
    cam.compute(_img)
    _output = cam.get_output()
    
    if _output.rect is not None:
        # 물체 감지됨
        _r = _output.rect
        tag_id = _output.idx
        
        # 물체 중심 계산
        center_x = _r[0] + _r[2] / 2
        center_y = _r[1] + _r[3] / 2
        
        # 위치 저장 & 안정성 검사
        # ... (상세한 계산)
        
        return (center_x, center_y, tag_id)
    
    return None  # 감지 실패
```

---

## 📊 감지 파라미터 조정

| 파라미터 | 현재값 | 조정 | 영향 |
|---------|-------|------|------|
| threshold | 1 | 증가 (예: 3) | 더 안정적 (느림) |
| stable_range | 10 | 증가 (예: 20) | 더 관대 (덜 정확) |
| miss_tol | 3 | 증가 (예: 5) | 더 관대 |

---

## 💡 감지 문제 해결

| 문제 | 원인 | 해결 |
|------|------|------|
| 물체가 감지 안 됨 | 카메라 레벨 부족 | Phase 3 카메라 설정 확인 |
| 감지가 불안정함 | threshold 또는 stable_range 부족 | 값 증가 |
| 잘못된 물체 인식 | AI 모델 문제 | 조명 또는 카메라 각도 확인 |

---

**뒤로**: [Phase 4: 물체 분류](phase-4-classify.md)
