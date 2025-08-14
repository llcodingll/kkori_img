 ## 🗂️ 팀 문서 & 자료 링크

<p align="center">
  <a href="https://www.notion.so/229656e282d88069a69fe9a18ca1cc58?v=229656e282d88040a866000cc977e780">📒 팀 노션</a> &nbsp;|&nbsp;
  <a href="https://www.notion.so/230656e282d8801991e7fda7326561a8">📚 개발 위키</a> &nbsp;|&nbsp;
  <a href="https://www.notion.so/Ground-Rule-229656e282d88055a6bccf41c7cf1064">📏 그라운드 룰</a> &nbsp;|&nbsp;
<!--   <a href="https://kkori.site/">🚀 데모 페이지</a> -->
</p>

<br/>
<br/>

## 🧑‍💻 역할 및 기여

| 담당자 | 주요 작업                                                                                                                                                                                       |
|--------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **강진규** | - CI/CD 파이프라인 구축 및 배포 자동화 설정<br>- 실시간 채팅 기능 WebSocket 구현<br>- WebRTC 시그널링 서버 구현 및 P2P 연결 관리<br>- 꼬리질문 생성 로직 및 STT API 연동 구현<br>- 음성 처리 및 텍스트 변환 기능 개발<br>- 면접 세션 관리 및 WebSocket 기반 면접 로직 개발 |
| **배수한** | - 면접 세션 클래스 설계 및 상태 관리 로직 개발 및 구현<br>- WebSocket 기반 면접 비즈니스 로직 전반 개발<br>- 연결 끊김 시 재연결 로직 및 상태 복구 구현<br>- 면접 결과 저장 및 조회 API 구현<br>- 면접방 관리 및 사용자 권한 처리 로직 개발                                 |


<br/>
<br/>

## 👋 프로젝트 소개

### 🎤 *"AI 기반 실시간 면접 연습 플랫폼"*

**Kkori**는 사용자가 **실시간 WebSocket 통신을 통해 면접을 연습**하고,  
**AI 기반 음성 인식과 꼬리질문 생성**으로 실제 면접과 같은 경험을 제공하는 **면접 연습 서비스**입니다.

- 사용자는 **혼자 연습(SOLO)** 또는 **둘이서 연습(PAIR)** 모드를 선택할 수 있어요.
- **실시간 음성 인식(STT)** 으로 답변을 텍스트로 변환하고 **AI가 꼬리질문을 자동 생성**합니다.
- **WebRTC 기반 영상/음성 통화**와 **실시간 채팅**으로 생생한 면접 환경을 제공해요.

<br/>
<br/>

## 🧩 **고민과 해결 방안**

### 🔄 **WebSocket 재연결 전략으로 안정적인 면접 환경 구축**

실시간 면접 시스템에서 네트워크 불안정이나 브라우저 강제 종료로 인한 WebSocket 연결 끊김은 치명적인 문제였습니다. 연결이 끊어지면 진행 중인 면접이 중단되고, 사용자는 처음부터 다시 시작해야 하는 상황이 발생할 수 있었습니다.

전통적인 heartbeat나 ping/pong 방식은 지속적인 메시지 교환으로 인한 오버헤드가 발생했고, 우리 서비스의 특성상 대부분의 이벤트가 broadcast되어 즉각적인 연결 끊김 감지가 어려웠습니다.

이를 해결하기 위해 **"마지막 이벤트 재발송"** 전략을 도입했습니다. 각 사용자별로 마지막 발생 이벤트를 메모리에 저장하고, 재연결 시 해당 이벤트를 재전송하여 끊어진 지점부터 자연스럽게 이어갈 수 있도록 구현했습니다.

JWT 기반 사용자 인증과 userId 매핑을 통해 재연결 시 이전 세션 상태를 정확히 복구할 수 있었고, 연결 상태 모니터링 오버헤드 없이도 빠른 재연결이 가능한 안정적인 면접 환경을 구축했습니다.

