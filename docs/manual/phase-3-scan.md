# Phase 3: 스캔 준비 (Camera Preparation)

## 📸 개요

로봇을 스캔 위치로 이동하고 카메라를 물체 인식 모드로 설정합니다.

---

## 🔄 동작 흐름

1. 로봇을 카메라 위치로 이동
2. 카메라 초기화 (조명, 노출 자동 조절)
3. 물체 인식 준비 완료

---

## 🖥️ 핵심 코드

```python
def phase_3():
    # 스캔 위치로 이동
    robot.moveG0(스캔__위치)
    
    # 카메라 준비 (레벨 2 = 보통 밝기)
    prepare_camera_for_tag(2)
```

**결과**: 카메라가 물체를 감지할 준비 완료

---

## 📚 상세 설명

- [카메라 레벨 설정](phase-3-1-camera-levels.md)
- [노출 및 게인 조절](phase-3-2-exposure-gain.md)
- [카메라 초기화 과정](phase-3-3-camera-init.md)

---

**다음 단계**: [Phase 4: 물체 분류](phase-4-classify.md)
