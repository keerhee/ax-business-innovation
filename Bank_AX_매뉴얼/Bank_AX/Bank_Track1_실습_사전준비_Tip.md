# Bank Track1 실습 사전 준비 Tip

W1~W6 실습을 진행하기 전에 필요한 환경 설정과 외부 서비스 연동 가이드입니다. 각 주차 실습가이드(`Bank_Track1_W*_실습가이드.html`)와 함께 참고하세요.

원본 문서: [Tip (1).docx](Tip%20%281%29.docx)

---

## 1. 실습 파일(.json) Import

각 주차 폴더(`W1 실습/` ~ `W5 실습/`)에 들어 있는 `.json` 파일을 n8n으로 가져옵니다.

1. 제공된 실습 파일(`W*.json`) 다운로드
2. n8n에서 **Create workflow** 클릭
3. **Import from file** 선택 → 1번에서 받은 `.json` 파일 지정

---

## 2. Google OAuth2 인증 (Sheets / Gmail / Calendar)

n8n 노드에서 **Sign in with Google** 만으로 즉시 연결 가능한 서비스:

- Google Sheets
- Gmail
- Google Calendar

각 노드의 Credential에서 `Sign in with Google` 버튼을 누르고 본인 Google 계정으로 인증하면 됩니다.

---

## 3. Google Cloud Console로 OAuth 클라이언트 직접 발급 (Drive / Docs 등)

`Google Drive`, `Google Docs` 같이 추가 권한이 필요한 라이브러리는 **Google Cloud Console**에서 직접 OAuth 클라이언트를 만들어야 합니다.

### 3-1. Google Cloud Console 작업

1. [Google Cloud Console](https://console.cloud.google.com/) 접속
2. **새 프로젝트 생성** → 프로젝트 선택
3. **API 및 서비스 → 사용자 인증 정보 → 사용자 인증 정보 만들기**
4. 입력값
   - **애플리케이션 유형**: `웹 애플리케이션`
   - **이름**: 임의의 애플리케이션 이름
   - **승인된 리디렉션 URI**: `https://oauth.n8n.cloud/oauth2/callback`
5. 발급된 **Client ID**와 **Client Secret** 복사
6. **OAuth 동의 화면 → 테스트 사용자 추가**: 본인 Google 계정 추가

### 3-2. n8n에 등록

n8n 해당 노드의 Credential 화면에서:

| Google Cloud Console | n8n Credential |
|----------------------|----------------|
| 클라이언트 ID | Client ID |
| 클라이언트 보안 비밀번호 | Client Secret |

값을 입력한 뒤 **OAuth 인증** 버튼을 눌러 연결을 마칩니다.

---

## 4. Slack Webhook 생성

> 메시지를 보낼 **각 채널별로** 아래 1~3을 반복합니다.

1. Slack에서 **채널 세부 정보 열기**
2. **앱 추가**
3. **앱 설치** (Incoming Webhooks 등)
4. 발급된 Webhook URL을 n8n Slack/HTTP Request 노드의 URL에 입력

> ⚠️ **보안 주의**: Webhook URL은 곧 인증입니다. 외부에 공개되지 않도록 주의하고, 실수로 노출되면 즉시 폐기·재발급하세요.

---

## 5. OpenAI API Key 발급

1. [OpenAI Platform](https://platform.openai.com/api-keys) 에서 **API Key 발급**
2. **API Key는 최초 생성 시에만 전문 확인 가능** → 안전한 장소에 보관
3. **Billing**
   - 충전된 금액(Credit) 만큼 API 호출 가능
   - 모델별로 토큰당 비용이 다르므로 사용량에 따라 Credit 소진 속도가 달라짐

---

## 6. Qdrant 벡터 DB (RAG 실습용)

추가 학습(RAG) 실습에서 사용하는 벡터 DB입니다.

1. [Qdrant Cloud](https://cloud.qdrant.io/) 계정 생성 후 **클러스터 생성**
2. 클러스터 생성 직후 자동 발급되는 **API Key**는 한 번만 전문 확인 가능 → 반드시 안전하게 보관
3. **Cluster Endpoint** 도 함께 메모해두기 (둘 다 n8n Credential에 필요)
4. **Collection 생성** (벡터 저장 단위)
5. n8n Qdrant 노드의 Credential에 **API Key**와 **Cluster Endpoint** 입력

---

## 7. 워크플로우 색상 코딩 시스템

n8n 캔버스에서 노드를 색상으로 구분합니다.

| 색상 | 역할 |
|------|------|
| 🔵 파란색 | 데이터 입력 / 수집 노드 |
| 🟢 초록색 | 처리 / 변환 노드 |
| 🟡 노란색 | 조건 / 분기 노드 |
| 🔴 빨간색 | 알림 / 에러 처리 노드 |
| 🟣 보라색 | 외부 API 호출 노드 |

워크플로우를 만들 때 이 컨벤션을 따르면 흐름 파악이 쉬워집니다.

---

## 8. n8n 셀프 호스팅 (Docker Desktop)

### 셀프 호스팅의 장점

- 데이터 보안 / 프라이버시
- 워크플로우 호출량 제한 없음
- 비용 절감
- 커스텀 노드 사용 가능

### 8-1. Docker Desktop 설치

- Windows: Docker Desktop for Windows
- macOS: Docker Desktop for Mac

### 8-2. n8n 컨테이너 실행

1. **n8n Image Pull**: `docker pull n8nio/n8n`
2. **n8n Container Run**: 다음 옵션을 설정해 실행

| 옵션 | 의미 |
|------|------|
| Host : Container | 내 컴퓨터(호스트)와 도커 내부 가상 공간 |
| Port | 내 컴퓨터의 포트를 컨테이너의 `5678` 포트로 연결 |
| Volumes | 컨테이너 삭제 시에도 데이터를 유지하기 위해 내 컴퓨터 경로를 연결 |
| Environment variables | 컨테이너 실행 시 참조할 환경설정 변수 |

> 자세한 설정은 [n8n 공식 Docker 문서](https://docs.n8n.io/hosting/installation/docker/) 참고.

### 8-3. GUI 접속

- 브라우저에서 `http://localhost:5678` 접속
- 최초 접속 시 계정 생성 후 워크플로우 작업 가능

---

## 9. Gmail 바닥글 "n8n" 문구 제거

n8n에서 Gmail 노드로 메일을 보내면 본문 하단에 다음 문구가 자동으로 붙습니다:

```
---
This email was sent automatically with n8n
```

이 문구를 제거하려면 Gmail 노드 옵션에서:

1. **Add option** 클릭
2. `Append n8n Attribution` 항목 추가
3. 기본값 **True → False** 로 변경

---

## 참고: 키 관리 체크리스트

| 항목 | 발급 위치 | 주의사항 |
|------|----------|----------|
| Google OAuth Client ID/Secret | Google Cloud Console | 리디렉션 URI를 `https://oauth.n8n.cloud/oauth2/callback`로 정확히 입력 |
| Slack Webhook URL | Slack 채널 → 앱 추가 → Incoming Webhooks | URL 자체가 인증, 노출 시 즉시 폐기 |
| OpenAI API Key | platform.openai.com | 발급 직후만 전문 확인 가능, Credit 잔액 모니터링 |
| Qdrant API Key + Endpoint | cloud.qdrant.io | API Key는 발급 직후만 확인 가능 |

발급한 모든 키는 **GitHub 등 공개 저장소에 절대 commit하지 말 것**. 실습 `.json` 파일에 키가 들어 있다면 placeholder로 교체 후 공유하세요.
