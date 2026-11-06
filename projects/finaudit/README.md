# FinAudit 금융 AI 감사 플랫폼

[프로필로 돌아가기](../../README.md)

신용평가 AI의 설명가능성·공정성 분석 결과를 보고서와 질의응답으로 확인하는 팀 프로젝트입니다. 저는 LLM 응답 검증, 분석 결과와 보고서 저장의 연결, 무거운 작업의 실행 제어에 기여했습니다.

| 항목 | 내용 |
| --- | --- |
| 개발 활동 | 2026.07.10 – 2026.08.20, 확인 가능한 본인 PR 활동 기준 |
| 역할 | AI·백엔드 개발 참여 |
| 주요 기술 | Python · FastAPI · Java · Spring Boot · PostgreSQL/pgvector · AWS S3 |
| 수상 | KT AIVLE School 빅프로젝트 우수상 · 팀 |
| 코드 | [AI 저장소](https://github.com/kt-aivle-big-project-13/ai-repo) · [백엔드 저장소](https://github.com/kt-aivle-big-project-13/backend-repo) |

## 담당 기능과 연동 흐름

지표·법령·보고서 근거를 LLM API에 전달하고, 응답의 인용 번호와 소수 수치를 검증했습니다. 근거가 없으면 호출을 생략하고, 답변에 실제 사용한 인용만 반환하도록 구성했습니다.

```text
질문 → 지표·법령·보고서 근거 조회 → LLM API → 인용·소수 수치 검증
                      │
                      └─ 근거 없음 → 호출 생략

분석 요청 → 기존 분석 API → 분석 결과
                  └─ 보고서 payload·S3 저장 → 저장 실패 격리
```

기존 SHAP 분석 API는 팀원이 구현했습니다. 제가 확장한 부분은 보고서 payload·S3 저장 연동, 챗봇 검증, 분석·보고서 실행 제어 등입니다.

## 질문에서 가져온 숫자를 오류로 처리하던 문제

“임계값을 0.5로 바꾸면?”이라는 질문에서 가져온 `0.5`까지 근거 없는 수치로 판정했습니다. 답변의 소수를 감사 근거뿐 아니라 질문과도 대조하도록 수정하고 회귀 테스트를 추가했습니다. [문제·변경·검증 상세](evidence-validation.md) · [PR #57](https://github.com/kt-aivle-big-project-13/ai-repo/pull/57)

## 분석 결과를 유지하면서 보고서 저장 확장

팀원의 분석 API 위에 보고서에 필요한 payload와 S3 저장을 추가했습니다. 기존 호출자가 받는 분석 응답을 유지하고, 저장 실패가 분석 결과의 소실로 이어지지 않도록 격리했습니다. 이후 S3의 기존 SHAP 결과를 재사용하고 조회 실패 시 재계산하는 경로를 추가했습니다. [PR #29](https://github.com/kt-aivle-big-project-13/ai-repo/pull/29) · [PR #93](https://github.com/kt-aivle-big-project-13/ai-repo/pull/93)

법령 검색에서는 pgvector 유사도 검색과 검색 실패 격리를 다뤘습니다. 검색 결과를 챗봇의 근거로 연결하는 역할입니다. [백엔드 PR #202](https://github.com/kt-aivle-big-project-13/backend-repo/pull/202)

## 무거운 분석과 PDF 생성의 실행 한도 분리

분석과 보고서 생성이 동시에 자원을 점유하므로 작업별 실행 한도를 분리했습니다. 대기 한도 초과 시 `503`으로 응답하고 예외 발생 후에도 슬롯을 반환하도록 처리했습니다. [선택 이유와 적용 범위](execution-limits.md) · [PR #95](https://github.com/kt-aivle-big-project-13/ai-repo/pull/95)

## 검증

- 답변 검증은 LLM 응답을 가정한 단위 테스트로 인용·소수 판정 분기를 확인했습니다. 실제 모델의 환각 발생률을 측정한 결과와 구분합니다.
- 실행 제어 테스트는 허용량 초과·대기 초과·예외 후 슬롯 반환·HTTP 상태 매핑을 다룹니다.
- 배포 환경의 응답속도·메모리 개선률이나 상용 트래픽 성과는 제시하지 않습니다.
