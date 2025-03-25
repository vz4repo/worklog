# 작업계획 관리 시스템

![작업계획 대시보드](https://example.com/dashboard-screenshot.png)
<!-- 메인 대시보드 화면 스크린샷을 넣으면 좋습니다. 작업계획 목록이 표시된 UI 화면 -->

## 📋 프로젝트 개요

작업계획 관리 시스템은 제조업체의 작업 일정과 계획을 효율적으로 관리하기 위한 웹 애플리케이션입니다. 실시간 상태 업데이트, 작업 이력 관리, 그리고 엑셀 기반의 대량 데이터 업로드 기능을 제공합니다. 특히 제조업 환경에서 작업자들이 작업 내역을 쉽게 확인하고 관리할 수 있도록 설계되었습니다.

### 핵심 기능

- 작업계획 생성, 조회, 수정, 삭제 (CRUD) 기능
- 실시간 상태 업데이트 (SSE 기술 활용)
- 엑셀 파일 업로드를 통한 대량 데이터 일괄 등록
- 날짜별, 상태별 작업계획 필터링
- 다양한 정렬 옵션 제공
- 모바일 환경에 최적화된 반응형 디자인

## 🛠️ 기술 스택

### 백엔드

- **Java 17**
- **Spring Boot 3.2.3**: 웹 애플리케이션 프레임워크
- **MyBatis 3.0.4**: SQL 매핑 프레임워크
- **SQLite**: 경량 데이터베이스
- **Apache POI**: 엑셀 파일 처리
- **Springdoc-openapi**: API 문서화 (Swagger)
- **Lombok**: 반복 코드 제거 유틸리티

### 프론트엔드

- **HTML5/CSS3/JavaScript**
- **Bootstrap 5.3.0**: UI 프레임워크
- **Server-Sent Events (SSE)**: 실시간 업데이트
- **Flatpickr**: 날짜/시간 선택 컴포넌트

![실시간 업데이트 데모](https://example.com/real-time-update.gif)
<!-- 실시간 업데이트 기능을 보여주는 짧은 GIF 이미지가 효과적입니다 -->

## 📁 프로젝트 구조

```
src/
├─ main/
│  ├─ java/com/calman/
│  │  ├─ domain/
│  │  │  └─ worklog/
│  │  │     ├─ controller/    # REST API 및 View 컨트롤러
│  │  │     ├─ dto/           # 데이터 전송 객체
│  │  │     ├─ mapper/        # MyBatis 매퍼 인터페이스
│  │  │     └─ service/       # 비즈니스 로직
│  │  ├─ global/
│  │  │  ├─ config/           # 애플리케이션 설정
│  │  │  │  └─ sse/           # 서버-센트 이벤트 구성
│  │  │  └─ util/             # 유틸리티 클래스
│  │  └─ Application.java     # 애플리케이션 진입점
│  └─ resources/
│     ├─ mapper/              # MyBatis XML 매퍼
│     ├─ schema/              # 데이터베이스 스키마
│     ├─ static/
│     │  ├─ css/              # 스타일시트
│     │  ├─ js/               # 클라이언트 스크립트
│     │  └─ images/           # 이미지 리소스
│     └─ application.yml      # 애플리케이션 설정
```

## 💻 주요 기능 상세

### 1. 엑셀 파일 업로드 및 처리

![엑셀 업로드 기능](https://example.com/excel-upload.png)
<!-- 엑셀 업로드 모달 또는 결과 화면 스크린샷 -->

특화된 엑셀 파서를 통해 복잡한 형식의 엑셀 파일에서 작업계획 데이터를 추출하고 처리합니다. 특정 시트와 열에서 필요한 정보를 추출하여 데이터베이스에 저장합니다.

```java
// 핵심 코드 예시
@PostMapping("/upload")
public ResponseEntity<Map<String, Object>> uploadExcel(
    @RequestParam("file") MultipartFile file,
    @RequestParam(value = "carModel", required = true) String carModel) {
    // 엑셀 파일 처리 로직
}
```

### 2. 실시간 데이터 업데이트 (SSE)

Server-Sent Events(SSE) 기술을 사용하여 작업계획 상태 변경 시 실시간으로 모든 클라이언트에 업데이트를 전달합니다. 이를 통해 여러 사용자가 동시에 작업할 때도 최신 상태를 확인할 수 있습니다.

```javascript
// 클라이언트 SSE 연결 코드
const SSE = {
  init: function() {
    this.eventSource = new EventSource('/api/sse/subscribe');
    // 이벤트 리스너 설정
  }
};
```

### 3. 반응형 모바일 최적화 디자인

태블릿과 모바일 디바이스에서도 최적의 사용자 경험을 제공하도록 반응형 디자인을 적용했습니다. Bootstrap 기반의 UI에 커스텀 CSS를 추가하여 다양한 화면 크기에 대응합니다.

![모바일 화면](https://example.com/mobile-view.png)
<!-- 모바일 화면 스크린샷 -->

### 4. 상태 관리 및 필터링

작업계획 상태(완료/미완료)를 직관적으로 관리하고, 다양한 필터링 옵션을 제공합니다. 날짜별, 상태별, 차종별 필터링이 가능하며, 효율적인 검색을 위한 정렬 기능을 제공합니다.

## 🚀 설치 및 실행 방법

### 사전 요구사항
- JDK 17 이상
- Gradle

### 설치 단계

1. 저장소 클론
```bash
git clone https://github.com/vz4repo/worklog.git
cd worklog
```

2. 애플리케이션 빌드
```bash
./gradlew build
```

3. 애플리케이션 실행
```bash
java -jar build/libs/worklog-v1.jar
```

4. 웹 브라우저에서 애플리케이션 접속
```
http://localhost:9090
```

## 📊 개발 과정 및 성과

이 프로젝트는 제조업체의 작업 관리 효율성을 높이기 위해 개발되었습니다. 주요 도전 과제와 해결 방법은 다음과 같습니다:

1. **복잡한 엑셀 파일 처리**: Apache POI 라이브러리를 사용하여 기존에 업무에 쓰이던 엑셀 파일의 특정 셀에서 데이터를 추출, 전산화 하여 웹을 통한 대시보드 생성
2. **실시간 데이터 동기화**: SSE를 활용한 효율적인 실시간 통신 구현
3. **모바일 최적화**: 작업 현장에서 태블릿으로 쉽게 사용할 수 있는 UI/UX 설계

## 🔗 API 문서

Swagger UI를 통해 API 문서를 확인할 수 있습니다.
```
http://localhost:9090/swagger-ui.html
```

![API 문서](https://example.com/api-docs.png)
<!-- Swagger UI 스크린샷 -->

## 🌟 향후 개발 계획

- 작업자별 통계 대시보드 추가
- 생산성 분석 리포트 기능
- 알림 시스템 구현 (이메일, 푸시 알림)
- 사용자 권한 관리 시스템 확장

## 📫 연락처

프로젝트에 관한 질문이나 피드백이 있으시면 언제든지 연락주세요:
- Email: thevzforalt@gmail.com
- GitHub: [Hyukrak Kwon](https://github.com/vz4repo/worklog)

---

© 2025 [Hyukrak Kwon]. All rights reserved.