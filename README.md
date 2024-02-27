### GDSC BE Tutorial - Hands On

- 이용 대상
  - BE를 경험해보고 싶은 타 파트분들
- 제한 대상
  - gdsc BE 맴버

<details>
<summary>1장</summary>
<div markdown="1">

- 0단계 : 시작하기 전 
  - start.spring.io 라는 곳이 있다. 스프링이 뭔지

- 1단계 : Download

  1. java download
     - 아래 링크로 들어가서 **java 17버전**으로 다운로드 받아주세요!
     - [설치 link](https://www.oracle.com/java/technologies/downloads)
     - 환경 변수 설정 방법 window : https://coding-factory.tistory.com/838
     - 환경 변수 설정 방법 mac : https://gymdev.tistory.com/72
     - 설치가 완료된 후 java -version을 cmd에 입력하면 아래와 같이 java 17버전이 깔렸다고 나와야 합니다．
     - ![img_1.png](java_version.png)

  2. intellij 다운로드
     - 아래 링크로 들어가서 으로 다운로드 받아주세요!
     -[설치 link]() 

- 2단계 : 실행 

  1. spring project download 
     - [spring.io](https://start.spring.io/)에서 들어가서 아래와 같이 설정해주세요.
     - <img src = "start_spring.png" width="700">
     - 해당 화면과 같이 설정을 해주세요! 
       - 옆에 보이는 Spring Web은 Add Dependencies를 누르고 검색한 이후 선택하면 됩니다.
     - 이후 Generate를 눌러주세요!
  2. 스프링 첫 실행해보기
      - <img src="spring_play.png" width="600">
      - 재생 버튼 눌러보기!
      - http://localhost:8080/ 해당 url로 가보기
  3. resources/static/index.html
     - 해당 경로에 아래 사진과 같이 넣기!
     - <img src="static_index.png" width="700">
     - 다시 http://localhost:8080/ 해당 url로 가보기
     - 어떻게 바뀌었나요?

🔎　생각해보기
> 1. java 11 왜 선택할 수 없었을까요?
> 2. 어떻게 아무것도 안했는데 index.html이 보일까요?
> 3. http://localhost:8080/　에서　`:8080` 말고 다른 숫자로 바꿀 수 있는 방법이 있을까요?，　이 숫자가 어떤 의미였을까요?

위의 내용에 대한 답변은 pr로 남겨주세요　


1장을 해보고 해당 이유에 대해서 알게 된 정보를 pr로 올려주세요.

정말 수고하셨습니다! 



</div>
</details>

<details>
<summary>2장</summary>
<div markdown="1">

- 1단계 : 백엔드가 하는 일 
  - 백엔드가 하는 일을 무엇이라고 생각하시나요?
    - 백엔드 개발자의 주된 업무는 서버 측 애플리케이션을 개발하는 일입니다.
    - 개발 중 사용자가 필요로 하는 정보를 저장하고 관리하며 전달하는 역할을 수행한다고 생각하시면 됩니다. 
    - 즉, 서버, 데이터베이스, API 관련 일을 합니다.
    - 이번 챕터에서는 API에 대해 간단하게 알아보는 시간을 가져 보도록 하겠습니다.

  - API 란? 
    - API는 클라이언트의 요청을 서버에 전달하고, 서버의 결과물을 클라이언트에게 잘 돌려주는 역할을 합니다. 
    - 간단하게 서버와 클라이언트의 '중개자'라고 말할 수 있습니다.
    - ![api_image](api_image.png)


- 2단계 : 실습
  - 1장에서 다운로드 받은 스프링 프로젝트로 시작해 주세요.

### 📁 src/main/java/com/example/hello/

### HelloWorldApplication

```java
@SpringBootApplication
public class HelloworldApplication {

    public static void main(String[] args) {
        SpringApplication.run(HelloworldApplication.class, args);
    }

}
```


### 📁 src/main/java/com/example/hello/controller/

### GdscController

```java
@RestController
@RequestMapping("/api/v1")
public class GdscController {

    private final GdscService gdscService;

    public GdscController(GdscService gdscService) {
        this.gdscService = gdscService;
    }

    @GetMapping("/user")
    public ApiResponse callResponse(@RequestParam String username){
        return gdscService.madeMemberResponse(username);
    }

}
```

### 📁 src/main/java/com/example/hello/service/

### GdscService

```java
@Service
public class GdscService {
    public ApiResponse madeMemberResponse(String username) {
        return new ApiResponse(username, 본인나이를 넣어주세요, AUTHORITY.MEMBER);
    }
}
```


### 📁 src/main/java/com/example/hello/domain/

### Authority
```java
public enum Authority {
    MEMBER, CORE, LEAD;
}
```

### ApiResponse
```java
public record ApiResponse(String name, Integer age, AUTHORITY authority) {
}
```

- 3단계 : 결과화면
  - 1. 스프링 실행하고! 
  - 2. url 입력 : `localhost:8080/api/v1/user?username=아무개`
    - ![img_5.png](api_result.png)

🔎　생각해보기
1. 실습에서 사용되었던 URL 을 보시게 되면 queryParameter가 사용되었는데요. queryParameter가 무엇일까요?
2. api 개발하기 전 api명세서를 작성하게 됩니다. api 명세서는 왜 필요할까요?
3. naver.com 에 들어갔을 때 어떤 api들이 요청되고 있을까요? (아래 사진과 같이 크롬의 개발자 탭 > 네트워크 탭 > Fetch/XHR 클릭하고 확인)
![img_6.png](api_find_network_tab.png)

위의 내용에 대한 답변 및 질문은 pr로 남겨주세요.
1장을 해보고 해당 이유에 대해서 알게 된 정보를 pr로 올려주세요.

수고하셨습니다!
</div>
</details>