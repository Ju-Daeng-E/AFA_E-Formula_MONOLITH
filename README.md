# A-FA Telemetry System

A-FA Telemetry System은 Node.js (Express + Socket.IO), Nginx를 이용해 원격 계측(텔레메트리) 데이터 수집, 그리고 로그 기록 및 리뷰를 제공하는 통합 시스템입니다.

---

## 주요 기능

- **원격 계측 (Telemetry)**
  - ESP32, ECU 등에서 전송한 데이터를 Node.js 서버가 실시간으로 수신합니다.
  - Socket.IO를 통해 클라이언트에 데이터를 중계하며, 로그 파일로 기록할 수 있습니다.

- **로그 기록 및 리뷰(미완성)**
  - log파일 변환을 위한 JSON 및 CSV 파일 다운로드 기능을 제공합니다.

- **Nginx Reverse Proxy**
  - Nginx는 80(HTTP) 및 443(HTTPS) 포트를 통해 SSL 처리를 하고, 내부적으로 Node.js 서버(예: 7777 포트)로 요청을 프록시합니다.
  - API, Socket.IO 등 필요한 경로를 프록시하여 통합 환경을 구성합니다.

## 사용 방법

### 1. 원격 계측 디바이스 연결
- **디바이스** (예: ESP32, ECU 등)는 아래 URL을 통해 소켓 연결을 수행합니다:
```
wss://afa2024.ooguy.com/socket.io/?channel=afa&key=1234&device=true
```

- 디바이스는 `tlog` 이벤트로 데이터를 전송하며, 서버는 이를 실시간으로 클라이언트에 중계하고 로그 파일로 기록합니다.

### 2. 실시간 모니터링 페이지
- 브라우저에서 **`https://afa2024.ooguy.com/live.html`** 에 접속하여 실시간 텔레메트리 데이터를 확인합니다.
- 페이지 내 “로그 기록 시작” 및 “로그 기록 정지” 버튼을 통해 별도의 로그 파일 기록을 제어할 수 있습니다.

### 3. 로그 리뷰 페이지
- JSON 및 CSV 형식으로 로그 데이터를 다운로드할 수 있는 기능이 제공됩니다.

