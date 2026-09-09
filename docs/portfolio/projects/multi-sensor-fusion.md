# Multi-Sensor Fusion 통합 R&D

RGB · Depth · LiDAR 이기종 센서를 하나의 파이프라인으로 통합하고, 운행 중 발생하는 정합 어긋남까지 자동으로 보정하는 아키텍처를 설계하고 있다. 현재 사내 R&D로 진행 중.

<figure markdown>
  <video controls muted playsinline width="100%">
    <source src="../media/media23.mp4" type="video/mp4">
  </video>
  <figcaption>PointNet 계열 3D 검출 시연 (Depth-only 환경)</figcaption>
</figure>

## 문제

단일 센서로는 정확도와 신뢰성에 한계가 있다. RGB만 쓰면 어두운 환경에서 무너지고, Depth만 쓰면 물체가 무엇인지 알 수 없다. 여러 센서를 함께 쓰려면 시각적으로만이 아니라 물리적으로도 정확히 정합되어야 하는데, 운행 중 진동·충격으로 정합이 조금씩 어긋나는 것이 문제다.

## 접근

세 축을 하나의 파이프라인으로 통합한다.

- **정적 캘리브레이션** — 설치 시점에 마커·기하 특징 기반으로 강체 정합 (yaw ±0.2° · offset ±2mm)
- **온라인 자가 보정** — 운행 중 LiDAR 특징점 재정합과 Kalman Smoothing으로 정합 어긋남을 지속 보정
- **PointPainting 스타일 융합** — RGB Segmentation을 3D Point Cloud에 픽셀 단위로 투영해서 3D 검출 정확도를 높인다
- **이상 감지·재캘리 트리거** — 재투영 오차와 Depth 일관성을 상시 모니터링, 임계 초과 시 자동 재캘리 트리거

## 현재 상태

- PointNet 계열 3D 검출 시연 완료 (Depth-only 환경)
- Fusion 통합 파이프라인 설계 단계
- 온라인 자가 보정 알고리즘 초기 구현 완료

## 사용 기술

PyTorch · CUDA · TensorRT · PointNet 계열 · ROS 2

## 관련 기술 조사

- [FAST-Calib: LiDAR-Camera Extrinsic Calibration in One Second](../../posts/fast-calib-review.md) — Cross-modal 캘리브레이션 타겟 설계에 참고한 논문 리뷰
- [NVIDIA Isaac ROS NITROS: 득실과 실제 제약 정리](../../posts/nitros-review.md)
