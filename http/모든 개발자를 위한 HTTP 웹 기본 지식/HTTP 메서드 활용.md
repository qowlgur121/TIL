## HTTP 메서드 활용

### 클라이언트에서 서버로 데이터 전송
보통 2가지 방식이 있다.
1. 쿼리 파라미터를 통한 데이터 전송
   - 주로 GET 메서드를 사용할 때 이 방식으로 많이 사용하고 검색할 때, 게시판에 정렬 조건을 넣을 때 쿼리 파라미터를 이용해서 데이터를 전송한다.
2. 메시지 바디를 통한 데이터 전송
   - HTTP 메시지에 바디에 데이터를 넣어서 전송하는 방식이다. 주로 POST, PUT, PATCH 메서드를 쓸 때 쓰인다. 

#### 클라이언트에서 서버로 데이터를 전송하는 4가지 상황
1. 정적 데이터 조회 - 쿼리 파라미터 미사용  
   <img src="https://github.com/qowlgur121/TIL/blob/main/http/images/정적데이터조회.png" width = 600/>  
   - 정적 데이터는 클라이언트가 어떤 요청을 하든 항상 같은 결과를 나타내는 것. 예로 이미지, 정적 텍스트 문서.  
   - 정적 데이터 조회할 땐 보통 파라미터를 사용하지 않아도 된다. 그저 리소스 경로로 조회가 가능
2. 동적 데이터 조회 - 쿼리 파라미터 사용  
   <img src="https://github.com/qowlgur121/TIL/blob/main/http/images/동적데이터조회.png" width = 600/>  
   - 동적 데이터는 클라이언트가 어떤 요청을 하느냐에 따라 다른 결과가 나올 수 있는 것. 예로 검색, 게시판 목록 정렬 필터 결과.  
   - 동적 데이터 조회할 땐 쿼리 파라미터를 같이 보내야 한다. 서버가 클라이언트의 커스텀된 요청에 맞게 동적으로 결과를 만들어서 보내줘야 하기 때문이다.

3. HTML Form을 통한 데이터 전송  
   HTML Form이란 사용자가 웹 페이지에 정보를 입력하고, 그 정보를 서버로 전달하기 위한 중간 역할을 하는 HTML 코드이다. 사용자가 입력한 정보는 웹 브라우저에 의해 HTTP 메시지로 만들어져 서버에게 전송된다.  
   <img src="https://github.com/qowlgur121/TIL/blob/main/http/images/HTML-Form-POST.png" width = 600/>  
   <img src="https://github.com/qowlgur121/TIL/blob/main/http/images/HTML-Form-GET1.png" width = 600/>  
   여기 설명에서 action/="/save"인데 get메서드를 쓰면 안되는 이유가 보통 /save경로는 데이터를 서버에 저장하기 위한 용도로 설계되었을지도 모른다. 그래서 그 위치로 이 메시지를 전달하게 되니까 get메서드의 목적과 달리 리소스를 저장,변경시킬 수도 있으니까.  
   <img src="https://github.com/qowlgur121/TIL/blob/main/http/images/HTML-Form-GET2.png" width = 600/>  
   <img src="https://github.com/qowlgur121/TIL/blob/main/http/images/HTML-Form-multipart.png" width = 600/>  
   다른 종류의 여러 데이터를 함께 전송 가능
4. HTTP API를 통한 데이터 전송
   HTTP API란 클라이언트와 서버가 데이터를 주고 받는 모든 방식을 말한다. HTML Form보다 큰 개념이다. 중요한 건 페이지를 나타내지 않고 데이터만 주고 받는 방식이다. HTML Form은 사용자에게 정보를 입력받는 화면을 제공하는데 초점을 맞춘것과 대비된다.  
    <img src="https://github.com/qowlgur121/TIL/blob/main/http/images/HTTP-API1.png" width = 600/>  
   HTTP API 방식은 컬렉션, 스토어, HTML Form 이렇게 3가지 방식이 있다.   
   <img src="https://github.com/qowlgur121/TIL/blob/main/http/images/HTTP-API-POST1.png" width = 600/>  
   <img src="https://github.com/qowlgur121/TIL/blob/main/http/images/HTTP-API-POST2.png" width = 600/>  
   왜 컬렉션 방식을 POST 기반이라고 하냐면 컬렉션 방식은 특정 종류의 리소스들을 다 모아놨으니까 리소스의 정확한 위치를 클라이언트가 모르더라도 /members만 하고 POST를 하면 서버가 알아서 새 리소스를 생성하고 그 위치를 반환하니까 컬렉션방식은 POST 기반 등록이라고 한다. 핵심은 클라이언트가 리소스의 정확한 위치를 몰라도 된다는 것이다.
   <br><br>
   <img src="https://github.com/qowlgur121/TIL/blob/main/http/images/HTTP-API-PUT1.png" width = 600/>  
   <img src="https://github.com/qowlgur121/TIL/blob/main/http/images/HTTP-API-PUT2.png" width = 600/>  
   왜 스토어 방식을 PUT 기반이라고 하냐면 클라이언트가 원하는 리소스의 위치를 알고 직접 찾아가서 확인하거나 수정하는 방식이어서 스토어 방식을 PUT 기반 등록이라고 한다. 중요한 것은 이 PUT 기반은 클라이언트가 원하는 리소스의 위치를 안다는 것이다.
   <br><br> 
   <img src="https://github.com/qowlgur121/TIL/blob/main/http/images/HTTP-API-Form1.png" width = 600/>  
   <img src="https  ://github.com/qowlgur121/TIL/blob/main/http/images/HTTP-API-Form2.png" width = 600/>  
   <img src="https://github.com/qowlgur121/TIL/blob/main/http/images/HTTP-API-Form3.png" width = 600/>  
   이렇게 HTML Form 방식은 GET, POST만 지원하기 때문에 여러 수정, 삭제 등 여러 기능을 이 GET, POST만으로 나타내기는 한계가 있기 때문에 동사로 된 리소스 경로를 사용하여 해결한다. 이 경로를 컨트롤 URI라고 한다.
   <br><br>
   <img src="https://github.com/qowlgur121/TIL/blob/main/http/images/HTTP-API-URI.png" width = 600/>  
   정리하자면 이러하다.



