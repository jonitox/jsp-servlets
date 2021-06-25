# jsp-servlets
웹서버상에서 동작하는 자바코드. jsp파일: html대신 사용하여, html내부에 java코드를 포함시켜 동적인 페이지 반환 가능.     

# tomcat   
자바 서버 프로그램. 서버 실행 후, localhost:8080 사용(의미?) --    

#jsp     
- scriptng 요소: expressions, Scriptlet, Declaration   

- Expressions    
<%= (java object)%>로 표현. html에선 해당 객체의 toString()으로 자동 변환되어짐.          

- Scriptlet    
<% ... %>로 표현.     
여러줄의 자바코드 입력가능. 코드 중간중간 out.println으로 html에 포함될 string명시 가능.     
너무 긴 동작의 코드 대신 java class혹은 mvc로 구현하여 사용하는 것이 좋음. 이유: jsp코드는 간결할수록 좋음.     

- Declarations    
<%! %>로 표현.    
자바 메소드를 명시 가능. 다른 jsp java코드에서 해당 메소드를 사용할수 있음. 마찬가지로, 사용은 최소화하는것이 좋음.     

- java class 호출    
java class를 jsp에서 호출하여 사용. 미리 생성된 java class파일이 있다면, (src등의 폴더 내에)    
<%@page import="com.example.jsp.FunUtils, java.util.ArrayLists"%> 와 같이 jsp에서 java 패키지나 클래스를 import 후     
해당 파일 내의 클래스나 클래스내의 메소드 호출 가능. (,(콤마) 로 여러 파일 명시 가능)           

- jsp built-in java classes.    
request, response, out, session, application 등    

- jsp 파일에 다른 파일을 포함하는법      
jsp, html등의 다른 파일을 포함시킬때: <jsp:include page = "my-footer.jsp" />, <jsp:include page = "my-header.html"/>.     
처럼 현 jsp파일에 다른파일의 내용을 중간에 포함가능.    

- html form 입력을 받는법.      
html의 form태그로 submit된 data와 함께 jsp response를 요청받은 경우,(ex) <form action="student-response.jsp">)        
jsp에서 request.getParameter("firstName"(fieldName)) 혹은, (shortcut) ${param.firstName(fieldName)}으로 접근 가능.      
  
- session.   
  jsp 페이지에 대하 요청시 각 유저에 대한 세션 보유 가능.      
  jsp코드에선 session객체를 통해 여러 정보 저장 및 참조 가능. session.setAttribute(String(name), Object(value))로 모든 객체 저장.    
  session.getAttribute("(name)")로 세션에 저장된 객체 참조. session.invalidate : 현session의 모든 정보 비활성화,     
  session.getid: id를 get(id는 각 유저에대해 일반적으로 서버가 자동으로 배정) 그 외 isNew(), setMaxInactiveInterVal(long mils) 등등.         
  
  - cookies
  web browser에 저장되는 name-value 형태의 정보. 서버에 연결시, 해당 url에 대한 쿠키를 요청에 같이 보냄. 서버는 해당 쿠키를 읽을수 있음.          
  서버는 또한 요청에 따라 쿠키를 새로 생성하여 클라이언트가 저장하도록 다시 response에 담아 전송 가능.   
  jsp에선 이미 포함된 Cookie api사용.     
  Cookie(String(name), String(value))로 생성.        
  (cookie).setMaxAge(int(sec))로 만료기간 지정. 
  response.addCookie(cookie)로 브라우저로 보낼 응답에 생성한 쿠키를 명시.     
  request.getCookies()로 요청에 포함된 기존 쿠키를 읽음.     
  
  # jsp tags
  - jsp custom tags% jsp standard tags library.   
  
  
  # servlets.   
  - jsp와 차이. jsp: 내부적으론 .jsp를 가진 html 형식파일(단, 중간에 동적인 자바코드로 페이지생성)      
  servlets: 내부적으로는 자바 클래스. 클래스내의 doGet, doPost등의 메소드로 HTML코드를 동적으로 생성.    
  일반적으로, 비지니스 로직에 servlet을, 뷰 생성에 jsp를, 같이 혼합해서 사용. -> mvc.      
  
  -doGet.   
  해당 url(@)로 get요청을 보낼떄. 일반적인 코드 steps:    
  1)respons content type지정, 2)response의 HTML생성을 위한 printwriter선언. 3) printwriter로 HTML 페이지 생성(print).      

  - configuration parameters.    
  servlet은 특정 값들을 hard-coding하지않고 별도의 파일에 name-value로 명시해두어 사용할 수 있음. 해당 파일은 WEB0INF/web.xml로      
  xml형식의 표준파일에 context param으로 값들을 명시. 그 후 servlet상에선 httpServlet에 포함된 getServletContext()로 ServletContext를 선언해 객체로 저장하고,         
  (ServletContext.)getInitParameter("변수명"))로 web.xml에 선언되 값들을 가져올수 있다. (ServletContext는 web.xml에 접근해주는 helper class).        
