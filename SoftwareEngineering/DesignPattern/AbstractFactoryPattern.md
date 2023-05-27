# অ্যাবস্ট্রাক্ট ফ্যাক্টরি প্যাটার্ন (Abstract Factory Pattern)                    
অ্যাবস্ট্রাক্ট ফ্যাক্টরি হল ক্রিয়েশনাল ডিজাইন প্যাটার্ন যেটা বিভিন্ন ধরনের অবজেক্ট তৈরি করে এমন একটা ইন্টারফেস থেকে যেখানে অবজেক্ট গুলো ক্যাটেগরি এবং সাব ক্যাটেগরিতে বিভক্ত থাকে।                

**উদাহরন**                    
১. javax.xml.parsers.DocumentBuilderFactory এবং javax.xml.transform.TransformerFactory ক্লাস দুইটি অ্যাবস্ট্রাক্ট ফ্যাক্টরি প্যাটার্ন ফলো করে তৈরি করা। 

**সমস্যা**         
ধরি আমাদেরকে ফার্নিচারের ফ্যাক্টরি বানাতে হবে। তাহলে আমরা ফ্যাক্টরি মেথড প্যাটার্নের মত একটা ফ্যাক্টরি বানাতে পারি। আমাদের ফার্নিচার ৩ ধরনের - চেয়ার, সোফা ও কফি টেবিল। তাহলে আমরা এখন ফ্যাক্টরি মেথড প্যাটার্নের মত করে ফার্নিচার ফ্যাক্টরি মেথড বানাতে পারবো। কিন্তু এখন আমাদের যদি বিভিন্ন স্টাইলের ফার্নিচার বানাতে হয় যেমনঃ মডার্ন, ভিক্টোরিয়ান, আর্টডেকো। সেই ক্ষেত্রে ডিজাইন টা আরো জটিল হয়ে যাবে কারন চেয়ারের স্টাইল ৩ ধরনের হতে পারে, একইভাবে সোফার স্টাইল ও ৩ ধরনের হতে পারে আবার কফি টেবিলের ও। তো এই ক্ষেত্রে আমাদের ডিজাইন করতে হবে এই সব কিছু মাথায় রেখেই।                   

**সমাধান**                                     
অ্যাবস্ট্রাক্ট ফ্যাক্টরি প্যাটার্ন  প্রথমে আমাদের যেটা ফলো করতে বলে সেটা হল একটা ইন্টারফেস যার ভেতরে ৩ ধরনের স্টাইলের (মডার্ন, ভিক্টোরিয়ান, আর্টডেকো) অ্যাবস্ট্রাক্ট টাইপের ফ্যাক্টরি মেথড বানাতে হবে। তারপর আমাদেরকে এক একটা অ্যাবস্ট্রাক্ট মেথডের ভেতর ৩ ধরনের ফার্নিচার (চেয়ার, সোফা, কফি টেবিল) বানানোর ইন্টারফেস বানাতে হবে। সেই ইন্টারফেসগুলো চেয়ার, সোফা, কফি টেবিলের অবজেক্ট তৈরি করে। এই জন্যই এটাকে বলে অ্যাবস্ট্রাক্ট ফ্যাক্টরি প্যাটার্ন  কারন একটা ফ্যাক্টরি মেথডের ভেতর আরও অনেকগুলো ফ্যাক্টরি মেথড লেখা থাকে।                         

**ইমপ্লিমেন্টেশন**                

```
public enum Style {
    MODERN, VICTORIAN, ARTDECO
}
```

```
public enum FurnitureType {
    CHAIR, SOFA, COFFEETABLE
}
```

```
public abstract class Furniture {
    public Furniture(FurnitureType model) {

    }

    public Furniture(FurnitureType chair, Style style) {
    }

    private void arrangeParts() {
        // Do one time processing here
    }

    protected abstract void construct();

    protected abstract void construct(Style style);

    private FurnitureType model = null;

    public FurnitureType getModel() {
        return model;
    }

    public void setModel(FurnitureType model) {
        this.model = model;
    }
}
```