(위키 추가 필요)    
[Wiki로 자세히 보기](https://www.notion.so/230656e282d8801991e7fda7326561a8)

<br/>

### 🛡️ **백**


[Wiki로 자세히 보기]()

<br />

### 🚀 프론트


[Wiki로 자세히 보기]()

<br/>
<br/>

## 🎯 주요 기능 소개

### 🎤 실시간 면접 세션 관리
> **"혼자도, 둘이서도! 다양한 면접 연습 모드"**

**사용자는 SOLO 또는 PAIR 모드를 선택해 면접을 시작**할 수 있습니다.  
**WebSocket 기반 실시간 통신**으로 면접 상태가 실시간으로 동기화되며,  
**면접관/면접자 역할을 자유롭게 바꿔가며** 연습할 수 있어요.

<img src="" width="700" alt="면접 세션 관리" />

<br/>
<br/>

### 🤖 AI 기반 꼬리질문 생성
> **"답변에 따라 달라지는 똑똑한 질문!"**

**사용자의 답변을 실시간으로 분석**하여  
**GPT API를 통해 맞춤형 꼬리질문을 자동 생성**합니다.  
**STT(Speech-to-Text) 기술**로 음성 답변을 텍스트로 변환하고,  
이를 바탕으로 **개인화된 후속 질문**을 제공해요.

<img src="" width="700" alt="AI 꼬리질문" />

<br/>
<br/>

### 🎥 WebRTC 화상 면접
> **"실제 면접과 똑같은 화상 환경!"**

**WebRTC 시그널링 서버**를 통해 P2P 화상 통화를 지원하며,  
**실시간 음성/영상 스트리밍**으로 실제 면접과 동일한 환경을 제공합니다.  
**화면 공유와 음성 제어** 기능으로 다양한 면접 상황을 연출할 수 있어요.

<img src="" width="700" alt="WebRTC 화상면접" />

<br/>
<br/>

### 💬 실시간 채팅 시스템
> **"면접 중에도 소통은 계속되어야죠!"**

**WebSocket 기반 실시간 채팅**으로 면접 진행 중  
**참여자들이 즉시 소통**할 수 있습니다.  
**방별 채팅방 관리**와 **메시지 브로드캐스팅**으로  
원활한 커뮤니케이션을 지원해요.

<img src="" width="700" alt="실시간 채팅" />

<br/>
<br/>

### 📊 면접 결과 분석
> **"연습 결과를 한눈에! 성장하는 나를 확인하세요"**

**면접 진행 과정과 답변 내용을 자동 저장**하여  
**개인별 면접 기록과 통계를 제공**합니다.  
**질문별 답변 시간, STT 정확도, 면접 횟수** 등  
다양한 지표로 **면접 실력 향상도를 추적**할 수 있어요.

<img src="" width="700" alt="면접 결과 분석" />

<br/>
<br/>

## ✅ 서비스 구조도

<img src="https://raw.githubusercontent.com/SwnBae/kkori_img/main/arc.png" width="700" alt="Kkori 서비스 아키텍처" />

<br/>
<br/>

## ⚒️ Tech Stacks

| 분류 | 기술 스택                                                                                                |
|------|------------------------------------------------------------------------------------------------------|
| **Frontend** | [![My Skills](https://skillicons.dev/icons?i=react,vite,tailwind,ts,nodejs)](https://skillicons.dev) |
| **Backend** | [![My Skills](https://skillicons.dev/icons?i=java,spring,hibernate)](https://skillicons.dev)          |
| **Database / Infra** | [![My Skills](https://skillicons.dev/icons?i=mysql,nginx,aws)](https://skillicons.dev)               |
| **배포** | [![My Skills](https://skillicons.dev/icons?i=docker,jenkins)](https://skillicons.dev)                 |
| **협업 / 개발도구** | [![My Skills](https://skillicons.dev/icons?i=git,gitlab,notion,jira)](https://skillicons.dev)        |

<br/>
<br/>

## 🤼 팀원 소개

| 이찬 | 김형진 | 강진규 | 배수한 | 유윤지 | 장동현 |
|:---:|:---:|:---:|:---:|:---:|:---:|
| <img src="https://github.com/user-attachments/assets/3bc958ec-4303-4559-b20e-465fe1776e17" width="120"> | <img src="https://avatars.githubusercontent.com/u/49364688?v=4" width="120"> | <img src="https://avatars.githubusercontent.com/u/64190888?v=4" width="120"> | <img src="https://avatars.githubusercontent.com/u/128581113?v=4" width="120"> | <img src="https://avatars.githubusercontent.com/u/105447233?v=4" width="120"> | <img src="https://avatars.githubusercontent.com/u/205485545?v=4" width="120"> |
| **Frontend** | **Frontend** | **Backend** | **Backend** | **Backend** | **Backend** |
| [@today-is-first](https://github.com/today-is-first) | [@hyeongjin-kim](https://github.com/hyeongjin-kim) | [@jin0410](https://github.com/jin0410) | [@SwnBae](https://github.com/SwnBae) | [@llcodingll](https://github.com/llcodingll) | [@SuitGGam](https://github.com/SuitGGam) |
