### JSTL (Jsp Standard Tag Library)

* 자바서버 페이지 표준 태그 라이브러리은 Java EE 기반의 웹 애플리케이션 개발 플랫폼을 위한 컴포넌트 모임이다.
* JSTL은 XML 데이터 처리와 조건문, 반복문, 국제화와 지역화 같은 일을 처리하기 위한 JSP 태그 라이브러리를 사양을 확장했다.
* JSTL은 JSP 페이지 내에서 자바 코드를 사용하지 않고 로직을 내장하는 효율적인 방법을 제공한다. 표준화된 태그 셋을 사용하여 자바 코드가 들락거리는 것보다 더 코드의 유지보수와 응용소프트웨어코드와 사용자 인터페이스 간의 관심사와 분리로 이어지게 된다

### JSTL 

* custom tag : 개발자가 직접 태그를 작성 할 수 있는 기능을 제공 
* custom tag 중에서 많이 사용되는 것을을 모아 JSTL이라는 규약을 만듦 
* 논리적인 판단, 반복문의 처리, 데이터베이스 등의 처리를 할 수 있다. 
* JSP 2.1 - JSP 2.2 와 호환되는 JSTL 버전은 1.2 이다
* JSTL은 JSP 페이지에서 스크립트릿을 사용하지 않고 액션을 통해 간단하게 처리할 수 있는 방법을 제공 
* JSTL은 다양한 액션이 있으며, EL과 함께 사용하여 코드를 간결하게 작성할 수 있다. 



### JSTL Tag 

* directive 선언 형식 : <%@ taglib prefix="prefix" uri = "uri" %>

  | library  | prefix | function                             | uri                                    |
  | -------- | ------ | ------------------------------------ | -------------------------------------- |
  | core     | c      | 변수지원, 흐름제어, url처리          | http://java.sun.com/jsp/jstl/core      |
  | xml      | x      | xml 코어, 흐름제어, xml 변환         | http://java.sun.com/jsp/jstl/xml       |
  | 국제화   | fmt    | 지역, 메시지 형식, 숫자 및 날짜 형식 | http://java.sun.com/jsp/jstl/fml       |
  | database | sql    | SQL                                  | http://java.sun.com/jsp/jstl/sql       |
  | 함수     |        | Collection, String 처리              | http://java.sun.com/jsp/jstl/functions |

### JSTL-core tag

* 선언 : <%@ taglib prefix="c" uri ="http://java.sun.com/jsp/jstl/core" %> 

  

| function  | tag                       | description                                    |
| --------- | ------------------------- | ---------------------------------------------- |
| 변수 지원 | **set**                   | jsp page에서 사용 할 변수 설정                 |
| 변수 지원 | remove                    | 설정한 변수를 제거                             |
| 흐름 제어 | **if**                    | 조건에 따른 코드 실행                          |
| 흐름 제어 | **choose,when,otherwise** | 다중 조건을 처리할 때 사용 (if~else if ~ else) |
| 흐름 제어 | **for Each**              | array나 collection의 각 항목을 처리할 때 사용  |
| 흐름 제어 | forTokens                 | 구분자로 분리된 각각의 토큰을 처리할 때 사용   |
| URL처리   | import                    | URL을 사용하여 다른 자원의 결과를 삽입         |
| URL처리   | redirect                  | 지정한 경로로 redirect                         |
| URL처리   | url                       | url작성                                        |
| 기타 태그 | catch                     | Exception 처리에 사용                          |
| 기타 태그 | out                       | jspWriter에 내용을 처리한 후 출력              |

### 변수선언 : `<c:set>`

* `<c:set>` 액션은 변수나 특정 객체의 프로퍼티에 값을 할당할때 사용 

* value속성의 값이나 액션의 body content로 값을 설정 

* var 속성은 변수를 나타내며, 변수의 생존범위는 scope속성으로 설정(디폴트는 page)

