## HTTP 상태코드
상태코드란 클라이언트가 서버에게 요청을 했을때 서버는 그 응답을 하는데 그 응답에 함께 보내는 세자리 숫자이다. 이것은 지금 통신에서 어떤 상태인지 알려주는 역할을 한다.

상태코드는 크게 5가지로 분류된다.

- 1xx: 요청을 성공적으로 받았고 아직 처리를 하지 않았다는 뜻.
- 2xx: 요청을 성공적으로 받았고 처리를 시작하거나 완료했다는 뜻
- 3xx: 리다이렉션을 해야 한다는 뜻이다. 
- 4xx: 문제의 원인이 클라이언트에게 있다는 뜻이다.
- 5xx: 문제의 원인이 서버에게 있다는 뜻이다.

모르는 상태 코드가 나타나면, 클라이언트는 상위 상태코드로 해석하여 처리하면 된다.
보통 1xx는 거의 사용 안한다.

### 2xx - 성공
2xx는 클라이언트의 요청을 성공적으로 받았고 처리를 시작하거나 완료했다는 뜻이다.

<<<<<<< HEAD
- 200 OK  
<img src="https://github.com/qowlgur121/TIL/blob/main/http/images/HTTP200.png" width = 600/>  
200은 요청을 성공적으로 받았고 처리를 성공적으로 완료했다는 뜻이다.
  
=======
#### 200 OK  
<img src="https://github.com/qowlgur121/TIL/blob/main/http/images/HTTP200.png" width = 600/>  
200은 요청을 성공적으로 받았고 처리를 성공적으로 완료했다는 뜻이다.  

>>>>>>> origin/main
#### 201 Created  
<img src="https://github.com/qowlgur121/TIL/blob/main/http/images/HTTP201.png" width = 600/>  
201은 요청을 성공적으로 받았고 처리를 성공적으로 완료했고 새로운 리소스를 생성했다는 뜻이다.  

#### 202 Accepted
202는 요청을 성공적으로 받았지만 처리를 완료하지 않았다는 뜻이다. 처리 완료까지 시간이 걸릴 수 있음을 의미한다.  

#### 204 No Content
204는 요청을 성공적으로 받았고 처리를 성공적으로 완료했지만 응답할 바디가 없다는 뜻이다.
ex) 웹 문서 편집기에서 save 버튼

### 3xx - 리다이렉션
3xx는 리다이렉션을 해야 한다는 것이다.  
무슨 소리냐면 만약 응답으로 3xx을 받았고 헤더에 Location 헤더가 있으면 Location 위치로 자동 이동하는 것을 말한다.  
<<<<<<< HEAD
<br><br>
<img src="https://github.com/qowlgur121/TIL/blob/main/http/images/HTTP-Redirection.png" width = 600/>  
=======

<img src="https://github.com/qowlgur121/TIL/blob/main/http/images/HTTP-Redirection.png" width = 600/>  

>>>>>>> origin/main
그니까 클라이언트가 서버에게 요청을 보냈는데 그 요청에 대한 응답에 3xx가 있고 헤더에 Location이 있으면 클라이언트는 그 Location으로 수정하여 자동으로 요청을 다시 보내는 것이다. 이때 사용자가 새로고침을 할 필요없이 자동으로 된다.  

<img src="https://github.com/qowlgur121/TIL/blob/main/http/images/HTTP-Redirection2.png" width = 600/>  

종류는 이러하다.
PRG 패턴은 뭐냐면 POST/Redirect/Get를 말하는 것인데, 그니까 리다이렉트할 때 클라이언트가 전의 요청과 같이 POST로 요청한다면 똑같은 요청을 하는 것이므로 중복이 되어 문제가 생길 수 있기 때문에 리다이렉트 때 GET으로 메서드를 변경하여 요청을 하는 패턴이다.  

### 4xx - 클라이언트 오류
요청이 실패했음을 나타내는 것인데 오류의 원인이 클라이언트에게 있다는 뜻이다.

### 5xx - 서버 오류
요청이 실패했음을 나타내는 것인데 오류의 원인이 서버에게 있다는 뜻이다.

