---
title: "What is Servlet?"
excerpt: "What is Servlet?"

categories:
  - Servlet
tags:
  - Servlet
  - JAVA
  - WebServer
last_modified_at: 2020-07-26
---  

## Servlet?  
[JSP](https://github.com/ssk807/ssk807.github.io/blob/master/_posts/2020-07-26-JSP.md)와 유사하게 정적인 웹 페이지를 동적인 컨텐츠를 제공하는 웹 페이지로 제공해주기 위한 기술이다.  

## Servlet 작동 과정
![](assets/images/servlet_container.png)
- 작동 과정만 보면 JSP의 작동과정과 유사하다. 하지만 차이점이라면 JSP는 __JSP 스크립트 파일__ 을 HTML로 응답을 보내는 느낌이라면, Servlet은 __JAVA__ 코드를 컨테이너가 변환시켜 브라우저로 응답을 보낸다.  

## Servlet Mapping
Servlet Mapping 이란?  
- 사용자로부터 Request가 왔을 때 무수히 많은 Servlet이 존재한다면 어떤 Servlet을 실행할지 구분이 필요하다. 이러한 Servlet을 구분하기 위해 Servlet Mapping이 필요하다.
  ```
     http://localhost::8080/context_path/servlet/package명.servlet명
  ```  
   또한 이와 같이 Full Path로 servlet을 URL에 표현할 수 있지만 이는 불필요하게 길고 보안에 취약하다는 단점이 있다.
   
Mapping에는 두 가지 방식이 있다.  
1. web.xml  
   - 일단 코드를 먼저 살펴보자.  
	   ```
	   <servlet>
		<servlet-name>ServletEx</servlet-name>
		<servlet-class>com.servlet.ServletTest</servlet-class>
	   </servlet>
	   <servlet-mapping>
		<servlet-name>ServletEx</servlet-name>
		<url-pattern>/SE</url-pattern>
	   </servlet-mapping>
	   ```  
   - 이와 같은 방식으로 web.xml에 servlet을 추가해주고 mapping을 시켜준다.  
	   ```
	   <servlet>
	    <servlet-name>ServletEx</servlet-name>
	    <servlet-class>com.servlet.ServletTest</servlet-class>
	   </servlet>
	   ```
   - servlet의 이름을 지정해주고 현재 패키지 안에 존재하는 servlet java class를 지정해준다.  
	   ```
	   <servlet-mapping>
		<servlet-name>ServletEx</servlet-name>
		<url-pattern>/SE</url-pattern>
	   </servlet-mapping>
	   ```  
   
   그리고 Mapping 시킬 servlet의 이름을 지정한 후 URL에 나타낼 servlet_mapping name을 지정한다.  
 
1. Annotation
  - 위의 web.xml을 수정하는 방식에 비해 매우 간단하다.
  ```java
  @WebServlet("/SE")
  public class ServletTest extends HttpServlet {
  }
  ```
  - 이와 같이 servlet java class를 선언하는 바로 위 줄에 @WebServlet("/서블릿 맵핑명")을 추가해주면 된다.  
  
  
## Servlet Request, Response
사용자의 request와 Web-server의 response를 담당하는 객체에 대해 알아보자.
![](https://github.com/ssk807/ssk807.github.io/blob/master/assets/images/request%2Cresponse.png)
- 위 그림과 같이 user는 웹 서버에게 request를 하게 되고 web server는 user에게 response를 하게 된다. 
이러한 과정에서 request를 처리해주기 위한 servlet이 실행이 되게 될텐데 servlet java 클래스는 위 그림과 같은 클래스들의 상속을 받고 있다.  
- 먼저 servletEx라는 클래스는 HttpServlet을 상속받고 있다. HttpServlet은 추상클래스로 GenericServlet이란 추상클래스를 상속받고 있고 GenericServlet은 각각 ServletConfig,
Servlet,Serializable이란 interface를 구현하고 있다.  
이런 상속 방식으로 작동되고 있는 이유는 local에서 작업하는 것이 아니라 웹 서비스란 것은 통신 과정에서 대량의 다양한 데이터가 오고가기 때문에 이러한 다양한 데이터들을 처리하기 위한 기능들을 상속받는다.  
- servlet class 를 생성하고 나면 doGet과 doPost에 parameter로 __HttpServletRequest request__ 와 __HttpServletResponse response가 있는 것을 확인할 수 있다.
  - HttppServletRequest : 요청에 대한 정보를 가지고 있는 객체로 대표적인 method는 getCookies(),getParameter(),getParameterNames(),getParameterValues()가 있다.  
  - HttpServletResponse : 응답에 대한 정보를 가지고 있는 객체로 대표적인 method는 getWriter(),getOutputStream(),addCookie()등이 있다.

## form 태그
form data처리 에 대해서 자세히 알아보기 전에 간단하게 HTML의 form tag에 대해서 짚고 넘어가보도록 하자.
```html
<form action="mSignUp" method="post">
.
.
.
</form>
```
- 위와 같이 form 태그를 사용하며 속성 중 하나인 action은 Servlet URL mapping 명을 적으며 해당 URL mapping을 가진 servlet에게 Request를 보내게 된다. 또한 method 속성은 get과 post 방식이 있다.
  - Get  
     1. 사용자의 form data가 URL과 함께 보내진다. 따라서 1024문자라는 크기제한을 가지며 보안에 취약점을 가지게 된다.  
     1. DB에 영향을 주지 않는 단순한 read 위주의 작업에 사용된다.  
  - Post
     1. 사용자의 form data가 HTTP Request에 포함되어 웹 서버로 전송된다. 따라서 URL엔 URL_Mapping 정보만 노출되며 보안에 덜 민감하다.  
     1. 보통 DB상에 업데이트나 정보 추가를 할때 사용하는 방식이다.  
    
```html
<form action="mSignUp" method="post">
		name : <input type="text" name="m_name"> </br>
</form>
```
- 위 코드 중 input의 속성 중 name은 데이터를 보낼 때 데이터들을 구분짓기 위한 속성이다.


## form data 처리
앞서 봤듯이, form은 server에게 request함과 동시에 사용자의 data를 보내는 태그이다. 이러한 form을 Servlet에선 HttpServletRequest 객체를 통해 받게 된다.  
Servlet에서 form data를 처리할 수 있는 방식은 두 가지가 있다. 바로 doGet() 과 doPost()이다.
1. doGet()  
  - doGet() 방식은 form tag의 method 속성을 get으로 했을 때 혹은 default로 지정해주지 않았을 때 실행된다. get method가 가지는 보안에 취약하다는 단점이 존재한다.
2. doPost()
	- doPost() 방식은 form tag의 method 속성을 post로 했을 때 실행된다.
두 방식 모두 HttpServletRequest 객체를 받아 data를 처리할 수 있는데 이 객체의 대표적인 공통 method를 살펴본다.  

- getParameter() : input tag의 name의 해당되는 파라미터를 가진 data를 get하겠다.  

  ```java
  ex) String m_name = request.getParameter("m_name");
  ```  
- getParameterValues() : 여러 개의 data가 들어오는 경우 getParameter를 이용해 배열로 받을 수 있다.  
예를 들어, HTML의 checkbox type의 경우 하나의 name에 여러 개의 data들이 선택되어 전달될 수 있다. 이런 경우  
```java
ex) String[] m_hobbys = request.getParameterValues("m_hobby");
```  
- getParameterNames() : 서버쪽으로 날아오는 input tag의 name들을 확인할 수 있다.  
```java
Enumeration<String> names = request.getParameterNames();
		while (names.hasMoreElements()) {
			String name = (String) names.nextElement();
			System.out.println("name : " + name);
		}
```

## Servlet Life-Cycle
![](assets/images/servlet_life_cycle.png)
- 클라이언트의 요청이 들어오면  WAS는 해당 요청에 맞는 Servlet이 메모리에 있는지 확인
	- 만약 없다면 해당 Servlet class를 메모리에 올린 후 init 실행
	- 이 후에 service 실행
- init()
	- 초기 servlet을 메모리에 올릴 때 한번만 호출된다.
	- servlet 객체 초기화 역할
-service(request,response)
	- servlet이 수신한 모든 request에 대해 service()가 호출된다.
		- service() 메서드는 request의 type(HTTP Method: GET, POST, PUT, DELETE 등)에 따라 적절한 메서드(doGet, doPost, doPut, doDelete 등)를 호출한다.
- destroy()
	- Web Application이 갱신 혹은 WAS가 종료될 때 한번만 호출된다.
	- Servleet 객체를 메모리에서 제거하는 역할
> reference: https://gmlwjd9405.github.io/2018/10/28/servlet.html
