 # জাভা জেডিবিসি  

* জেডিবিসি ভূমিকা
* জেডিবিসি ড্রাইভার এবং টাইপস
* কানেকশান
* স্ট্যাটমেন্ট
* কুয়েরি
* রেজাল্টসেট
* ট্রানসেকশান
* ব্যাচ প্রসেসিং 
* সারসংক্ষেপ


**জেডিবিসি**

জেডিবিসি(JDBC) এর পূর্ণরূপ হল জাভা ডাটাবেজ কানেক্টিভিটি। জেডিবিসি হল একটা জাভা এপিআই যেটা জাভা প্রোগ্রাম আর ডাটাবেজের মধ্যে একটা ব্রিজ হিসেবে কাজ করে। এটা জাভা স্ট্যান্ডার্ড এডিশনের অন্তর্ভুক্ত। জেডিবিসি ড্রাইভার ব্যবহার করে জাভা কোড লিখে আমরা যেকোন রিলেশনাল ডাটাবেজ(sql, mysql) থেকে ডাটা পড়ে আনা(read) এবং ডাটা লেখা(write) করা যায়। 

জেডিবিসি ড্রাইভার ব্যবহার করে আমরা জাভা প্রোগ্রাম দিয়ে ৩ টা প্রধান কাজ করতে পারিঃ	

১. ডাটাবেজে সংযোগ স্থাপন করতে পারি। 

২. কুয়েরি এক্সিকিউট করা এবং ডাটাবেজের তথ্য হালনাগাদ করতে পারি। 

৩. ডাটাবেজের কোন কুয়েরি অপারেশনের ফলাফল পেতে পারি। 

	
**জেডিবিসি ড্রাইভার এবং টাইপস (JDBC Driver and Types)**

জেডিবিসি ড্রাইভার হল চার ধরনেরঃ

1. JDBC-ODBC Bridge Driver
2. Native-API Driver
3. Network Protocol Driver
4. Thin Driver

**১. জেডিবিসি-ওডিবিসি ব্রিজ ড্রাইভার**

জেডিবিসি-ওডিবিসি ব্রিজ ড্রাইভার ওডিবিসি(ODBC) ড্রাইভার কে ব্যবহার করে ডাটাবেজে কানেক্ট হওয়ার জন্য। জেডিবিসি-ওডিবিসি ব্রিজ ড্রাইভার জেডিবিসি মেথড কল কে ওডিবিসি ফাংশন কলে রুপান্তরিত করে। ওডিবিসি এর পূর্ণরূপ ওপেন ডাটাবেজ কানেক্টিভিটি এবং এটা সব ল্যাঙ্গুয়েজ ও প্লাটফর্মে চলে।  জেডিবিসি-ওডিবিসি ব্রিজ ড্রাইভার কে ইউনিভার্সাল ড্রাইভার ও বলা হয়ে থাকে কারন এটা সব ডাটাবেজে চলে। কিন্তু জাভা ৮ ভার্সনে এই ড্রাইভার টা বাদ দিয়ে দেওয়া হয়েছে। 

**২. নেটিভ-এপিআই ড্রাইভার**

নেটিভ-এপিআই ড্রাইভার ডাটাবেজের ক্লাইন্ট সাইড লাইব্রেরী ব্যবহার করে থাকে। এই ড্রাইভার জেডিবিসি মেথড কল কে যেই ডাটাবেজের এপিআই এর নেটিভ কলে রুপান্তরিত করে। প্রতিটা ডাটাবেজের নিজের লোকাল এপিআই আছে, এই ড্রাইভার সেটা ব্যবহার করে কাজ সম্পন্ন করে থাকে। 

**৩. নেটওয়ার্ক প্রোটোকল ড্রাইভার**

নেটওয়ার্ক প্রোটোকল ড্রাইভার middleware (অ্যাপ্লিকেশন সার্ভার) এর মাধ্যমে জেডিবিসি কল কে সরাসরি বা পরোক্ষভাবে নির্দিষ্ট ডাটাবেজ প্রোটোকলে কনভার্ট করে নেয়। এটা পুরোটা জাভা প্রগ্রামে লেখা হয়। 

**৪. থিন ড্রাইভার**

থিন ড্রাইভার সরাসরি জেডিবিসি কল কে নির্দিষ্ট ডাটাবেজ প্রোটোকলে কনভার্ট করে। এর জন্য তাকে কোন নেটিভ ডাটাবেজ লাইব্রেরীর দরকার পড়ে না।  এর মাঝখানে আর কোন লেয়ার নেই এজন্যই একে থিন ড্রাইভার বলে। 


