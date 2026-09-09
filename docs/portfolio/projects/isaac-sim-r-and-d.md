# Isaac Sim 기반 Sim-to-Real R&D

Reality Gap을 통제 가능한 변수로 분해해서 모델의 강건성과 검증 가능성을 정량적으로 평가하는 시뮬레이션 기반 R&D. 현재 사내 R&D로 진행 중.

<figure markdown>
  <video controls muted playsinline width="100%">
    <source src="../media/media26.mp4" type="video/mp4">
  </video>
  <figcaption>Isaac Sim 4.2 + ROS2 통합 시뮬레이션 시연</figcaption>
</figure>

## 문제

실환경에서 재현하기 어려운 극한 상황들이 있다. 특정 조명 조건, 특정 시간대의 역광, 반복 구조에서의 Feature Ambiguity, 다중 이동체 동시 상황 같은 것들. 이런 상황들을 실환경에서 반복 재현하는 것은 시간·비용 모두 부담이 크고, 안전 문제도 있다. 시뮬레이션에서 이 조건들을 파라미터화해서 통제할 수 있다면, 모델의 강건성을 정량적으로 평가하고 회귀 검증할 수 있다.

## 접근

- **4단계 워크플로우** — Scene 설정 → 데이터 생성 → 자동 라벨링 → 검증
- **다중 모달 동기 렌더링** — RGB · Depth · LiDAR · Segmentation 동시 생성
- **자동 라벨링** — 기존 학습된 인식 모델을 활용해서 시뮬레이션 데이터에 자동으로 라벨을 붙인다
- **Reality Gap Factor 파라미터화** — 조명 변화·반복 구조·동적 장애물·센서 노이즈 네 가지 축을 각각 통제 가능한 변수로 분해
- **반복 시나리오 검증** — 같은 시나리오를 반복해서 데이터·모델 품질을 정량 비교

## 현재 상태

- Isaac Sim 4.2 + ROS 2 통합 환경 구축 완료
- 다중 모달 렌더링 파이프라인 초기 구현
- Reality Gap Factor 파라미터화 설계 단계

## 사용 기술

NVIDIA Isaac Sim · ROS 2 · Python

## 이 R&D의 뿌리

석사 시절 진행한 [AirSim + Unreal Engine 기반 Sim-to-Real 강화학습 연구](sim2real-drone.md)에서 자리 잡은 감각이 실무 R&D로 이어진 부분이다. 시뮬레이션의 완벽함이 실환경에서 무너지는 지점을 통제 가능한 형태로 다루는 것이 두 프로젝트의 공통 축이다.
