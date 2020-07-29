# অবজারভার প্যাটার্ন (Observer Pattern)   
অবজারভার প্যাটার্ন হল বিহ্যাভিওরাল ডিজাইন প্যাটার্ন যা এমন একটা সিস্টেম যাতে করে নির্দিষ্ট একাধিক অবজেক্টকে নোটিফিকেশন পাঠানোর প্রক্রিয়া যেই অবজেক্টগুলো লিস্টের অন্তর্ভুক্ত থাকে।                          

**উদাহরন**                    
১. java.util.Observer/java.util.Observable অবজারভার প্যাটার্ন ফলো করে তৈরি করা।                
২. javax.servlet.http.HttpSessionBindingListener ও একইভাবে তৈরি।              

**সমস্যা**         
ধরি আমাদের কাছে দুই ধরনের অবজেক্ট আছে ক্রেতা ও দোকান। উদাহরনস্বরূপ যদি দোকানটা মোবাইলের দোকান হয় এবং ক্রেতা যদি জানতে যায় লেটেস্ট অ্যাপল ফোন কবে বাজারে আসবে। তাহলে ক্রেতা প্রতিদিন দোকানে আসবে খোজ নেওয়ার জন্য কবে লেটেস্ট আইফোন বাজারে আসবে। কিন্তু এই ক্ষেত্রে অধিকাংশ সময় ক্রেতার নষ্ট হবে। একটা উপায় আছে সমস্যা সমাধানের সেটা হল ক্রেতাকে নতুন পন্যের তথ্য ইমেইলে পাঠানো। কিন্তু এই ক্ষেত্রে যদি সব পন্যের আপডেট সব ক্রেতাকে পাঠানো হয় তাহলে এমন অনেক ক্রেতা আছে যারা এই তথ্য জানতে আগ্রহী নন। তখন এই ইমেইলগুলো সেই ক্রেতার বিরক্তির কারন হয়ে যাবে।                                         
     
**সমাধান**                              
এটার সমাধান হল আমাদের প্রথমে দুইটা ইন্টারফেস বানাতে হবে। একটা হল Subject এইটার কাজ হল মেসেজ নোটিফিকেশন পাঠানো এবং Publisher ক্লাস তৈরি করতে হবে Subject ইন্টারফেসকে implement করে। আরেকটা ইন্টারফেস হল Observer/Subscriber যেটা implement করে আমরা যত ইচ্ছা Subscriber বানাতে পারি। এই ক্ষেত্রে আমাদেরকে ডিজাইন করতে হবে ইউটিউব সাবস্ক্রিপশনের মত। একজন ইউজার ইচ্ছা অনুযায়ী তার চ্যানেলগুলোতে সাবস্ক্রাইব করতে পারবে এবং সেই চ্যানেলের আপডেট ইউজার পাবে।                    

**ইমপ্লিমেন্টেশন**                
```
public class Message {

    final String messageContent;

    public Message (String m) {
        this.messageContent = m;
    }

    public String getMessageContent() {
        return messageContent;
    }
}
```

```
public interface Subject {
    public void attach(Observer o);
    public void detach(Observer o);
    public void notifyUpdate(Message m);
}
```

```
public class Publisher implements Subject {

    private List<Observer> observers = new ArrayList<>();

    @Override
    public void attach(Observer o) {
        observers.add(o);
    }

    @Override
    public void detach(Observer o) {
        observers.remove(o);
    }

    @Override
    public void notifyUpdate(Message m) {
        for(Observer o: observers) {
            o.update(m);
        }
    }
}
```

```
public interface Observer {
    public void update(Message m);
}
```

```
public class SubscriberOne implements Observer {
    @Override
    public void update(Message m) {
        System.out.println("MessageSubscriberOne :: " + m.getMessageContent());
    }
}
```

```
public class SubscriberTwo implements Observer {
    @Override
    public void update(Message m) {
        System.out.println("MessageSubscriberTwo :: " + m.getMessageContent());
    }
}
```

**সুবিধা - অসুবিধা**              
* এটা Open/Closed Principle মেনে চলে।                
* Subscriber নোটিফিকেশন পায় random ভাবে।      