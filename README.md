# 황민서 | Backend · AI Backend

AI 모델을 서비스에 연결하고, 실패했을 때의 처리 흐름까지 만드는 개발자입니다.
반도체 검사 프로그램의 추론 연동, 금융 AI 감사 챗봇, 티켓 예약·결제 백엔드 개발에 참여했습니다.

[GitHub](https://github.com/MinseoHwang) · [실무 경험](experience/nexusone.md) · [FinAudit](projects/finaudit/README.md) · [Remy](projects/remy/README.md)

## 기술

| 영역 | 프로젝트에서 사용한 기술 |
| --- | --- |
| Backend | Java · Spring Boot · Python · FastAPI |
| Data · AI | PostgreSQL · pgvector · RAG · LangGraph |
| 모델·추론 연동 | PyTorch · ONNX Runtime · TensorRT · C++/MFC |

## 실무 경험

**넥서스원 · 반도체 검사 AI** | 2025.02.03 – 2025.07.31

- 웨이퍼 결함 이미지 전처리·라벨 정리, 클래스 불균형 대응과 분류 모델 실험.
- C++/MFC 검사 프로그램에 ONNX Runtime 추론 연동, 기존 CSV 정보를 유지하며 분류 결과 기록.
- PyTorch → ONNX → TensorRT FP16 변환과 추론 호출 시간 측정.

[업무 상세 →](experience/nexusone.md)

## 프로젝트

| 프로젝트 | 서비스와 다룬 문제 | 주요 기술 |
| --- | --- | --- |
| [FinAudit](projects/finaudit/README.md) | 금융 AI 감사 플랫폼 · 답변 근거 검증과 분석·보고서 실행 제어 | Python · FastAPI · Spring Boot · pgvector |
| [Remy](projects/remy/README.md) | 해외 스포츠 티켓 예약·결제 · 결제 결과 확인과 환불·재고 처리 | Java · Spring Boot · PostgreSQL |
| [Melpik](projects/melpik/README.md) | 의류 대여 서비스 · 이용권 차감·취소 복원과 상품 검수·적재 | TypeScript · NestJS · MySQL · Python |
| [AutoUpload](projects/autoupload/README.md) | 콘텐츠 제작·승인·게시 자동화 · 중단 후 재개와 게시 결과 확인 | Python · LangGraph · SQLite |

## 대표 기여

**FinAudit — 감사 챗봇·분석 API 연동**

- 질문의 임계값 `0.5`를 근거 없는 수치로 잘못 판정하던 검증을 수정하고 회귀 테스트를 추가했습니다.
- 분석과 보고서의 실행 한도를 분리하고, 대기 한도 초과 시 `503`으로 응답하도록 처리했습니다.
- 팀원의 SHAP 분석 API에 보고서·S3 저장을 확장하고, 저장 실패에도 분석 응답을 유지하도록 보강했습니다.

[공개 코드](https://github.com/kt-aivle-big-project-13/ai-repo) · [답변 검증 PR](https://github.com/kt-aivle-big-project-13/ai-repo/pull/57) · [실행 제한 PR](https://github.com/kt-aivle-big-project-13/ai-repo/pull/95)

**Remy — 결제수단 확장·환불 연동**

- 카드·실시간 계좌결제가 공통 승인·조회·환불 흐름을 사용하도록 확장하는 데 기여했습니다.
- 고객·관리자 환불 진입점 연결과 관리자 대사 상태 표시에 기여했습니다.

[본인 기여와 프로젝트 구현 범위 →](projects/remy/README.md)

## 기술 사례

| 사례 | 설명하는 판단 |
| --- | --- |
| [감사 답변의 인용·수치 검증](projects/finaudit/evidence-validation.md) | 질문에서 온 숫자와 근거 없는 수치를 어떻게 구분할 것인가 |
| [분석·보고서 실행 한도 분리](projects/finaudit/execution-limits.md) | 무거운 작업이 서로의 실행 슬롯을 점유하지 않게 하는 방법 |
| [결제 응답 유실 후 조회 복구](projects/remy/payment-recovery.md) | 성공 여부를 모를 때 재승인 대신 거래 조회로 확인하는 이유 |
| [공급 실패 환불과 재고](projects/remy/refund-inventory.md) | 확보하지 못한 티켓을 다시 판매하지 않도록 하는 재고 정책 |

## 교육·수상·자격

- **명지대학교 졸업** · 2025.02
- **KT AIVLE School 9기 AI 트랙 수료** · 840시간, Agentic AI·RAG·LLMOps 학습
- **Dean’s List 우수수료생** · 개인 수상
- **KT AIVLE School 빅프로젝트 우수상** · FinAudit 팀 수상
- **AICE Associate** · 2026.04 취득
