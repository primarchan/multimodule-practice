# Spring Multi Module 실습

### Multi Module 이란?
- 필요한 기능별로 Module 을 생성한다.
- 기계를 조립하는 것과 같이 필요한 Module 을 조립한다.
- N 개의 Module 이 조립되어 있는 프로젝트를 Multi Module 이라고 부른다.
- > ex) `로그인 Module`, `인증 Module`, `DB Entity Module` 등

### Multi Module 을 사용하는 이유
- > 예를 들어 API 서버에도 `DB Entity` 가 필요하고 `Batch 서버`에서도 동일한 `DB Entity` 가 필요하다면  
  > 중복된 `Entity` 를 `Module 화` 시켜 사용하기 위해 `Multi Module` 프로젝트를 사용한다.  
  > 만약 독립적으로 관리하다면 중복해서 관리해야하므로 `Risk` 가 증가한다.

### Exception Handling
- 개발 언어 혹은 프레임워크에서 발생한 `Exception` 은 반드시 `Custom` 하게 `Wrapping` 하여 처리한다.  
- `RestControllerAdvice` 어노테이션을 사용하여 모든 예외를 해당 클래스에서 클라이언트와 사전에 정의한  
- 값으로 재정의 한다.
- > `NPE(= Null Point Exception)` 일 경우, `Error Code` 를 `4001` 로 내린다.

### Multi Module 구조에서 Gradle을 사용한 배포
- `Multi Module` 구조에서는 원하는 `Module` 을 골라서 빌드&배포가 가능하다.
- `Build Tool` 로는 `Gradle` 혹은 `Maven` 을 사용하는데 근래에 생성되는 프로젝트는 대부분 `Gradle` 을 사용한다.
- `Gradle` 을 사용하여 빌드&배포를 하려면 `Gradle` 문법을 학습해야 한다.
- > ex) 빌드 명령어 : `./gradlew clean :module-api:buildNeeded --stacktrace --info --refresh-dependencies -x test`

### Profile이 필요한 이유
- 실제 회사에서 개발할 땐 N 개의 `Profile` 을 설정한다.
- > ex) `local`, `dev`, `test`, `prod`
- 위와 같이 `Profile` 을 나누는 이유는 환경별로 설정해야 하는 `Property` 값들이 다르기 때문이다.

### Profile사용 방법
- 실제 프로젝트에서는 다음과 같은 파일로 환경별 Property를 구분한다.
- > ex) `application-{env}.yaml`
- > ex) `application-local.yaml`, `application-pdev.yaml`, `application-prod`
- > ex) 환경에 따른 명령어 예시 : `java -jar "-Dspring.profiles.active={ 환경의 profile-name }" module-api-0.0.1-SNAPSHOT.jar`
- ref : https://docs.spring.io/spring-boot/docs/2.1.9.RELEASE/reference/html/boot-features-external-config.html

### MySQL DB User 생성 가이드
> ```sql
> -- DB(스키마) 조회
> show databases;  
> -- DB(스키마) 생성
> create database multimodule;  
> -- USER 삭제
> drop user primarchan;  
> -- USER 생성
> create user 'primarchan'@'localhost' identified by '1111';  
> -- USER 조회
> select `user` from `mysql`.`user`;  
> -- USER 권한 조회
> show grants for 'primarchan'@'localhost';
> -- USER - DB(스키마) 권한 부여
> grant all on `multimodule`.* to 'primarchan'@'localhost' with grant option;
> -- UPDATE 사항 반영
> flush privileges;
> ```
 
