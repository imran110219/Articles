# স্টেট প্যাটার্ন (State Pattern)                  
স্টেট প্যাটার্ন হল বিহ্যাভিওরাল ডিজাইন প্যাটার্ন যেটা একটা অবজেক্টের স্বভাব পরিবর্তন করে দেয় তার স্টেট পরিবর্তনের সাথে সাথে। এক কথায় অবজেক্ট তার নিজের ক্লাস পরিবর্তন করবে।              

**উদাহরন**                    
১. javax.faces.lifecycle.LifeCycle স্টেট প্যাটার্ন ফলো করে তৈরি করা।       

**সমস্যা**                       
যদি আমাদের এমন একটা ডিজাইন প্যাটার্নের প্রয়োজন হয় যে একটা অবজেক্ট বিভিন্ন ক্লাসের অবজেক্ট হিসেবে কাজ করবে। সাধারনভাবে একটা অবজেক্ট একটা নির্দিষ্ট ক্লাসের থেকেই তৈরি হয়। অবজেক্টের ক্লাস টাইপ পরিবর্তন করা সাধারনভাবে সম্ভব নয়।         
     
**সমাধান**                                     
স্টেট প্যাটার্ন অনুযায়ী যেটা সমাধান সেটা হল যত ধরনের স্টেট আছে তার ক্লাস বানানো। সেটার জন্য আমাদের একটা ইন্টারফেস State নামে। এটাকে ইমপ্লিমেন্ট করে সব ক্লাস গুলো বানাতে হবে। যেই অবজেক্ট বিভিন্ন স্টেটে থাকবে সেই অবজেক্টের ভেতরে State অবজেক্ট স্টোর করে রাখতে হবে। 

**ইমপ্লিমেন্টেশন**                
```
public interface State {
    public void updateState(DeliveryContext ctx);
}
```

```
public class Acknowledged implements State
{
    //Singleton
    private static Acknowledged instance = new Acknowledged();

    private Acknowledged() {}

    public static Acknowledged instance() {
        return instance;
    }

    //Business logic and state transition
    @Override
    public void updateState(DeliveryContext ctx)
    {
        System.out.println("Package is acknowledged !!");
        ctx.setCurrentState(Shipped.instance());
    }
}
```

```
public class Shipped implements State
{
    //Singleton
    private static Shipped instance = new Shipped();

    private Shipped() {}

    public static Shipped instance() {
        return instance;
    }

    //Business logic and state transition
    @Override
    public void updateState(DeliveryContext ctx)
    {
        System.out.println("Package is shipped !!");
        ctx.setCurrentState(InTransition.instance());
    }
}
```

```
public class InTransition implements State
{
    //Singleton
    private static InTransition instance = new InTransition();

    private InTransition() {}

    public static InTransition instance() {
        return instance;
    }

    //Business logic and state transition
    @Override
    public void updateState(DeliveryContext ctx)
    {
        System.out.println("Package is in transition !!");
        ctx.setCurrentState(OutForDelivery.instance());
    }
}
```

```
public class OutForDelivery implements State
{
    //Singleton
    private static OutForDelivery instance = new OutForDelivery();

    private OutForDelivery() {}

    public static OutForDelivery instance() {
        return instance;
    }

    //Business logic and state transition
    @Override
    public void updateState(DeliveryContext ctx)
    {
        System.out.println("Package is out of delivery !!");
        ctx.setCurrentState(Delivered.instance());
    }
}
```

```
public class Delivered implements State
{
    //Singleton
    private static Delivered instance = new Delivered();

    private Delivered() {}

    public static Delivered instance() {
        return instance;
    }

    //Business logic
    @Override
    public void updateState(DeliveryContext ctx)
    {
        System.out.println("Package is delivered!!");
    }
}
```

```
public class DeliveryContext {
    private State currentState;
    private String packageId;

    public DeliveryContext(State currentState, String packageId)
    {
        super();
        this.currentState = currentState;
        this.packageId = packageId;

        if(currentState == null) {
            this.currentState = Acknowledged.instance();
        }
    }

    public State getCurrentState() {
        return currentState;
    }

    public void setCurrentState(State currentState) {
        this.currentState = currentState;
    }

    public String getPackageId() {
        return packageId;
    }

    public void setPackageId(String packageId) {
        this.packageId = packageId;
    }

    public void update() {
        currentState.updateState(this);
    }
}
```

**সুবিধা - অসুবিধা**             
* এটা Single Responsibility Principle মেনে চলে।            
* 