# জাভা টেম্পলেট ইঞ্জিন

জাভা টেম্পলেট ইঞ্জিন হল এমন একটা সিস্টেম যাতে জাভা ডাটা অবজেক্ট html অথবা jsp তে দেখানো যায়। টেম্পলেটের মাধ্যমে জাভা কোড এইচটিএমএল অথবা জেএসপি তে লেখা যায়। একটু সহজভাবে বলতে গেলে html/jsp তে জাভা ডাটা অবজেক্ট দেখানোর জন্য বিভিন্ন টেম্পলেটের সিনট্যাক্স আছে যার দ্বারা আমরা ডাইনামিকভাবে ভ্যালু দেখতে পারি।                
বিভিন্ন ধরনের জাভা টেম্পলেট ইঞ্জিন আছে। যেমনঃ       
১. Java Server Pages with the Java Server Pages Tag Library (JSP/JSTL)                  
২. Thymeleaf                
৩. FreeMarker                  

<img src="Images/Template Engine.png" />

**JSP and JSTL**                                   
JSP হল Java Server Pages এমন একটি টেকনোলজি যার দ্বারা এইচটিএমএল পেজে jsp ট্যাগ ব্যবহার করে জাভা কোড লেখা যায়।              
```
<%@ page language="java" contentType="text/html; charset=US-ASCII"
    pageEncoding="US-ASCII"%>
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "https://www.w3.org/TR/html4/loose.dtd">
<html>
	<head>
		<meta http-equiv="Content-Type" content="text/html; charset=US-ASCII">
		<title>First JSP</title>
	</head>
	<%@ page import="java.util.Date" %>
	<body>
		<h3>Hi Pankaj</h3><br>
		<strong>Current Time is</strong>: <%=new Date() %>
	</body>
</html>
```

JSTL হল JSP Standard Tag Library যেটা কিছু ট্যাগের সমষ্টি যা jsp এর ভেতরে ব্যবহার করা হয়।                      
```
<%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c" %>
<html>
  <head>
    <title>Tag Example</title>
  </head>
  <body>
    <c:if test="${param.name == 'studytonight'}">
      <p>Welcome to ${param.name} </p>
    </c:if>
  </body>
</html>
```

**Thymeleaf**                  
Thymeleaf বর্তমানে স্প্রিং কমিউনিটিতে বেশ জনপ্রিয়।                        
```
<tbody>
    <tr th:each="student: ${students}">
        <td th:text="${student.id}" />
        <td th:text="${student.name}" />
    </tr>
</tbody>
```

**FreeMarker**               
FreeMarker হল Apache Software Foundation

https://hackernoon.com/java-template-engines-ef84cb1025a4