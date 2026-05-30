# turbo

자율주행 ROS 미션 로봇 프로젝트. 카메라 + LiDAR 기반 단계별 미션 수행.

## 미션 구성

| 미션 | 파일 | 센서 | 설명 |
|------|------|------|------|
| Basic | `lanefollow.py` | 카메라 | HSV 흰색 차선 검출 + 슬라이딩 윈도우 |
| Mission 1 | `zone.py` | 카메라 | 빨강/파랑 색상 존 전환 |
| Mission 2 | `crosswalk.py` | 카메라 | 노란 횡단보도 검출 → 정지 |
| Mission 3 | `RonCone.py` | LiDAR | 콘 중심선 추종 + 벽 추종 폴백 + Pure Pursuit |
| Mission 4 | `lane_decision.py` | 카메라 | 우측 차선 단독 추종 |
| Mission 5 | `roundabout.py` | LiDAR + 카메라 | 이동 차량 감지 → 진입 판단 |
| Mission 6 | `tunnel_follow_50cm.py` | LiDAR | 좌우 벽 50cm 유지 터널 주행 |
| Mission 7 | `barrier_mission.py` | LiDAR | 차단기 감지 → 열릴 때까지 대기 후 통과 |
| Mission 8 | `auto_parking.py` | 없음 | 하드코딩 3단계 자동 주차 |

## 미션 전환

`/mission_num` (Float64) 토픽으로 모든 노드 간 미션 상태 공유.

## 제어 토픽

- `/high_level/ackermann_cmd_mux/input/nav_0` — 기본 차선 추종
- `/high_level/ackermann_cmd_mux/input/nav_1` — 미션별 제어 (우선순위 높음)
- `/commands/motor/speed`, `/commands/servo/position` — 터널/차단기 직접 제어
