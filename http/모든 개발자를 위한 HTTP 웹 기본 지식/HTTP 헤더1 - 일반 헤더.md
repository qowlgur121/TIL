## HTTP 헤더1 - 일반 헤더
HTTP 헤더에는 HTTP 전송에 필요한 메타 데이터가 들어간다.  
<img src="https://github.com/qowlgur121/TIL/blob/main/http/images/HTTP-header1.png" width = 600/>  

### 표현 헤더
특히 헤더 중 표현 헤더는 메시지 바디에 실제로 들어있는 데이터와 관련된 메타 데이터이다. 
표현이라는 것이 생소한데 메시지 바디는 데이터가 들어갈 박스이고 표현 바디는 그 박스에 들어가는 실제 데이터를 말한다. 
왜 표현 바디라고 부르냐면 데이터가 정해진 표현(형태)를 이루고 있어서 그렇게 부른다.
그러면 표현 헤더는 이러한 표현 바디에 관련된 정보를 가지고 있는 메타데이터인 것이다.

<img src="https://github.com/qowlgur121/TIL/blob/main/http/images/HTTP-header2.png" width = 600/>
표현 헤더들은 위와 같이 특히 저러한 것들이 있다. 

#### Content-Type 헤더
![img.png](../images/HTTP-header3.png)
- 표현 헤더에서 이 헤더는 데이터의 형식을 명시한다.

#### Content-Encoding 헤더
![img_1.png](../images/HTTP-header4.png)
- 데이터가 어떤 방식으로 압축되었는지를 알려준다.

#### Content-Language 헤더
![img_2.png](../images/HTTP-header5.png)
- 데이터의 주요 언어를 알려준다.

#### Content-Length 헤더
![img_3.png](../images/HTTP-header6.png)
- 데이터의 길이를 알려준다. 바이트 기준이다.

이것들은 서버가 응답 데이터의 형식을 알려줄 때 이 헤더들을 쓴다.

반대로 클라이언트가 요구하는 특정 형식이 있을 때는 콘텐츠 협상을 한다.

### 콘텐츠 협상
콘텐츠 협상은 클라이언트가 선호하는 형식을 요구하는 것이다. "Accept~"으로 보낸다.

![img_4.png](../images/HTTP-header7.png)

![img_5.png](../images/HTTP-header8.png)

![img_6.png](../images/HTTP-header9.png)

이렇게 우선순위를 숫자를 이용하여 알려줄 수도 있고 구체적으로 적음으로써 우선순위를 알려주는 방식을 쓴다.

### 전송 방식
![img.png](HTTP-header10.png)  
전송 방식을 이렇게 존재한다.

#### 단순 전송
![img_1.png](../images/HTTP-header11.png)  
단순 전송은 서버가 클라이언트에게 데이터를 보낼 때 미리 전체 데이터의 크기를 알려주고 한번에 데이터를 보내는 방식이다.

#### 압축 전송
![img_2.png](../images/HTTP-header12.png)  
압축 전송은 데이터를 압축해서 보내는 방식이다.  
  
#### 분할 전송
![img_3.png](../images/HTTP-header13.png)  
데이터를 한번에 보내지 않고 분할해서 보내는 방식이다.

#### 범위 전송
![img_4.png](../images/HTTP-header14.png)  
이 방식은 필요한 데이터의 범위만 전송하는 방식인데 이 방식은 클라이언트가 전체 데이터 중 특정 부분만 필요할 때 쓰면 좋다.

### 일반 정보
![img.png](../images/HTTP-header15.png)
HTTP의 일반 정보에는 이러한 것들이 있다.

#### From
![img_1.png](../images/HTTP-header16.png)  
이것은 클라이언트가 서버에게 방문한 자의 이메일 주소를 남기는 용도이다.
예를 들어, 검색 엔진이 웹 사이트를 크롤링 할 때 쓰였는데 이 때 크롤링 담당 근무자의 이메일 주소를 남겼었다. 만약 문제가 생기면 이 담당자에게 연락하라고 하는 용도로 From이 쓰였었다.
지금은 보안 이슈로 잘 쓰이지 않는다.

#### Referer
Referer은 현재 페이지를 방문하기 전에 있던 웹 페이지 주소

#### User-Agent
클라이언트가 어떤 환경인지 알려준다.
![img_2.png](../images/HTTP-header17.png)
