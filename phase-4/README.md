# Phase 4: 물체 분류

## 🤖 개요

카메라로 물체를 인식하고, 인식 결과에 따라 적절한 분류 위치로 옮깁니다.

***

## 🔄 동작 흐름

1. 카메라로 물체 감지
2. 물체 위치를 로봇 좌표로 변환
3. 물체를 해당 분류 위치로 옮기기
4. 홈으로 돌아가기

***

## 🖥️ 핵심 코드

```python
def phase_4():
    while True:
        # 1. 물체 감지 대기
        result = _stable_check(1, 10, 3)
        
        if result != None:
            pixel_x, pixel_y, tag_id = result
            
            # 2. 픽셀 → 로봇 좌표 변환
            target_x, target_y = pixel_to_suction_movement(
                pixel_x, pixel_y, 집기__높이
            )
            
            # 3. 물체 집기
            robot.moveG0(target_x, target_y, 기본_Z__좌표)
            robot.suctionOn()
            time.sleep(1)
            
            # 4. 분류 위치로 옮기기
            분류_y = 분류_y_좌표__목록[tag_id - 1]
            robot.moveG0(분류_X__좌표, 분류_y, 기본_Z__좌표)
            robot.suctionOff()
            
            # 5. 홈으로 돌아가기
            robot.moveG0(HOME_X__좌표, HOME_Y__좌표, 기본_Z__좌표)
            break
```

**결과**: 물체 분류 완료 → 다음 사이클 준비

***

## 📚 상세 설명

* [물체 감지 (Detection)](phase-4-1-detection.md)
* [좌표 변환 (Pixel to Robot)](phase-4-2-coordinate-conversion.md)
* [물체 분류 규칙](/broken/pages/OCNB87LwpwHwZQeCP8pC)

***

**완료**: 한 사이클 종료. Phase 1부터 다시 시작됩니다.
