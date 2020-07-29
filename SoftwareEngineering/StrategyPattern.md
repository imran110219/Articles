# স্ট্রাটেজি প্যাটার্ন (Strategy Pattern)               
স্ট্রাটেজি প্যাটার্ন হল বিহ্যাভিওরাল ডিজাইন প্যাটার্ন যার মাধ্যমে অ্যালগরিদমের সমষ্টি আলাদা আলদা ক্লাসে রাখা হয় এবং প্রয়োজনে অবজেক্টের ক্লাস পরিবর্তন করা যায়।                         
  
**উদাহরন**                    
১. javax.servlet.http.HttpServlet স্ট্রাটেজি প্যাটার্ন ফলো করে তৈরি করা।      

**সমস্যা**         
আমাদের যদি এমন কোন সিস্টেম লাগবে যার দ্বারা আমরা বিভিন্ন সামাজিক যোগাযোগ মাধ্যমে কোন ব্যাক্তির সাথে কানেক্ট হতে পারবো। সেই ক্ষেত্রে আমাদের প্রতিটা সামাজিক মাধ্যমের জন্য আলাদা আলাদা ক্লাস বানানো লাগবে এবং একটা ক্লাস লাগবে সেটা যেন কোন ব্যাক্তির নাম উল্লেখ করলে যেন তার সাথে কানেক্ট হয়ে যায়। তখন যদি আমাদের কোন ক্লাস তার গঠন পরিবর্তন করে ক্লায়েন্টকে তার কোডে ও পরিবর্তন করতে হয়।       
     
**সমাধান**                                     
স্ট্রাটেজি প্যাটার্ন অনুসারে আমাদেরকে একটা ক্লাস তৈরি করতে হবে যার নাম হবে context ক্লাস। এই ক্লাসের ভেতরে সামাজিক যোগাযোগ মাধ্যমের অবজেক্টগুলোর রেফারেন্স সেভ করা থাকেবে। ক্লায়েন্ট তার দরকার অনুযায়ী ফেসবুক/টুইটার তার অবজেক্ট লোড করবে। এই ক্ষেত্রে আমাদের সামাজিক যোগাযোগ মাধ্যমের ক্লাসগুলোর একটা কমন ইন্টারফেস ডিজাইন করতে হবে। পরে প্রয়োজন অনুযায়ী ক্লাস ইমপ্লিমেন্ট করে নিতে হবে। তাহলে আমাদের context ক্লাস জেনেরিক রাখা সম্ভব হবে কারন আমরা ইন্টারফেসের অবজেক্ট লোড করে রাখব।                

**ইমপ্লিমেন্টেশন**               
```
public interface ISocialMediaStrategy {
    public void connectTo(String friendName);
}
```

```
public class SocialMediaContext {
    ISocialMediaStrategy smStrategy;

    public void setSocialmediaStrategy(ISocialMediaStrategy smStrategy)
    {
        this.smStrategy = smStrategy;
    }

    public void connect(String name)
    {
        smStrategy.connectTo(name);
    }
}
```

```
public class FacebookStrategy implements ISocialMediaStrategy {

    public void connectTo(String friendName)
    {
        System.out.println("Connecting with " + friendName + " through Facebook");
    }
}
```

```
public class TwitterStrategy implements ISocialMediaStrategy {

    public void connectTo(String friendName)
    {
        System.out.println("Connecting with " + friendName + " through Twitter");
    }
}
```

```
public class TestStrategy {
    public static void main(String[] args) {

        SocialMediaContext context = new SocialMediaContext();

        context.setSocialmediaStrategy(new FacebookStrategy());
        context.connect("Facebook Name");

        System.out.println("====================");

        context.setSocialmediaStrategy(new TwitterStrategy());
        context.connect("Twitter Name");
    }
}
```

**সুবিধা - অসুবিধা**             
* রান টাইমে অবজেক্টের ভিতর অ্যালগরিদম পরিবর্তন করা যায়।         
* এটা Open/Closed Principle মেনে চলে।     