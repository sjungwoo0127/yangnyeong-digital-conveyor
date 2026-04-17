# Phase 2: 컨베이어 이동 (Conveyor Movement)

## 🎛️ 개요

로봇이 물체를 집어 컨베이어로 옮깁니다.

---

## 🔄 동작 흐름

1. 집기 위치로 이동 → 물체 집기 (흡입)
2. 컨베이어로 이동 → 물체 놓기
3. 컨베이어 벨트 회전

---

## 🖥️ 핵심 코드

```python
def phase_2():
    # 집기 위치 선택
    집기_Y = 집기_y_좌표__목록[i]
    
    # 1. 집기
    robot.moveG0(집기_x__좌표, 집기_Y, 기본_Z__좌표)
    robot.moveG0(집기_x__좌표, 집기_Y, 집기_z__좌표)
    robot.suctionOn()
    time.sleep(1)
    
    # 2. 컨베이어로 이동 후 놓기
    robot.moveG0(집기_x__좌표, 집기_Y, 기본_Z__좌표)
    robot.moveG0(컨베이어__놓기)
    robot.suctionOff()
    
    # 3. 컨베이어 벨트 회전
    robot.sendCommand("G1 E43\n")
```

---

## 📚 상세 설명

- [물체 집기 (Gripper)](phase-2-1-gripper.md)
- [컨베이어 이동](phase-2-2-movement.md)
- [컨베이어 벨트 제어](phase-2-3-conveyor-belt.md)

---

**다음 단계**: [Phase 3: 스캔 위치로 이동](phase-3-scan.md)
