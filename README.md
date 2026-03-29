# OpenClaw Windows 데스크탑 가이드

## 1. 전체 인터페이스 구조

```
┌──────────────────────────────────────────────────────────────────────┐
│                         사용자 (User)                                 │
└──────────────────────────────────────────────────────────────────────┘
                               ↓
                     【메시지 입력 / 명령】
                               ↓
┌──────────────────────────────────────────────────────────────────────┐
│               📱 채널 (Channels) - 메시지 인터페이스                   │
├──────────────────────────────────────────────────────────────────────┤
│                                                                      │
│   • Discord      - 텍스트 기반 메시지                               │
│   • Telegram     - 채팅 앱 통합                                     │
│   • Slack        - 업무 협업 도구                                   │
│   • Signal       - 암호화 메시징                                    │
│   • WhatsApp     - 메시지 송수신                                    │
│   • CLI/Terminal - 로컬 명령어 입력 (Windows PowerShell/CMD)        │
│                                                                      │
└──────────────────────────────────────────────────────────────────────┘
                               ↓
            【Gateway - OpenClaw 라우팅 & 수신 대기】
                               ↓
┌──────────────────────────────────────────────────────────────────────┐
│               🖥️  OpenClaw Gateway (로컬 서버)                       │
├──────────────────────────────────────────────────────────────────────┤
│                                                                      │
│   • 포트: 18789 (기본값)                                             │
│   • 로컬 접속 URL: http://localhost:18789                           │
│   • 역할: 채널에서 메시지 수신                                       │
│   • 기능: 라우팅, 인증, 응답 반환                                    │
│   • 상태: openclaw gateway start/stop/restart                      │
│   • 설정: ~/.openclaw/config.yml                                   │
│                                                                      │
└──────────────────────────────────────────────────────────────────────┘
                               ↓
            【메시지 분석 & 도구 선택】
                               ↓
┌──────────────────────────────────────────────────────────────────────┐
│             🧠 AI Agent (Claude/GPT/etc via OpenClaw)               │
├──────────────────────────────────────────────────────────────────────┤
│                                                                      │
│   선택 가능 모델:                                                    │
│   • Claude 3.x+  (Provider: Anthropic)   - 기본 모델                │
│   • GPT-4.x      (Provider: OpenAI)      - 고성능                  │
│   • Gemini 2.x   (Provider: Google)      - 멀티모달               │
│   • Llama 2.x+   (Provider: Meta/Ollama) - 로컬 모델              │
│   • 기타 모델    (Provider: 다양)        - 커스텀                 │
│                                                                      │
│   역할: 사용자 의도 파악 → 적절한 도구 선택 → 작업 실행              │
│                                                                      │
└──────────────────────────────────────────────────────────────────────┘
                               ↓
            【사용 가능한 도구 선택 & 실행】
                               ↓
┌──────────────────────────────────────────────────────────────────────┐
│                 ⚙️  도구 (Tools) - 작업 실행                         │
├──────────────────────────────────────────────────────────────────────┤
│                                                                      │
│   파일 작업:                                                        │
│   • read      - 파일 읽기                                           │
│   • write     - 파일 생성/쓰기                                      │
│   • edit      - 파일 편집 (정확한 텍스트 교체)                      │
│                                                                      │
│   시스템 작업:                                                      │
│   • exec      - 터미널 명령 실행 (shell)                           │
│   • process   - 백그라운드 작업 관리                                │
│                                                                      │
│   인터넷 & 통신:                                                    │
│   • web_search   - 웹 검색 (DuckDuckGo)                            │
│   • web_fetch    - 웹페이지 내용 추출                              │
│   • sessions_*   - 다른 세션과 메시지 송수신                       │
│                                                                      │
│   기타:                                                             │
│   • memory_*     - 메모리 저장/검색                                │
│   • image        - 이미지 분석                                      │
│                                                                      │
└──────────────────────────────────────────────────────────────────────┘
                               ↓
             【Windows 데스크탑에서 실제 작업 수행】
                               ↓
┌──────────────────────────────────────────────────────────────────────┐
│          💻 Windows 로컬 리소스 (Desktop/Files/System)               │
├──────────────────────────────────────────────────────────────────────┤
│                                                                      │
│   • 파일 시스템      - 문서, 프로젝트 폴더                          │
│   • 터미널           - PowerShell, CMD, Git Bash                   │
│   • 프로세스         - 앱 실행, 백그라운드 작업                     │
│   • 시스템 설정      - 환경변수, 포트 설정                         │
│   • 네트워크         - 로컬호스트 서버, API 호출                   │
│                                                                      │
└──────────────────────────────────────────────────────────────────────┘
                               ↓
                    【결과 반환 & 표시】
                               ↓
┌──────────────────────────────────────────────────────────────────────┐
│             📤 응답 (Response) - 사용자에게 반환                      │
├──────────────────────────────────────────────────────────────────────┤
│                                                                      │
│   • 일반 텍스트      - 설명, 정보 제공                              │
│   • 코드 블록        - 스크립트, 명령어                             │
│   • 파일 내용        - 읽은 파일 표시                              │
│   • 실행 결과        - 터미널 출력 결과                            │
│   • 상태 정보        - 성공/실패 메시지                            │
│                                                                      │
└──────────────────────────────────────────────────────────────────────┘
                               ↓
                     【채널로 메시지 반환】
                               ↓
┌──────────────────────────────────────────────────────────────────────┐
│               💬 사용자 화면 (Discord/Telegram/CLI 등)               │
└──────────────────────────────────────────────────────────────────────┘
```

