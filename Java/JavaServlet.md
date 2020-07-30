# জাভা সার্ভলেট            

* সার্ভলেট কি?
* লাইফ সাইকেল
* সার্ভলেট এপিআই 
* সার্ভলেট ইন্টারফেস 
* জেনেরিক সার্ভলেট
* এইচ টি টি পি সার্ভলেট
* কনফিগারেশন 

**সার্ভলেট কি?**                   
সার্ভলেট হল জাভার ডাইনামিক ওয়েব অ্যাপ্লিকেশন তৈরি করার এক ধরনের প্রযুক্তি। এটি ক্লায়েন্ট রিকুয়েস্ট আর সার্ভার রেসপন্স নিয়ন্ত্রন করে।  CGI (Common Gateway Interface) খুব কমন সার্ভার সাইড ল্যাঙ্গুয়েজ কিন্তু সার্ভলেট ই এখন জাভার সার্ভার সাইড ল্যাঙ্গুয়েজ হিসেবে ব্যবহৃত হয়। যে যে বিষয়ে সার্ভলেট CGI এর থেকে ভাল সেগুলো হলঃ                     
১. সার্ভলেটের পারফরম্যান্স অপেক্ষাকৃত ভাল।                                   
২. সার্ভলেট স্বাধীনভাবে যে কোন প্লাটফর্মে চলতে পারে কারন এটা জাভা দিয়ে তৈরি।                                 
৩. CGI কম্পিউটারে আলাদা প্রসেস হিসেবে রান করে আর জাভা রান হয় JVM এর ভেতরে।                  
৪. সার্ভলেটের সিকুরিটি CGI থেকে বেশি।                    

**লাইফ সাইকেল**                                   
সার্ভলেটের বিভিন্ন ধাপে তার লাইফ সাইকেল সম্পন্ন হয়। সাধারণভাবে বলতে গেলে এটা আমরা ৩ ভাগে বিভক্ত করতে পারি। সেগুলো হলঃ                                     
১. সার্ভলেট শুরু হয়  init() মেথড কলের মাধ্যমে।                      
২. সার্ভলেট ক্লায়েন্ট রিকুয়েস্ট প্রসেস করে service() মেথড কলের মাধ্যমে।                           
৩. সার্ভলেট টার্মিনেট হয় destroy() মেথড কলের মাধ্যমে।                     

**init() মেথড**                       
সার্ভলেট রিকুয়েস্ট আসার পর init() মেথড একবার ই কল করা হয়। এটা হল একবারে শুরুর মেথড।                                           

```
public void init() throws ServletException {
   // Initialization code...
}
```

**service() মেথড**                     
service() মেথড হল মেইন মেথড সার্ভারের রিকুয়েস্ট রেসপন্স নিয়ন্ত্রন করার জন্য। প্রতিবার ক্লায়েন্ট রিকুয়েস্ট অথবা সার্ভার রেসপন্স পাঠানোর সময় service() মেথড কল করা হয়। service() মেথড HTTP রিকুয়েস্টের ধরন চেক করে যেমনঃ GET, POST, PUT, DELETE এবং সেই অনুসারে doGet, doPost, doPut, doDelete মেথড কল করে।                     

```
public void service(ServletRequest request, ServletResponse response) 
   throws ServletException, IOException {
}
```

**doGet() মেথড**              
যদি কোন get রিকুয়েস্ট পাঠানো হয় কিন্তু মেথডের নাম উল্লেখ করা না থাকে তাহলে ডিফল্টভাবে doGet() মেথড কল হয়।        

```
public void doGet(HttpServletRequest request, HttpServletResponse response)
   throws ServletException, IOException {
   // Servlet code
}
```

**doPost() মেথড**                          
যদি কোন post রিকুয়েস্ট পাঠানো হয় কিন্তু মেথডের নাম উল্লেখ করা না থাকে তাহলে ডিফল্টভাবে doPost() মেথড কল হয়।        

```
public void doPost(HttpServletRequest request, HttpServletResponse response)
   throws ServletException, IOException {
   // Servlet code
}
```

**destroy() মেথড**               
যখন সার্ভলেটের কাজ শেষ হয়ে যায় আমরা এই মেথডটি কল করি। এই মেথডের ভেতরে আমরা ডাটাবেজ কানেকশান বন্ধ করা, ব্যাকগ্রাউন্ড থ্রেড বন্ধ করা এবং অন্যান্য কাজ করে নিতে পারে যে গুলো সার্ভলেটের শেষ হওয়ার সাথে সাথে শেষ করা দরকার। destroy() মেথড কল করলে সার্ভলেটটি garbage collection এ চলে যায়।                

```
public void destroy() {
   // Finalization code...
}
```

