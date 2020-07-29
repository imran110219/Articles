# বিল্ডার প্যাটার্ন (Builder Pattern)              
বিল্ডার প্যাটার্ন হল ক্রিয়েশনাল ডিজাইন প্যাটার্ন যেটা কোন জটিল অবজেক্ট ধাপে ধাপে তৈরি করে। এই প্যাটার্ন ব্যবহার করে অবজেক্টের বিভিন্ন অংশ তৈরি করা যায় আলাদাভাবে একই কন্সট্রাকশান কোডের মাধ্যমে।            
 
**উদাহরন**                    
১. javax.json.Json এবং javax.json.JsonBuilder ক্লাস দুইটি বিল্ডার প্যাটার্ন ফলো করে তৈরি করা।           

**সমস্যা**         
আমাদের যদি এমন একটা বাড়ি বানাতে হয় যেটা বিভিন্ন রকম ফিচার থাকে। কিন্তু যখন বাড়ি বানাবো একটা একটা বাড়ি ভিন্ন ভিন্ন রকম হতে পারে। ধরুন যেমন একটা বাড়িতে শধু ঘর থাকবে, একটাতে সুইমিং পুল থাকবে, একটাতে গ্যারেজ থাকবে আবার কোনটাতে দুইটাই থাকবে। তো এই ক্ষেত্রে আমরা সাধারণভাবে যেটা চিন্তা করি সেটা হল ইনহেরিটেন্স। অর্থাৎ বাড়ির একটা প্যারেন্ট ক্লাস থাকবে এবং প্যারেন্ট ক্লাসে সাধারন প্যারামিটার থাকবে যেমন দেয়াল, ছাদ, মেঝে ইত্যাদি। আর আমাদের যেমন বাড়ি দরকার হবে সেটা আমরা প্যারেন্ট ক্লাসকে এক্সটেন্ড করে নেব এবং প্রয়োজন অনুযায়ী বিভিন্ন প্যারামিটার তৈরি করে নেব। কিন্তু এই পদ্ধতি অনুসরন করলে একটা একটা অবজেক্টের একটা একটা ক্লাস বানাতে হবে। এটা কোন ভাল সমাধান হতে পারে না।                        

**সমাধান**                                     
বিল্ডার প্যাটার্ন ব্যবহার করে আমরা উক্ত সমস্যার সমাধান করতে পারি খুব সহজেই। এই প্যাটার্নে একটা builder ক্লাস তৈরি করতে হয়। তারপর ওই ক্লাসের কন্সট্রাক্টর আর মেথড লিখতে হবে। কন্সট্রাক্টরে প্রাথমিক প্যারামিটার দিতে হবে যেমন একটি বাড়িতে দেওয়াল আর দরজা অবশ্যই থাকবে। তো এই দুইটা কন্সট্রাক্টরে তৈরি করতে হবে। আর বাকি প্যারামিটারগুলো যেমন বাড়ির সঙ্গে বাগান, গ্যারেজ এই গুলো থাকতে ও পারে আবার না ও পারে। এই গুলোর বানানোর মেথড থাকবে যেটা ইচ্ছামত সংযুক্ত করে নেওয়া যেতে পারে। পড়ে এই builder ক্লাসের অবজেক্টকে House এর কন্সট্রাক্টরের ভেতর পাস করতে হবে।                                             

**ইমপ্লিমেন্টেশন**                

```
public class House {
    //All final attributes
    private final int walls; // required
    private final int doors; // required
    private final int windows; // optional
    private final int garden; // optional
    private final int garage; // optional

    private House(HouseBuilder houseBuilder){
        this.walls = houseBuilder.walls;
        this.doors = houseBuilder.doors;
        this.windows = houseBuilder.windows;
        this.garden = houseBuilder.garden;
        this.garage = houseBuilder.garage;
    }

    @Override
    public String toString() {
        return "House: has "+this.walls+" walls, "+
                this.doors+" doors, "+
                this.windows+" windows, "+
                this.garden+" sized garden, "+
                this.garage+" sized garage";
    }

    public static class HouseBuilder{
        private final int walls;
        private final int doors;
        private int windows;
        private int garden;
        private int garage;

        public HouseBuilder(int wallNumber, int doorNumber){
            this.walls = wallNumber;
            this.doors = doorNumber;
        }

        public HouseBuilder windows(int windowNumber){
            this.windows = windowNumber;
            return this;
        }

        public HouseBuilder garden(int gardenSize){
            this.garden = gardenSize;
            return this;
        }

        public HouseBuilder garage(int garageSize){
            this.garage = garageSize;
            return this;
        }

        public House build() {
            House house =  new House(this);
            return house;
        }
    }
}
```

```
public class TestBuilder {
    public static void main(String[] args) {
        House house1 = new House.HouseBuilder(6,1).windows(2).build();
        System.out.println(house1);

        House house2 = new House.HouseBuilder(6,1).windows(2).garage(40).build();
        System.out.println(house2);
    }
}
```

Output               
```
House: has 6 walls, 1 doors, 2 windows, 0 sized garden, 0 sized garage
House: has 6 walls, 1 doors, 2 windows, 0 sized garden, 40 sized garage
```


**সুবিধা - অসুবিধা**              
* এটা ফলো করে কোন অবজেক্টকে ধাপে ধাপে তৈরি করা যায়।                    
* একই ধরনের কন্সট্রাকশান কোড ব্যবহার করে বিভিন্ন ধরনের অবজেক্ট তৈরি করা যায়।     