---

## 2. 사용자가 할 수 있는 것 vs 하기 어려운 것

### ✅ 쉽게 할 수 있는 것 (기본 기능)

#### 설정 변경
- [ ] **AI 모델 변경** (`/model claude-opus` 등)
- [ ] **채널 변경** (Discord → Telegram 등)
- [ ] **언어 설정** (English/한국어)
- [ ] **시간대 설정** (Timezone)
- [ ] **로깅 레벨** (INFO/DEBUG/ERROR)

#### 파일 작업
- [ ] **파일 읽기** (마크다운, 코드, 텍스트)
- [ ] **파일 생성** (새로운 문서 작성)
- [ ] **파일 편집** (기존 파일 수정)
- [ ] **파일 삭제** (정리)
- [ ] **폴더 탐색** (디렉토리 구조 파악)

#### 코드 & 자동화
- [ ] **Python 스크립트 실행**
- [ ] **Shell 명령어 실행** (PowerShell, CMD)
- [ ] **배치 파일 실행**
- [ ] **Git 명령** (커밋, 푸시, 풀 등)
- [ ] **환경 변수 설정**

#### 정보 수집
- [ ] **웹 검색** (DuckDuckGo)
- [ ] **웹페이지 내용 추출** (URL 입력)
- [ ] **시스템 정보 조회** (버전, 설정 등)
- [ ] **프로세스 관리** (앱 시작/종료)

#### 커뮤니케이션
- [ ] **다중 채널 메시지 송수신** (동시에 여러 채널 사용)
- [ ] **특정 세션에 메시지 보내기**
- [ ] **메모리 저장/검색**

---

### ⚠️ 하기 어렵거나 불가능한 것 (제한사항)

#### GUI 상호작용
- [ ] ❌ **마우스 클릭** (자동화 어려움)
- [ ] ❌ **창 제어** (윈도우 열기/닫기)
- [ ] ❌ **스크린샷 캡처** (이미지 분석용은 가능, 자동 캡처는 어려움)
- [ ] ❌ **드래그 앤 드롭** (GUI 자동화 없음)