**সার্ভলেট এপিআই**                   
javax.servlet এবং javax.servlet.http প্যাকেজের ইন্টারফেস আর ক্লাস গুলোই সার্ভলেট এপিআই এর কাজ গুলো করে থাকে। ওয়েব কন্টেইনার এবং সার্ভলেট javax.servlet এর প্যাকেজের ক্লাস আর ইন্টারফেস ব্যবহার করে থাকে। কিন্তু এই ক্ষেত্রে নির্দিষ্ট কোন প্রোটোকল নাই। javax.servlet.http প্যাকেজ শুধুমাত্র http রিকুয়েস্ট নিয়ে কাজ করে। 

কোন সার্ভলেট ক্লাস ৩ ভাবে তৈরি করা যায়। সেগুলো হলঃ                              
১. সার্ভলেট ইন্টারফেস ইমপ্লিমেন্ট করে                         
২. জেনেরিক সার্ভলেট ক্লাস এক্সটেন্ড করে            
৩. এইচটিটিপি সার্ভলেট ক্লাস এক্সটেন্ড করে            

**সার্ভলেট ইন্টারফেস**

```
public class ServletExample implements Servlet {
    ServletConfig config=null;

    public void init(ServletConfig config) throws ServletException {
        this.config = config;
        System.out.println("Servlet is initialized");
    }

    public ServletConfig getServletConfig() {
        return config;
    }

    public void service(ServletRequest request, ServletResponse response) throws ServletException, IOException {
        response.setContentType("text/html");

        PrintWriter out=response.getWriter();
        out.print("<html><body>");
        out.print("<b>hello simple servlet</b>");
        out.print("</body></html>");
    }

    public String getServletInfo() {
        return "copyright sadman";
    }

    public void destroy() {
        System.out.println("Servlet is destroyed");
    }
}
```
 
**জেনেরিক সার্ভলেট**

```
public class GenericExample extends GenericServlet {
    public void service(ServletRequest request, ServletResponse response)
            throws IOException, ServletException {
        response.setContentType("text/html");
        PrintWriter pwriter=response.getWriter();
        pwriter.print("<html>");
        pwriter.print("<body>");
        pwriter.print("<h2>Generic Servlet Demo</h2>");
        pwriter.print("<p>Servlet -> Generic Servlet</p>");
        pwriter.print("</body>");
        pwriter.print("</html>");
    }
}
```

**এইচটিটিপি সার্ভলেট**

```
public class HttpExample extends HttpServlet {
    private String mymsg;

    public void init() throws ServletException {
        mymsg = "Http Servlet Demo";
    }

    public void doGet(HttpServletRequest request, HttpServletResponse response)
            throws ServletException, IOException {
        // Setting up the content type of web page
        response.setContentType("text/html");
        // Writing the message on the web page
        PrintWriter out = response.getWriter();
        out.print("<h2>" + mymsg + "</h2>");
        out.print("<p>Servlet -> Generic Servlet -> Http Servlet</p>");
    }

    public void destroy() {
        System.out.println("Servlet is destroyed");
    }
}
```

**কনফিগারেশন**                                         
web.xml ফাইলে সার্ভলেট ম্যাপিং করতে হয়। অর্থাৎ কোন url এ হিট করলে কোন মেথড এক্সিকিউট হবে এইটাই লেখা থাকে এই ফাইলে। নিচে এই কনফিগারেশনের উদাহরন দেওয়া হলঃ          

```
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">

    <display-name>JavaServlet</display-name>
    <welcome-file-list>
        <welcome-file>index.jsp</welcome-file>
    </welcome-file-list>

    <servlet>
        <servlet-name>Servlet</servlet-name>
        <servlet-class>com.sadman.servlet.ServletExample</servlet-class>
    </servlet>

    <servlet-mapping>
        <servlet-name>Servlet</servlet-name>
        <url-pattern>/servlet</url-pattern>
    </servlet-mapping>

    <servlet>
        <servlet-name>GenericServlet</servlet-name>
        <servlet-class>com.sadman.servlet.GenericExample</servlet-class>
    </servlet>

    <servlet-mapping>
        <servlet-name>GenericServlet</servlet-name>
        <url-pattern>/generic</url-pattern>
    </servlet-mapping>

    <servlet>
        <servlet-name>HttpServlet</servlet-name>
        <servlet-class>com.sadman.servlet.HttpExample</servlet-class>
    </servlet>

    <servlet-mapping>
        <servlet-name>HttpServlet</servlet-name>
        <url-pattern>/http</url-pattern>
    </servlet-mapping>

</web-app>
```      

index.html                
```
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>$Title$</title>
</head>
<body>
    <a href="servlet">Click here to call Servlet</a>
    <br>
    <a href="generic">Click here to call Generic Servlet</a>
    <br>
    <a href="http">Click here to call Http Servlet</a>
</body>
</html>
```            

























