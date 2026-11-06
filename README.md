# 소개

AI 응답을 서비스에 연결하고, 외부 시스템의 결과가 불확실할 때 처리 흐름을 만드는 개발자입니다.
RAG 기반 금융 AI 감사 챗봇 구현, TypeScript·NestJS 서비스 개발, 결제 API 연동과 반도체 결함 분류 AI 개발에 참여했습니다.

[GitHub](https://github.com/MinseoHwang) · [넥서스원 실무](experience/nexusone.md) · [FinAudit](projects/finaudit/README.md) · [Remy](projects/remy/README.md) · [Melpik](projects/melpik/README.md) · [인스타그램 자동 업로드](projects/autoupload/README.md)

## 기술

| 영역 | 프로젝트에서 사용한 기술 |
| --- | --- |
| API와 서비스 | TypeScript · NestJS · Python · FastAPI · Java · Spring Boot |
| AI와 데이터 | LLM API · RAG · LangGraph · PostgreSQL · pgvector · MySQL · SQLite |
| 모델과 추론 연동 | PyTorch · ONNX Runtime · TensorRT · C++/MFC |
| 실행 환경과 협업 | Docker · AWS S3 · Git · GitHub |

## 대표 구현과 문제 해결

**FinAudit RAG 기반 감사 챗봇**

감사 지표·법령·보고서 근거를 활용해 질문에 답하는 챗봇을 구현했습니다. pgvector 법령 검색과 LLM API를 연결하고, 답변에 실제 사용한 근거를 함께 제공했습니다. 근거가 없으면 호출을 생략하고, 응답의 인용 번호와 소수 수치를 검증했습니다.

[챗봇 기능과 연동 흐름](projects/finaudit/README.md) · [본인 구현 PR #57](https://github.com/kt-aivle-big-project-13/ai-repo/pull/57)

다음은 기능 구현 과정에서 다룬 문제와 판단입니다.

| 상황 | 변경과 판단 | 상세 |
| --- | --- | --- |
| 질문에서 가져온 `0.5`까지 근거 없는 숫자로 판정 | 질문을 소수 수치 대조 범위에 포함하고 검증 분기 회귀 테스트 추가 | [FinAudit 답변 검증](projects/finaudit/evidence-validation.md) |
| 분석과 PDF 생성 요청이 겹쳐 무거운 작업이 중첩 | 작업별 실행 한도를 분리하고 대기 초과를 `503`으로 처리 | [FinAudit 실행 제어](projects/finaudit/execution-limits.md) |
| 실시간 계좌결제를 기존 결제 흐름에 추가 | 승인·조회·환불 흐름을 확장하고 외부 응답의 주문·금액·수단 대조 | [Remy 본인 기여](projects/remy/README.md) |
| 마지막 이용권 회차 사용 후 예약 취소 | 사용 이력·유효기간·종료 기록으로 복원 대상과 중복 복원을 구분 | [Melpik 이용권 처리](projects/melpik/README.md) |

## 실무 경험

**넥서스원 | 반도체 결함 분류 AI 개발·검사 프로그램 연동** · 2025.02.03 – 2025.07.31

- 클래스 불균형에 대응해 가중치·샘플링·손실함수를 실험하고 클래스별 평가와 CAM으로 분류 양상을 비교했습니다.
- C++/MFC 검사 프로그램에 ONNX Runtime 추론을 연결하고, 기존 CSV 검사 정보를 유지한 채 분류 결과·확률을 기록했습니다.
- 모델 형식을 비교한 내부 실험에서 이미지당 평균 추론 호출 시간을 PyTorch **6.222ms → TensorRT FP16 1.916ms**로 줄였습니다. 검사장비 전체 처리시간과 구분한 값입니다.

[문제와 구현 상세](experience/nexusone.md)

## 프로젝트

| 프로젝트 | 서비스와 담당 경험 | 주요 기술 |
| --- | --- | --- |
| [FinAudit](projects/finaudit/README.md) | 금융 AI 감사 플랫폼 · RAG 기반 감사 챗봇 구현, 답변 근거 제공·검증, 보고서 저장과 실행 제어 | Python · FastAPI · Spring Boot · pgvector |
| [Remy](projects/remy/README.md) | 해외축구 VIP 티켓 판매 사이트 · 실시간 계좌결제 확장, 환불 진입점·관리자 대사 상태 연결 | Java · Spring Boot · PostgreSQL |
| [Melpik](projects/melpik/README.md) | 의류 대여 서비스 · 이용권 차감·취소 복원, 상품 수집·검수 적재 | TypeScript · NestJS · MySQL · Python |
| [해외축구 이슈·유소년 홍보용 인스타그램 자동 업로드](projects/autoupload/README.md) | 콘텐츠 제작·검수·승인·게시 자동화 · 중단 후 재개와 게시 결과 확인 | Python · LangGraph · SQLite |

## 설계 사례

- [질문의 숫자와 모델이 생성한 숫자를 구분하는 검증](projects/finaudit/evidence-validation.md)
- [분석과 보고서가 서로의 실행 슬롯을 점유하지 않도록 한 제어](projects/finaudit/execution-limits.md)
- [결제 응답이 없을 때 재승인 대신 거래 조회로 확인하는 구조](projects/remy/payment-recovery.md)
- [공급 실패로 환불한 티켓이 다시 판매되지 않도록 하는 재고 정책](projects/remy/refund-inventory.md)

Remy 설계 사례는 프로젝트의 구현 설명입니다. 본인 작성 이력이 확인된 기여는 Remy 개요에서 구분했습니다.

## 교육과 수상

- **명지대학교 졸업** · 2025.02
- **KT AIVLE School 9기 AI 트랙 수료** · 840시간, Agentic AI·RAG·LLMOps 학습
- **KT AIVLE School Dean’s List 우수수료생 선정** · 개인
- **KT AIVLE School 빅프로젝트 우수상** · FinAudit 팀
- **AICE Associate** · 2026.04.25 취득
