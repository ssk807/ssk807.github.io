---
title: "JSP 내장 객체"
excerpt: "JSP에서 Config객체와 application객체?"
categories:
  - JSP
tags:
  - JSP
  - JAVA
  - Back-End
last_modifed_at: 2020-08-02
---  

## config 객체
- 서블릿 초기 환결 설정 데이터를 저장 할 때 사용하는 객체로써 JSP 웹 페이지를 변환한 서블릿을 초기화 할 때 사용되는 초기화 파라미터를 저장하고 있다.
이 객체는 서블릿에서는 유용하게 사용되지만 JSP에서는 별로 사용되지 않는다.  

## config 객체 초기화 및 선언  
```xml
<servlet>
  	<servlet-name>servletEx</servlet-name>
  	<jsp-file>/jspEx.jsp</jsp-file>
  	<init-param>
		<param-name>adminID</param-name>
		<param-value>admin</param-value>
	</init-param>
	<init-param>
		<param-name>adminPW</param-name>
		<param-value>1234</param-value>
	</init-param>
  </servlet>
```  
- init-param를 통해 name 과 value를 설정  
- jsp에서 name에 대한 value를 가져올 땐 cofig.getInitParameter("<param-name>") 사용  
- servlet에서 name에 대한 value를 가져올 땐 getServletConfig().cofig.getInitParameter("<param-name>") 사용  


## 어플리케이션 객체
- application 객체는 JSP 기본객체로 JSP 페이지에서 따로 선언하지 않아도 참조하여 사용 가능하고 또한 application 기본객체는 자신이 속한 웹어플리케이션 범위 안의 모든 JSP 범위에서 공유된다.
application 객체는 이름 그대로 웹 어플리케이션에 대한 정보들을 가지고 있으며 웹 어플리케이션이 시작될 때 설정되는 초기 설정 정보 또한 담고있어 설정값들을 얻을 수 있고, 웹 어플리케이션이 사용자는 파일 자원도 가져올 수 있다.  

## Application 객체 선언  
- 웹어플리케이션이 구동될 때 웹 어플리케이션 경로의 WEB-INF/web.xml파일을 참고하도록 정의되어 있다. web.xml에 다음과 같은 코드를 삽입하여 초기 설정값을 정의한다.  
```xml
<?xml version="1.0" encoding="UTF-8"?> 
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://xmlns.jcp.org/xml/ns/javaee" 
  xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaeehttp://xmlns.jcp.org/xml/ns/javaee/web-app_3_1.xsd" id="WebApp_ID" version="3.1"> 
  
  
  <context-param>
      <param-name>imgDir</param-name>
      <param-value>/upload/img</param-value>
  </context-param>
</web=app>
```  
- context-param을 통해 name과 value 설정  
- jsp에서 name에 대한 value를 가져올 땐 application.getInitParameter("<param-name>") 사용  
- servlet에서 name에 대한 value를 가져올 땐 getServletConfig().cofig.getInitParameter("<param-name>") 사용  

