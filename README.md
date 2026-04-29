# AX 업무혁신 (Bank AX Training)

은행권 AX(AI Transformation) 업무혁신 교육 과정의 실습 자료 모음입니다. 주차별 워크플로우 자동화 실습, RAG 기반 추가 학습 자료, AX 매뉴얼을 포함합니다.

🌐 **온라인 강의노트**: https://keerhee.github.io/ax-business-innovation/

## 디렉터리 구조

| 폴더 | 설명 |
|------|------|
| [manuals/](manuals) | Bank Track1 AX 업무혁신 본 매뉴얼 + W1~W6 / RAG 실습가이드 (HTML) + 사전 준비 Tip + 원본 docx |
| [W1 실습/](W1%20실습) | Week 1 실습 — 기본 워크플로우 (JSON, 실습 시트, 스크린샷) |
| [W2 실습/](W2%20실습) | Week 2 실습 — 이메일 분류 (경미/주의/위험) |
| [W3 실습/](W3%20실습) | Week 3 실습 — 여신심사 / 대출 신청 접수 / 캘린더 연동 |
| [W4 실습/](W4%20실습) | Week 4 실습 — 자동 이메일 응답 워크플로우 |
| [W5 실습/](W5%20실습) | Week 5 실습 — 결재 흐름 (자동승인/팀장승인/본부위임) + Slack 연동 |
| [추가 학습(RAG)/](추가%20학습\(RAG\)) | RAG 기반 추가 학습 자료 (Qdrant 임베딩, RAG Trigger, 금융기관 여신운용세칙 PDF) |

## 매뉴얼 (`manuals/`)

| 파일 | 설명 |
|------|------|
| `Bank_Track1_AX_main_v3.html` | 본 매뉴얼 (커리큘럼 전체 개요) |
| `Bank_Track1_prereq_tip.html` | 실습 사전 준비 Tip (n8n / OAuth / Slack / OpenAI / Qdrant / Docker) |
| `Bank_Track1_W1_guide.html` ~ `Bank_Track1_W6_guide.html` | 주차별 실습가이드 |
| `Bank_Track1_RAG_guide.html` | 추가학습(RAG) 실습가이드 |
| `Tip_source.docx` | 사전 준비 Tip 원본 docx |

## 파일 형식

- `*.json` — 워크플로우 정의 파일 (n8n 등 자동화 도구로 import)
- `*.xlsx` — 실습용 데이터 시트
- `*.png` — 화면 예시 / 스크린샷
- `*.pdf`, `*.docx` — 참고 문서 / 양식

## 사용 방법

1. [강의노트 메인](https://keerhee.github.io/ax-business-innovation/)에서 본 매뉴얼과 사전 준비 Tip을 읽습니다.
2. 각 주차의 실습가이드 HTML로 흐름을 이해한 뒤,
3. 해당 주차 폴더의 `W*.json`을 n8n에 import → 시트/이미지로 동작을 검증합니다.