**কানেকশান**

জেডিবিসি এর মাধ্যমে ডাটাবেজে সংযোগ স্থাপন করতে হলে কয়েকটা ধাপ আছে। নিচে সেগুলোর বর্ণনা তুলে ধরা হলঃ

ধাপ ১ - জেডিবিসি প্যাকেজ ইমপোর্ট করতে হবে। 

```package
import java.sql.* ; 
```

ধাপ ২ - আমরা যে ডাটাবেজে কানেক্ট হতে চাই সেই ডাটাবেজের ড্রাইভার ক্লাসকে রেজিস্টার করতে হবে। এটা দুইভাবে করা যায়ঃ 

```driver class 1
Class.forName("com.mysql.jdbc.Driver");  // for mysql 
```

অথবা 

```driver class 2
Driver myDriver = new com.mysql.jdbc.Driver();  // for mysql
DriverManager.registerDriver( myDriver );
```

ধাপ ৩ - কানেকশান অবজেক্ট তৈরী করতে হবে DriverManager.getConnection() মেথড ব্যবহার করে। এই মেথডের ৩ টি overloaded মেথড আছে। 

১. এর জন্য আমাদের দরকার যেই ডাটাবেজে কানেক্ট হব তার url, username আর password.

```connection object 1
Connection con=DriverManager.getConnection("jdbc:mysql://localhost:3306/test","root","12345678");  // parameter -> url, username & password
```

২. এর জন্য আমাদের দরকার শুধু url.

```connection object 2
Connection con=DriverManager.getConnection("jdbc:mysql://localhost:3306/test?user=root&password=12345678"); // parameter -> url
```

৩. এর জন্য আমাদের দরকার শুধু url এবং properties অবজেক্ট।

```connection object 3
Properties info = new Properties();
info.put("user", "root");
info.put("password", "12345678");
Connection con=DriverManager.getConnection("jdbc:mysql://localhost:3306/test",info);  // parameter -> url, properties
```

ধাপ ৪ - কাজ শেষ হওয়ার পর কানেকশান বন্ধ করে দিতে হবে। 

```connection close
conn.close();
```


**স্ট্যাটমেন্ট**

স্ট্যাটমেন্ট হল ইন্টারফেস। এই ইন্টারফেসের মেথড ব্যবহার করে কুয়েরি এক্সকিউট করা যায়। স্ট্যাটমেন্ট অবজেক্ট তৈরি করতে হয় কানেকশান অবজেক্ট ব্যবহারের মাধ্যমে। ৩ ধরনের স্ট্যাটমেন্ট ইন্টারফেস আছেঃ

**১. Statement**
এটা ব্যবহার করা হয় ডাটাবেজে সাধারণভাবে অ্যাক্সেস করার জন্য। এটি রান টাইমে কুয়েরি এক্সিউট করে থাকে। এই ইন্টারফেস কোন প্যারামিটার ইনপুট নেয় না। 

```Statement
Statement stmt=con.createStatement();
ResultSet rs=stmt.executeQuery("select * from user");
```

**২. PreparedStatement**
যখন একটা কুয়েরি অনেকবার ব্যবহার করার প্রয়োজন পড়ে তখন এই ইন্টারফেসের দরকার হয়। PreparedStatement হল Statement এর এক্সটেনশন। এটা রান টাইমে প্যরামিটার ইনপুট নেয়। এই ইন্টারফেসের ফাংশানালিটি এবং সুযোগ-সুবিধা জেনেরিক Statement থেকে কিছু বেশি।

```PreparedStatement
String sql = "update user set author=? where id=?";
PreparedStatement stmt = con.prepareStatement(sql);
```

**৩. CallableStatement**
যখন আমাদের ডাটাবেজের stored procedure অ্যাক্সেস করার প্রয়োজন হয় তখন আমরা এই ইন্টারফেস ব্যবহার করি। এটিও রান টাইমেপ্যরামিটার ইনপুট নেয়।

```CallableStatement
String sql = "{call getAuthor (?, ?)}";
CallableStatement stmt = con.prepareCall(sql);
```

কাজ শেষ হওয়ার পর  Statement close করে দিতে হবে। 

```Statement close
stmt.close();
```


**রেজাল্টসেট**