* 특정 객체의 프로퍼티에 값을 할당할 때는 target속성에 객체를 설정하고 property에 프로퍼티명을 설정 

  ```jsp
  <!--value 속성을 이용하여 생존버위 변수 값 할당-->
  <c:set value ="value" var ="varName" [scope="{page|request|session|application}"]/>
  <!--액션의 Body 컨텐츠를 사용하여 생존범위 변수 값 할당-->
  <c:set var="varName" [scope="{page|request|session|application}"]>
  body content
  </c:set>
  <!--value속성을 이용하여 대상 객체의 프로퍼티 값 할당-->
  <c:set value="value" target="target" property="propertyName"/>
  <!-- 액션의 Body 컨텐츠를 사용하여 대상 객체의 프로퍼티 값 할당-->
  <c:set target="target" property="propertyName">
  body content
  </c:set>
  ```

### 예외 : `<c:catch>`

* 기본적으로 JSP 페이지는 예외가 발생하면 지정된 오류페이지를 통해 처리한다. 

* `<c:catch>` 액션은 JSP 페이지에서 예외가 발생할 만한 코드를 오류페이지로 넘기지 않고 직접 처리할 때 사용 

* var 속성에는 발생한 예외를 담을 page 생존범위 변수를 지정 

* `<c:catch>` 와 `<c:if>`액션을 함께 사용하여 java 코드의 `try ~ catch`와 같은 기능을 구현 할 수 있다. 

  ```java
  try {
  String str =null;
  out.println("Length of string : " + str.length());
  }
  catch (Throwable ex){ 
     out.print(ex.getMessage());
  }
  ```

  ```jsp
  <%@ page contentType="text.html" pageEncoding="UTF-8" errorPage="error.jsp"%>
  <%@ taglib prefix="c"  uri ="http://java.sun.com/jsp/jstl/core" %>
  
  <c:catch  var ="ex">
    <% 
      String str = null;
      out.prinltn("Lenth of string: " + str.length()); //예외 발생! 
      %>
  </c:catch>
  <c:if test="${ex != null}">
  예외가 발생하였습니다. ${ex.message}
  </c:if>
  ```

  ### 조건문 : `<c:if> , <c:choose> <c:when> <c:otherwise>`

* `<c:if>` 액션은 test속성에 지정된 표현식을 평가하여 결과가 true인 경우 액션의 Body 컨텐츠를 수행 

* `<c:if>` 액션의 var 속성은 표현식의 평가 결과인 Boolean 값을 담을 변수를 나타내며, 변수의 생존범위는 scope 속성으로 설정 

* `<c:choose><c:when><c:otherwise>`액션을 사용하면 if, else if, else 와 같이 처리 할 수 있다. 

  ```jsp 
  <c:if test= "${userType eq 'admin'}">
       <jsp:include page = "admin.jsp"/>
  </c:if
  ```

  

```jsp
 <c:if test ="{userType eq 'adimin'}" var ="accessible">
     <jsp:include page ="admin.jsp"/>
 </c:if>
 <c:if test = "${category == 'user' && menu == 'list'}">
     <jsp:include page ="admin.jsp"/>
 </c:if>
```

### 반복문 `<c:forEach>`

`<c:foreach>` 액션은 컬렉션에 있는 항목들에 대하여 액션의 Body 컨텐츠를 반복하여 수행 

* 컬렉션에는 Array,Colletion,Map또는 콤바로 분리된 문자열이 올 수 있다. 
* var 속성에는 반복에 대한 현재 항목을 담는 변수를 지정하고 items 속성은 반복할 항목들을 갖는 컬렉션을 지정 
* varStatus 속성에 지정한 변수를 통해 현재 반복의 상태를 알 수 있다. 

```jsp
<b>1) courses 리스트를 반복하면서 과정명 출력하기 </b>
<c:forEach var ="course" items="${courses}">
${course.name}<br/>
</c:forEach>
<b>2) courses 리스트를 반복하면서 순번과 과정명 출력하기 </b>
<c:forEach var ="course" items="${courses}" varStatus="vatStatus">
${course.name}<br/>
</c:forEach>
<b>3) 짝수번째 과정명만 출력하기 </b>
<c:forEach var ="course" items="${courses}" begin="0" end="5" step="2">
${course.name}<br/>
</c:forEach>
<b>4)숫자 1부터 5까지 출력하기 </b>
<c:forEach var ="course" begin="1" end="5" step="1">
${course.name}<br/>
</c:forEach>
```

