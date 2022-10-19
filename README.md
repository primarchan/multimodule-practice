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


