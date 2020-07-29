# এডাপ্টার প্যাটার্ন (Adapter Pattern)   
এডাপ্টার প্যাটার্ন হল স্ট্রাকচারাল ডিজাইন প্যাটার্ন যা এমন একটা ডিজাইন প্যাটার্ন যেটা একটা অবজেক্টকে ভিন্ন ভিন্ন ইন্টারফেসের সাথে কাজ করতে পারে। অর্থাৎ একটা অবজেক্ট যখন বিভিন্ন ইন্টারফেসের সাথে এডাপ্ট বা মানিয়ে নেয়।                

**উদাহরন**                    
১. java.util.Arrays#asList() এডাপ্টার প্যাটার্ন ফলো করে তৈরি করা।                                     
২. java.util.Collections#list() ও একইভাবে তৈরি।

**সমস্যা**         
আমাদের দৈনন্দিন জীবনে বিদ্যুতের লাইন ব্যবহার করতে হয়। এখন বিদ্যুতের লাইনে ১২০ ভোল্ট থাকে যদি আমাদের তখন বিভিন্ন সকেটে ভিন্ন ভিন্ন ভোল্ট প্রয়োজন হবে যেমনঃ ১২, ৩ ভোল্ট। তাহলে আমরা তখন কিভাবে এই ১২০ ভোল্ট ব্যবহার করব বিভিন্ন ভোল্টে পরিবর্তন করে।            
     
**সমাধান**                                     
আমাদের যেটা দরকার সেটা হল ১২০ ভোল্টকে বিভিন্ন ভোল্টে কনভার্ট করা। আমাদের একটা এডাপ্টার ক্লাস তৈরি করতে হবে যেখানে ভোল্ট তার প্রয়োজন অনুযায়ী পরিবর্তন করে নেয়। আমরা Adapter ইন্টারফেস তৈরি করব যেটাতে ভোল্ট কনভার্সনের মেথডগুলো থাকবে। এবং এটা আমরা আমাদের সুবিধামত ইমপ্লিমেন্ট করে নেব।  

**ইমপ্লিমেন্টেশন**                
```
public class Volt {
    private int volts;

    public Volt(int v){
        this.volts=v;
    }

    public int getVolts() {
        return volts;
    }

    public void setVolts(int volts) {
        this.volts = volts;
    }
}
```

```
public class Socket {
    public Volt getVolt(){
        return new Volt(120);
    }
}
```

```
public interface SocketAdapter {
    public Volt get120Volt();

    public Volt get12Volt();

    public Volt get3Volt();
}
```

```
public class SocketAdapterImpl implements SocketAdapter{

    private Socket sock = new Socket();

    @Override
    public Volt get120Volt() {
        return sock.getVolt();
    }

    @Override
    public Volt get12Volt() {
        Volt v= sock.getVolt();
        return convertVolt(v,10);
    }

    @Override
    public Volt get3Volt() {
        Volt v= sock.getVolt();
        return convertVolt(v,40);
    }

    private Volt convertVolt(Volt v, int i) {
        return new Volt(v.getVolts()/i);
    }
}
```

```
public class TestAdapter {
    public static void main(String[] args) {

        SocketAdapter sockAdapter = new SocketAdapterImpl();
        Volt v3 = getVolt(sockAdapter,3);
        Volt v12 = getVolt(sockAdapter,12);
        Volt v120 = getVolt(sockAdapter,120);
        System.out.println("v3 volts using Object Adapter="+v3.getVolts());
        System.out.println("v12 volts using Object Adapter="+v12.getVolts());
        System.out.println("v120 volts using Object Adapter="+v120.getVolts());
    }

    private static Volt getVolt(SocketAdapter sockAdapter, int i) {
        switch (i){
            case 3: return sockAdapter.get3Volt();
            case 12: return sockAdapter.get12Volt();
            case 120: return sockAdapter.get120Volt();
            default: return sockAdapter.get120Volt();
        }
    }
}
```

**সুবিধা - অসুবিধা**              
১. এটা সিঙ্গেল রেস্পন্সিবিলিটি প্রিন্সিপাল এবং ওপেন ক্লোজ প্রিন্সিপাল অনুযায়ী ডিজাইন করা।