#### 권한 제한
- [ ] ❌ **시스템 레지스트리 수정** (위험)
- [ ] ❌ **관리자 권한 필요한 작업** (보안)
- [ ] ⚠️  **네트워크 설정 변경** (보안 정책)
- [ ] ❌ **방화벽 설정 수정** (관리자 인증 필요)

#### 보안 관련
- [ ] ❌ **API 키/토큰 관리** (외부 저장소만)
- [ ] ❌ **비밀번호 입력** (자동화되지 않음)
- [ ] ❌ **암호화된 파일 직접 수정** (암호 해제 필요)

#### 성능 제한
- [ ] ⚠️  **대용량 파일 처리** (메모리 제한)
- [ ] ⚠️  **실시간 모니터링** (네트워크 지연)
- [ ] ❌ **높은 CPU/GPU 작업** (로컬 리소스 한정)

#### 외부 의존성
- [ ] ⚠️  **설치되지 않은 프로그램 실행** (사전 설치 필요)
- [ ] ⚠️  **특정 라이브러리/패키지** (Python, Node.js 등 필수)
- [ ] ❌ **라이센스 필요한 소프트웨어** (구매/인증 필요)

#### 네트워크/API
- [ ] ⚠️  **느린 인터넷 환경** (타임아웃 가능)
- [ ] ⚠️  **API 속도 제한** (Rate limiting)
- [ ] ❌ **오프라인 환경** (인터넷 필수)

---

## 3. OpenClaw Windows 매뉴얼 초안

### 📘 OpenClaw Windows 데스크탑 가이드

#### 소개

OpenClaw는 Windows 데스크탑에서 AI 에이전트를 로컬로 실행할 수 있는 오픈소스 도구입니다.
사용자는 자연어로 명령을 내리면, AI가 파일 작업, 코드 실행, 웹 검색 등을 자동으로 처리합니다.

**주요 특징:**
- 🤖 AI 기반 자동화 (Claude, GPT-4 등)
- 📁 파일 시스템 접근 및 조작
- ⚙️ 터미널 명령 자동 실행
- 📱 멀티 채널 지원 (Discord, Telegram, CLI 등)
- 🔒 로컬 실행 (개인정보 보호)

---

### 🚀 빠른 시작

#### 1단계: 설치

```bash
# Windows PowerShell (관리자 권한)
# 1. Homebrew for Windows 설치 (또는 직접 다운로드)
# 2. OpenClaw 설치
brew install openclaw

# 또는 직접 설치
https://github.com/openclaw/openclaw#installation
```

#### 2단계: 초기 설정

```bash
# OpenClaw 상태 확인
openclaw status

# Gateway 시작
openclaw gateway start

# 로그 확인
openclaw gateway log
```

#### 3단계: 첫 메시지 보내기

**Discord를 통해:**
```
@OpenClaw 안녕! "C:\Users\YourName\Documents" 폴더 구조를 보여줘
```

**CLI를 통해:**
```bash
openclaw message "내 데스크탑의 모든 파일을 나열해줘"
```

---

### 📋 기본 사용법

#### AI 모델 변경

```bash
# 현재 설정 확인
openclaw config show

# 모델 변경
openclaw config set model=gpt-4o
openclaw config set model=claude-opus
openclaw config set model=gemini

# 로컬 모델 사용 (Ollama)
openclaw config set model=ollama/llama2
```

#### 채널 추가 & 관리

```bash
# Discord 연동
openclaw channel add discord
openclaw channel connect discord

# CLI 사용 준비
openclaw channel add cli

# Telegram 연동
openclaw channel add telegram
```

#### 파일 작업

**파일 읽기:**
```
@OpenClaw "C:\Users\MyName\Documents\notes.txt" 읽어줘
```

**파일 생성:**
```
@OpenClaw 다음 내용으로 "project_plan.md" 파일을 만들어줘:
# 프로젝트 계획
1. 설계
2. 구현
3. 테스트
```

