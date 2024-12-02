
## 민감한 정보등 보안문제로 인하여 YML 파일은 직접 만드셔야합니다.


## 개요
[S3란?](https://github.com/imsukju/MyStudyNote/blob/main/Cloud%20and%20Messaging%20Systems/AWS/AWS%20S3.md)
**S3demo**는 AWS S3를 활용하여 파일 업로드 및 다운로드 기능을 구현한 Spring Boot 기반의 애플리케이션입니다. 이 프로젝트는 AWS SDK를 활용하여 S3와의 연동을 처리하며, RESTful API를 통해 파일 관리 기능을 제공합니다.

---

## 프로젝트 구조

```
S3demo/
├── src/
│   ├── main/
│   │   ├── java/com/intheeast/
│   │   │   ├── S3demoApplication.java          # 메인 애플리케이션 클래스
│   │   │   ├── configuration/
│   │   │   │   └── S3Config.java               # S3 클라이언트 설정
│   │   │   ├── controller/
│   │   │   │   └── S3Controller.java           # S3 API 엔드포인트
│   │   │   ├── exception/
│   │   │   │   └── S3Exception.java            # 커스텀 예외 처리
│   │   │   ├── service/
│   │   │   │   ├── S3Message.java              # S3 응답 메시지 DTO
│   │   │   │   └── S3Service.java              # S3 비즈니스 로직
│   ├── test/
│   │   ├── java/com/intheeast/
│   │   │   └── S3demoApplicationTests.java     # 테스트 클래스
├── target/
│   ├── classes/
│   │   ├── application.yaml                    # 애플리케이션 설정 파일 (S3 버킷 정보 제거됨)
├── pom.xml                                     # Maven 설정 파일
```

---

## 주요 기능

### 1. **파일 업로드**
- REST API를 통해 로컬 파일을 AWS S3 버킷으로 업로드.
- 파일 이름 중복 방지를 위한 고유 키 생성.

### 2. **파일 다운로드**
- API를 통해 S3 버킷에서 파일을 로컬로 다운로드.
- 다운로드 시 파일 이름을 지정할 수 있음.

### 3. **파일 삭제**
- 특정 파일을 S3 버킷에서 삭제하는 기능.

### 4. **커스텀 예외 처리**
- `S3Exception` 클래스를 활용하여 S3 작업 중 발생하는 예외를 처리.

---

## 실행 방법

### 1. **필수 요건**
- Java 17 이상
- AWS 계정 및 S3 버킷
- Maven 설치

### 2. **설정**
- `application.yaml` 파일에 다음 내용을 추가하여 AWS 자격 증명과 S3 버킷 정보를 설정:
  ```yaml
  cloud:
    aws:
      credentials:
        access-key: YOUR_AWS_ACCESS_KEY
        secret-key: YOUR_AWS_SECRET_KEY
      region:
        static: YOUR_AWS_REGION
    s3:
      bucket: YOUR_S3_BUCKET_NAME
  ```

### 3. **실행**
1. 프로젝트 디렉토리로 이동:
   ```bash
   cd S3demo
   ```
2. Maven을 사용하여 애플리케이션 실행:
   ```bash
   mvn spring-boot:run
   ```
3. 브라우저 또는 Postman에서 API 호출 테스트:
   - 파일 업로드: `POST /api/s3/upload`
   - 파일 다운로드: `GET /api/s3/download/{filename}`
   - 파일 삭제: `DELETE /api/s3/delete/{filename}`

---

## 테스트

- `S3demoApplicationTests.java`에서 JUnit을 사용하여 S3와의 상호작용을 테스트.
- 테스트 실행:
  ```bash
  mvn test
  ```

---

## 주의 사항

- `application.yaml` 파일의 내용은 보안 및 민감한 정보 보호를 위해 비워졌습니다. 실행 전에 적절히 설정해야 합니다.
- AWS S3에 저장된 파일은 비용이 발생할 수 있으니 주의하시기 바랍니다.
