# 3D SLAM 시스템 참여

무인 지게차의 실내 창고 환경 자율주행을 위한 3D LiDAR-Inertial SLAM 시스템에 참여했다. SC-LIO-SAM 계열을 기반으로, 장기 운행 안정성과 동적 환경 대응을 개선하는 부분을 담당했다.

<figure markdown>
  <video controls muted playsinline width="100%">
    <source src="../media/media20.mp4" type="video/mp4">
  </video>
  <figcaption>실환경 SLAM 시연 — 실내 창고 환경 자율주행</figcaption>
</figure>

## 문제

창고 환경은 반복 구조(랙·팔레트)가 많고, 화물이나 작업자 같은 임시 물체가 계속 이동한다. 기본 SLAM은 이런 임시 물체까지 맵에 반영해서 ICP 정합이 흔들리고 위치 추정이 튀는 문제가 발생한다. 또한 장기 운행 시 loop closure가 실패하면서 맵이 점점 어긋난다.

## 접근

- **Loop closure 안정화** — 장기 운행 중 loop closure가 실패하는 원인을 분석하고, Scan Context 기반 relocalization의 트리거·검증 로직에 손을 얹었다
- **정적/동적 물체 분리** — Voxel Occupancy 기반으로 창고 내 임시 물체(화물·이동 물체·작업자)를 맵에서 분리해서, ICP 정합 저하와 위치 추정 튐 문제를 개선했다

## 결과

- 창고 환경 자율주행에서의 위치 추정 안정성 확보
- 임시 물체가 많은 상황에서도 맵 정합이 유지되는 흐름

## 사용 기술

SC-LIO-SAM · Scan Context · Voxel Occupancy · ROS 2 · C++17

## 관련 기술 조사

- [FAST-Calib: LiDAR-Camera Extrinsic Calibration in One Second](../../posts/fast-calib-review.md) — 이 SLAM 시스템에서 LiDAR-카메라 캘리브레이션 타겟 설계에 참고한 논문 리뷰