**파일 수정:**
```
@OpenClaw "config.json" 파일에서 "port: 3000"을 "port: 8080"으로 바꿔줘
```

---

### ⚙️ 고급 설정

#### 로깅 설정

```bash
# 로깅 레벨 변경
openclaw config set logging.level=DEBUG
openclaw config set logging.file=C:/logs/openclaw.log

# 로그 확인
type C:\logs\openclaw.log
```

#### API 키 관리

```bash
# 환경 변수로 설정
$env:OPENAI_API_KEY = "sk-..."
$env:ANTHROPIC_API_KEY = "sk-ant-..."

# 또는 설정 파일
# ~/.openclaw/config.yml
api_keys:
  openai: "sk-..."
  anthropic: "sk-ant-..."
```

#### 보안 설정

```bash
# 로컬호스트만 접근 허용
openclaw config set gateway.host=127.0.0.1

# 인증 토큰 설정
openclaw config set auth.token=YOUR_SECRET_TOKEN
```

---

### 🔧 일반적인 작업

#### 문서 작성 & 정리

```
@OpenClaw 
다음 구조로 문서 폴더를 만들어줘:
- project/
  - docs/
    - README.md
    - SETUP.md
    - API.md
  - src/
  - tests/
```

#### 코드 실행 & 자동화

```
@OpenClaw 
Python으로 "hello_world.py" 스크립트를 만들고 실행해줘:
print("안녕하세요!")
```

#### Git 작업

```
@OpenClaw 현재 폴더의 git 상태를 보여줘
@OpenClaw 변경사항을 커밋하고 푸시해줘 (메시지: "Update docs")
```

#### 웹 정보 수집

```
@OpenClaw "Python 3.12 최신 기능" 을 검색하고 요약해줘
@OpenClaw https://example.com 페이지의 내용을 추출해줘
```

---

### 📱 채널별 사용 팁

#### Discord 사용

```
@OpenClaw 명령어들 (DM 또는 채널에서)
- read <파일경로>
- write <파일명>
- exec <명령어>
- search <키워드>
```

#### CLI 직접 사용

```bash
# PowerShell
openclaw message "파일 목록을 보여줘"

# 또는 파이프 사용
echo "현재 디렉토리는?" | openclaw message
```

#### Telegram 봇

```
1. BotFather에서 봇 생성
2. OpenClaw에 토큰 연동
3. Telegram에서 @YourBot mention
```

---

### 🆘 트러블슈팅

#### Gateway가 시작되지 않음

```bash
# 포트 확인
netstat -ano | findstr :3000

# 포트 변경
openclaw config set gateway.port=3001

# Gateway 재시작
openclaw gateway restart
```

#### API 키 오류

```bash
# 키 확인
echo $env:OPENAI_API_KEY

# 유효성 테스트
openclaw test-api
```

#### 파일 접근 권한 오류

```bash
# PowerShell 관리자 권한으로 실행
# 또는 폴더 권한 확인
icacls "C:\path\to\folder"
```

---

### 📚 더 알아보기

- **공식 문서**: https://docs.openclaw.ai
- **GitHub**: https://github.com/openclaw/openclaw
- **커뮤니티**: https://discord.com/invite/clawd
- **기술 블로그**: https://blog.openclaw.ai

---

## 4. 다음 단계

이 초안은 다음과 같이 확장될 수 있습니다:

- [ ] 스크린샷 추가 (실제 사용 예시)
- [ ] 비디오 튜토리얼 링크
- [ ] FAQ 섹션
- [ ] 사용자 커뮤니티 사례 연구
- [ ] 보안 & 프라이버시 가이드
- [ ] Windows 특화 팁 (PowerShell, 경로 설정 등)
- [ ] 통합 예제 (Git + Python + 문서화)

---

**작성일**: 2026-03-29  
**버전**: 1.0  
**대상**: Windows 데스크탑 신규 사용자
