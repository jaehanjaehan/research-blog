# Sim-to-Real 강화학습 자율주행 드론

**과학기술정보통신부 장관상** (2022 · ITRC ICT 콜로키움 · 학생창의자율과제 부문)

시뮬레이션에서 학습한 회피 정책을 실제 드론으로 이관해서, GPS 신호가 없는 실내 환경에서 장애물 회피 비행에 성공한 프로젝트. 세종대학교 HCI 연구실 석사 과정에서 진행했다.

<figure markdown>
  <video controls muted playsinline width="100%">
    <source src="../media/media6.mp4" type="video/mp4">
  </video>
  <figcaption>실환경 실드론 회피 비행 시연 — Sim-to-Real 전이 검증</figcaption>
</figure>

## 문제

시뮬레이션에서 잘 학습된 정책이 실환경에서는 시각적 차이·물리적 노이즈로 무너진다 (Reality Gap). 특히 GPS가 통하지 않는 실내 환경에서는 외부 위치 신호 없이 영상만으로 자율주행이 가능한지 검증할 필요가 있었다.

## 접근

- **하이브리드 정책 학습** — Actor-Critic RL과 U-Net Segmentation을 결합. Critic 네트워크에 Segmentation Feature를 벡터화한 Optical Flow로 전달, Actor는 3축 속도(NED)를 출력
- **Reality Gap 완화** — RGB 원본이 아니라 Segmentation Label Map을 정책 입력으로 사용. 가상 환경과 실제 환경의 시각적 차이를 흡수한다
- **Sim-to-Real 전이** — AirSim + Unreal Engine 4에서 학습한 모델을 그대로 실드론에 이관해서 실내 GPS-Denied 환경에서 회피 비행 검증

## 결과

- 시뮬레이션에서 학습한 회피 정책이 **실환경에서 그대로 동작**하는 것을 검증
- 여러 세대(Generation)별 학습 진행에 따라 회피 궤적이 정밀화되는 정량 관찰
- **과학기술정보통신부 장관상 수상** (2022)

## 사용 기술

Unreal Engine 4 · AirSim · PyTorch · ROS · Python

## 이 연구가 남긴 것

시뮬레이션의 완벽함이 실환경에서 무너지는 지점, 그리고 그것을 통제 가능한 변수로 분해해야 한다는 감각이 이 프로젝트에서 자리 잡았다. 이후 실무에서 [Isaac Sim 기반 R&D](isaac-sim-r-and-d.md)로 이어졌다.