ResultSet এর অবজেক্ট তৈরী করতে দরকার হয় Statement এর অবজেক্টের। এর ভেতরে ডাটাবেজ থেকে পড়ে আনা ভ্যালু রাখা হয়। 

**রেজাল্টসেটের প্রকারভেদ**

১. ResultSet.TYPE_FORWARD_ONLY - এটা হল ডিফল্ট প্যরামিটার। cursor এই ক্ষেত্রে ফরওয়ার্ড মুভ করবে। 

২. ResultSet.TYPE_SCROLL_INSENSITIVE - cursor এই ক্ষেত্রে ফরওয়ার্ড অথবা ব্যাকওয়ার্ড দুদিকেই মুভ করতে পারবে।  এই রেসাল্টসেট সেনসিটিভ না অর্থাৎ রেসাল্টসেট তৈরি হবার পর ও পরিবর্তন করা যাবে। 

৩. ResultSet.TYPE_SCROLL_SENSITIVE - cursor এই ক্ষেত্রে ফরওয়ার্ড অথবা ব্যাকওয়ার্ড দুদিকেই মুভ করতে পারবে।  এই রেসাল্টসেট সেনসিটিভ অর্থাৎ রেসাল্টসেট তৈরি হবার পর পরিবর্তন করা যাবে না।

**রেজাল্টসেট কনকারেন্সি**

১. ResultSet.CONCUR_READ_ONLY - এটা শুধুমাত্র রিড করা যাবে এমন রেসাল্টসেট তৈরী করে। এটাই ডিফল্টভাবে থাকে। 

২. ResultSet.CONCUR_UPDATABLE - এটা আপডেট করা যাবে এমন রেসাল্টসেট তৈরী করে। 

**রেজাল্টসেট অবজেক্ট মেথডের প্রকারভেদ**

১. Navigational Methods - cursor অবস্থান পরিবর্তনের জন্য ব্যবহার করা হয়। 	

২. Getter/Reader Methods - যেই row তে cursor আছে সেই row এর ডাটা পড়ে আনার জন্য ব্যবহার করা হয়।  

৩. Setter/Updater Methods - যেই row তে cursor আছে সেই row এর ডাটা update করার জন্য ব্যবহার করা হয়।  

**১. Navigational Methods**
* beforeFirst() - cursor প্রথম row এর আগে চলে যাবে
* afterLast() - cursor শেষ row এর পরে চলে যাবে
* first() - cursor প্রথম row তে চলে যাবে
* last() - cursor শেষ row তে চলে যাবে
* absolute(int row) - cursor প্যারামিটারে যে নাম্বার দেওয়া আছে সেই row তে যাবে 
* relative(int row) - cursor তার বর্তমান অবস্থান থেকে প্যারামিটারে যে নাম্বার দেওয়া আছে সেই অনুযায়ী ফরওয়ার্ড অথবা ব্যাকওয়ার্ড row তে যাবে
* previous()- cursor তার আগের row তে চলে যাবে
* next() - cursor তার পরের row তে চলে যাবে
* getRow() - cursor এর বর্তমান row নাম্বার রিটার্ন করবে 
* moveToInsertRow() - cursor নতুন insert হওয়া row তে চলে যাবে 
* moveToCurrentRow() - cursor যদি insert হওয়া row তে থাকে তাহলে current row তে চলে যাবে

**২. Getter/Reader Methods**
এই মেথড গুলো যত ধরনের ডাটা টাইপ আছে ততো ধরনের হয়। এখানে শুধু ইন্টিজার এর ক্ষেত্রে দেখানো হল। 
* getInt(String columnName) - cursor যে row তে আছে সেই row এর ইন্টিজার ভ্যালু রিটার্ন করবে এবং প্যরামিটার হিসেবে যাবে কলামের নাম  
* getInt(int columnIndex) - cursor যে row তে আছে সেই row এর ইন্টিজার ভ্যালু রিটার্ন করবে এবং প্যরামিটার হিসেবে যাবে কলামের ইন্ডেক্স নাম্বার 

**৩. Setter/Updater Methods**
এখানে শুধু স্ট্রিং এর ক্ষেত্রে দেখানো হল। 
* updateString(int columnIndex, String s) - cursor যে row তে আছে সেই row এর ভ্যালু আপডেট হবে এবং প্যরামিটার হিসেবে যাবে কলামের ইন্ডেক্স নাম্বার এবং যে স্ট্রিং টা ওভারল্যাপ করবে
* updateString(String columnName, String s) - cursor যে row তে আছে সেই row এর ভ্যালু আপডেট হবে এবং প্যরামিটার হিসেবে যাবে কলামের নাম এবং যে স্ট্রিং টা ওভারল্যাপ করবে

