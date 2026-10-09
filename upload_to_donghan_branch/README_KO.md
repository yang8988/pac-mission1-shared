# 동한 5-③~⑥: 확장 학습과 runtime 검증 v2

동한 원격 기준은 `7860043228c81aec517c5a1966d475d36e12f68a`다.
이 제공본의 후속 연동·v2 학습 코드는 로컬 수정이며 아직 원격에 반영되지 않았다.

프로젝트 실행 root는 **`pac-mission1-shared/`**다. 생성기와 팀 runtime은
각각 별도 checkout으로 준비한다. 최신 실행 절차는
[v2 학습·검증 가이드](pac-mission1-shared/docs/model_training_v2_ko.md)에 있다.

| 경로 | 용도 |
|---|---|
| `pac-mission1-shared/scripts/donghan/model_pipeline.py` | generate → collect → train → evaluate |
| `pac-mission1-shared/config/model_development.yaml` | 36 시나리오/864 원본 박스 실행 설정 |
| `pac-mission1-shared/config/model_benchmark.yaml` | 180 시나리오/14,400 원본 박스로 확대하는 설정 |
| `pac-mission1-shared/models/candidate_runtime_v2.json` | validation으로 선택한 실험 후보; 기본 모델을 대체하지 않음 |
| `pac-mission1-shared/config/candidate_runtime_v2.yaml` | 제공 후보의 일치하는 planner 설정 |
| `pac-mission1-shared/docs/model_training_v2_results_ko.md` | 실제 학습·검증 수치와 미검증 범위 |
| `TRAINING_GUIDE_KO.md` | 이전 96박스 실험의 이력 문서 |

이번 기준 팀장은 `81d0333ba6550d9ee6f02661d8b8d9e79beaca6c`, 생성기는
`cc4c075daa3dd4c7f80510042732763fc9502933`다. 팀장의 새 로봇 받침대 배치에
맞춘 `robot_check_gazebo.yaml`을 Python runtime 평가에 사용한다.

패치 적용은 배포 ZIP의 `README_APPLY_KO.md`를 따른다. 원격 786004 기준
누적 패치와 이전 후속 제공본 기준 증분 패치는 **둘 중 하나만** 적용한다.
팀 runtime의 `ranker_config` 연결 패치는 팀장 checkout에 별도로 적용한다.
옛 `from_remote_146797e.patch`는 786004에 포함된 이력이며 다시 적용하지 않는다.

PPO의 proxy+DBLF value-provider/버퍼 4칸 계약은 유지한다. 학습·평가는
Python runtime 시뮬레이션이며 ROS2 Humble·MoveIt·Gazebo·실제 pick/place
실행 결과는 아니다. 단위는 m/kg/N/rad다.
