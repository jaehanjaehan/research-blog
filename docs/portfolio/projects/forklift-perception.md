# 자율주행 무인 지게차 3D Perception

산업 자율주행 무인 지게차의 비전 인식 시스템을 개발했다. 데이터, 알고리즘, 통합, 배포까지 전 주기를 담당했다.

<figure markdown>
  <video controls muted playsinline width="100%">
    <source src="../media/media11.mp4" type="video/mp4">
  </video>
  <figcaption>특수 팔레트 자동 검출 · 진입 판정 시연</figcaption>
</figure>

## 문제

산업 현장의 무인 지게차가 팔레트를 인식하고 정확한 위치에 포크를 진입시키는 문제. 강조명·반사·센서 노이즈가 큰 환경이라 시뮬레이션 성능이 그대로 나오지 않는다. 오인식이 곧 안전 사고로 이어지는 Safety-Critical 시스템.

## 접근

**Hybrid 설계** — AI가 "무엇이 어디에 있는가"를 찾고, 기하학이 "정확히 얼마인가"를 실측한다. 두 단계를 완전히 분리해서 사고가 났을 때 원인을 추적할 수 있게 했다.

- **AI (RGB → Semantic ROI)**: YOLO 계열 세그멘테이션 모델을 도메인 데이터로 파인튜닝
- **Geometry (ROI → 3D 실측)**: Depth 센서로 물리적 거리·각도를 계산
- **Robust Estimation**: 예측 오차 기반 필터로 이상치 거부, 검출 실패 프레임에서도 이전 궤적으로 위치 예측
- **Safety Fallback**: 인식과 제어를 교차 검증해서 이상 징후 시 즉시 정지

## 결과

- **검출 성공률 99.7%** (6개월간 오검출 1~2회 수준)
- **측정값 흔들림 약 79% 감소**
- **원시 오차 약 96% 감소** (P90 83mm → σ ±3mm)
- **이상치 발생률 15% → 0.3%**
- **국내 대형 제조사 라인 다수에 배포** — 수도권·지방 사업장에서 실운용 중

## 사용 기술

C++17 · Python · OpenCV · PyTorch · Ultralytics YOLO · TensorRT · ONNX · ROS 2 Humble · CAN · Docker · Weights & Biases

## 관련 기술 조사

- [NVIDIA Isaac ROS NITROS: 득실과 실제 제약 정리](../../posts/nitros-review.md)
- [ROS2 노드 컴포지션: 개념과 실제 성능 임팩트](../../posts/ros2-composition.md)