* updateRow() - বর্তমানে cursor যে row তে আছে সেই row আপডেট হবে 
* deleteRow() - বর্তমানে cursor যে row তে আছে সেই row ডিলিট হবে
* refreshRow() - বর্তমানে cursor যে row তে আছে সেই row রিফ্রেশ হবে
* cancelRowUpdates() - row এর আপডেট বাতিল হবে 
* insertRow() - নতুন row যুক্ত হবে ডাটাবেজে 


**ট্রানসেকশান**

Transaction হল ডাটাবেজে কোন কমান্ড পাঠানোর শেষ ধাপ। ট্রানসেকশান সাধারণত অটোমেটিকালি হয়ে থাকে। কিন্তু এটাকে ম্যানুয়ালি করতে চাইলে কানেকশান অবজেক্টের setAutoCommit(false) এই মেথড টা কল করলেই হয়। কানেকশান ইন্টারফেসে ৩ টা মেথড আছে ট্রানসেকশান ম্যানেজ করার জন্য। সেগুলো হলঃ
* void setAutoCommit(boolean status) - এটা যদি আমরা না লিখি প্রোগ্রামে তাহলে true হিসেবে থাকে। 
* void commit()	- ট্রানসেকশান সম্পন্ন করে। 
* void rollback() - ট্রানসেকশান বাতিল করে দেয়। 


```Transaction
try{
   con.setAutoCommit(false);
   Statement stmt = con.createStatement();
   
   String SQL = "INSERT INTO Employees  " +
                "VALUES (106, 20, 'Rita', 'Tez')";
   stmt.executeUpdate(SQL);  
   
   //ভুল sql কমান্ড submit হবে 
   String SQL = "INSERTED IN Employees  " +
                "VALUES (107, 22, 'Sita', 'Singh')";
   stmt.executeUpdate(SQL);
   // যদি কোন error না পায় 
   con.commit();
}catch(SQLException se){
   // যদি কোন error পায় 
   con.rollback();
}
```


**ব্যাচ প্রসেসিং**  
ব্যাচ প্রসেসিং হল যখন্ অনেকগুলো sql স্ট্যাটমেন্ট একটা ব্যাচে রাখা হয় এবং সেগুলো একসাথে ডাটাবেজে পাঠানো হয়। এটার পারফরম্যান্স  ও ভাল হয়। ব্যাচ প্রসেসিং করা দুইভাবে করা যায়ঃ

* স্ট্যাটমেন্ট অবজেক্টের মাধ্যমে
* প্রিপেয়ারড স্ট্যাটমেন্ট অবজেক্টের মাধ্যমে

**Statement Object**
```Statement
Statement stmt = conn.createStatement();
conn.setAutoCommit(false);

String SQL1 = "INSERT INTO user (id, title, author) " +
             "VALUES(1,'Mr', 'Ali')";
stmt.addBatch(SQL1);

String SQL2 = "INSERT INTO  user (id, title, author) " +
             "VALUES(1,'Mr', 'Ali')";
stmt.addBatch(SQL2);

String SQL3 = "UPDATE Employees SET age = 35 " +
             "WHERE id = 100";
stmt.addBatch(SQL3);

int[] count = stmt.executeBatch();
conn.commit();
```


**PrepareStatement Object**
```PrepareStatement
String SQL = "INSERT INTO user (id, title, author) " +
             "VALUES(?, ?, ?)";

PreparedStatemen pstmt = conn.prepareStatement(SQL);
conn.setAutoCommit(false);

pstmt.setInt( 1, 1 );
pstmt.setString( 2, "Mr" );
pstmt.setString( 3, "Rafiq" );
pstmt.addBatch();

pstmt.setInt( 1, 2 );
pstmt.setString( 2, "Mr" );
pstmt.setString( 3, "Habib" );
pstmt.addBatch();

int[] count = stmt.executeBatch();
conn.commit();
```

**সারসংক্ষেপ**

এখানে মোটামুটি বেসিক বিষয় গুলো আলোচনা করা হয়েছে। যদি আরো কিছু জানার থাকে যা এখানে আলোচনা করা হয় নি, তাহলে ওরাকলের সাইটে জেবিসির অফিসিয়াল ডকুমেন্টেশন দেখতে পারেন। 