```
public class Chair extends Furniture {
    public Chair() {
        super(FurnitureType.CHAIR);
        construct();
    }

    public Chair(Style style) {
        super(FurnitureType.CHAIR, style);
        construct(style);
    }

    @Override
    protected void construct() {
        System.out.println("Building Chair");
    }

    @Override
    protected void construct(Style style) {
        System.out.println("Building " + style + " Chair");
        // add accessories
    }
}
```

```
public class CoffeeTable extends Furniture {
    public CoffeeTable() {
        super(FurnitureType.CHAIR);
        construct();
    }

    public CoffeeTable(Style style) {
        super(FurnitureType.CHAIR, style);
        construct(style);
    }

    @Override
    protected void construct() {
        System.out.println("Building Coffee Table");
    }

    @Override
    protected void construct(Style style) {
        System.out.println("Building " + style + " Coffee Table");
    }
}
```

```
public class Sofa extends Furniture {
    public Sofa() {
        super(FurnitureType.CHAIR);
        construct();
    }

    public Sofa(Style style) {
        super(FurnitureType.CHAIR, style);
        construct(style);
    }

    @Override
    protected void construct() {
        System.out.println("Building Sofa");
    }

    @Override
    protected void construct(Style style) {
        System.out.println("Building "+ style +" Sofa");
    }
}
```

```
public class ArtDecoFurnitureFactory {
    public static Furniture buildFurniture(FurnitureType model)
    {
        Furniture furniture = null;
        switch (model)
        {
            case CHAIR:
                furniture = new Chair(Style.ARTDECO);
                break;

            case SOFA:
                furniture = new Sofa(Style.ARTDECO);
                break;

            case COFFEETABLE:
                furniture = new CoffeeTable(Style.ARTDECO);
                break;

            default:
                //throw some exception
                break;
        }
        return furniture;
    }
}
```

```
public class ModernFurnitureFactory {
    public static Furniture buildFurniture(FurnitureType model)
    {
        Furniture furniture = null;
        switch (model)
        {
            case CHAIR:
                furniture = new Chair(Style.MODERN);
                break;

            case SOFA:
                furniture = new Sofa(Style.MODERN);
                break;

            case COFFEETABLE:
                furniture = new CoffeeTable(Style.MODERN);
                break;

            default:
                //throw some exception
                break;
        }
        return furniture;
    }
}
```

```
public class VictorianFurnitureFactory {
    public static Furniture buildFurniture(FurnitureType model)
    {
        Furniture furniture = null;
        switch (model)
        {
            case CHAIR:
                furniture = new Chair(Style.VICTORIAN);
                break;

            case SOFA:
                furniture = new Sofa(Style.VICTORIAN);
                break;

            case COFFEETABLE:
                furniture = new CoffeeTable(Style.VICTORIAN);
                break;

            default:
                //throw some exception
                break;
        }
        return furniture;
    }
}
```

```
public class FurnitureFactory {
    private FurnitureFactory() {
        //Prevent instantiation
    }

    public static Furniture buildFurniture(FurnitureType type)
    {
        Style style = Style.MODERN;
        Furniture furniture = null;
        switch(style)
        {
            case MODERN:
                furniture = ModernFurnitureFactory.buildFurniture(type);
                break;
            case VICTORIAN:
                furniture = VictorianFurnitureFactory.buildFurniture(type);
                break;
            default:
                furniture = ArtDecoFurnitureFactory.buildFurniture(type);
        }
        return furniture;
    }

    public static Furniture buildFurniture(FurnitureType type, Style style)
    {
        Furniture furniture = null;
        switch(style)
        {
            case MODERN:
                furniture = ModernFurnitureFactory.buildFurniture(type);
                break;
            case VICTORIAN:
                furniture = VictorianFurnitureFactory.buildFurniture(type);
                break;
            default:
                furniture = ArtDecoFurnitureFactory.buildFurniture(type);
        }
        return furniture;
    }
}
```

**সুবিধা - অসুবিধা**       
১. এটা লুজ কাপলিং কোড স্ট্রাকচার।            
২. এটা সিঙ্গেল রেস্পন্সিবিলিটি প্রিন্সিপাল এবং ওপেন ক্লোজ প্রিন্সিপাল অনুযায়ী ডিজাইন করা।                     
৩. এটা একটু জটিল আকারের ডিজাইন প্যাটার্ন।                     