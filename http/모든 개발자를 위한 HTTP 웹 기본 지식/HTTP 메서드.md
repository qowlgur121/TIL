## HTTP 메서드

### HTTP API 만들기
- HTTP API를 만들 때 중요한 것은 리소스가 뭔지 구별하는 것이다. 만약 회원과 관련된 API를 만들어야 해서 URI를 만들때는 회원이 리소스이다.
  회원목록조회, 회원조회, 회원등록과 같이 기능이 뭔지는 URI에 기입하지 않아야 한다. 예를 들어 /members/100/update 와 같이 URI에 기능을 기입하지 말아야 하는 것이다
  이러한 기능은 HTTP메서드로 구분시키면 된다.

### HTTP 메서드 - GET  
<img src="https://github.com/qowlgur121/TIL/blob/main/http/images/GET.png" width = 600/>  

- GET 메서드는 리소스 조회 용도로 쓰인다. GET 요청을 하는 HTTP메시지에는 메시지 바디를 넣을 수도 있지만 호환되지 않는 서버도 있기 때문에 보통은 바디는 넣지 않는다.

### HTTP 메서드 - POST  
<img src="https://github.com/qowlgur121/TIL/blob/main/http/images/POST.png" width = 600/>  

- POST 메서드는 클라이언트가 서버에게 데이터를 보내서 처리해달라고 요청할 때 쓰인다. 보통 신규 리소스 등록, 프로세스 처리 등의 용도로 쓰인다.
  이 메서드를 쓰는 요청은 데이터가 중요하기 때문에 데이터 바디에 데이터를 넣어서 전달해야 한다. 만약 신규 리소스 등록으로 약속되었다면 이 메서드는 폴더 안에 파일을 넣는 것과 비슷하게 행동한다.
  만약 파일이 없다면 새로운 파일을 넣고, 있으면 새로운 파일로 덮어쓰는 것처럼. 서버는 반환값으로 이 리소스의 위치를 클라이언트에게 보낸다. /members/100처럼  
  
### HTTP 메서드 - PUT  
<img src="https://github.com/qowlgur121/TIL/blob/main/http/images/PUT1.png" width = 600/>
<img src="https://github.com/qowlgur121/TIL/blob/main/http/images/PUT2.png" width = 600/>  

- PUT 메서드는 리소스를 수정할 때 쓰이고, 이때 같이 보내는 메시지 바디로 완전히 대체한다. 만약 리소스가 존재하지 않는다면 신규 리소스가 생성된다.
  이때 중요한 건 클라이언트가 수정할 리소스의 위치를 알고 HTTP요청메시지에 기입해야 한다는 것이다. 예를 들어 members/100 같이 리소스의 구체적 위치를 기입해야 한다.
  완전히 대체하기 때문에 만약 이름과 나이가 있는 리소스일 경우 메시지 바디에 나이만 넣어서 보낸다면 리소스는 나이만 있게 된다.

### HTTP 메서드 - PATCH 메서드
<img src="https://github.com/qowlgur121/TIL/blob/main/http/images/PATCH1.png" width = 600/>  

<img src="https://github.com/qowlgur121/TIL/blob/main/http/images/PATCH2.png" width = 600/>  

- PUT에서는 나이만 보내면 리소스가 뭐였든 나이만 덩그러니 남는데 만약 나이만 바디에 넣어서 보내지만 이름은 그대로 살리고 나이만 변경하고 싶을 때는 이 PATCH 메서드를 쓰면 된다. 그런데 가끔 안되는 서버도 존재하는데 이럴 때는 POST 메서드를 쓰면 된다. 왜냐하면 POST메서드는 데이터를 처리하는 메서드로 거의 모든 처리를 할 수 있다.

### HTTP 메서드 - DELETE 메서드 
- DELETE 메서드는 이름 그대로 리소스를 삭제한다.

### HTTP 메서드의 속성
<img src="https://github.com/qowlgur121/TIL/blob/main/http/images/HTTP메서드속성.png" width = 600/>  

#### 안전
- 안전이라는 것은 메서드를 여러 번 쓰더라도 리소스의 변화가 있느냐이다. 리소스의 변화가 없으면 안전하고, 리소스의 변화가 있으면 안전하지 않다. 이때 이 안전을 판단할 때는 외부 요인은 신경쓰지 않는다. 예를 들어 로그가 쌓여서 장애가 발생해서 리소스가 변경 있더라도 신경쓰지 않는다.

#### 멱등
- 멱등이라는 것은 메서드를 여러 번 쓰더라도 결과가 같느냐이다. 만약 결과가 같으면 멱등이고, 결과가 다르면 멱등이 아니다. 주의할 것은 POST는 멱등이 아니다. 왜냐하면 중복한 리소스를 생성할 수 있기 때문이다. members/100, members/200....

#### 캐시가능
- 캐시 가능이라는 것은 응답 결과를 캐시해서 사용할 수 있느냐이다. 실제로는 GET정도만 캐시로 사용한다. 왜냐하면 다른 메서드들은 캐시키를 고려해야 하는데 GET은 그렇게 하지 않아도 되니까 간편하기 때문