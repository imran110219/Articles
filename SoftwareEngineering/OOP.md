# অবজেক্ট ওরিয়েন্টেড প্রোগ্রামিং

অবজেক্ট ওরিয়েন্টেড প্রোগ্রামিং বলতে বোঝায় আমি আমার ডাটা গুলোকে অবজেক্ট হিসেবে তৈরী করবো এবং প্রয়োজন অনুসারে ব্যবহার করবো।  ধরা যাক, আমি একটা বাইসাইকেল কোম্পানি দিতে চাই। একটা বাইসাইকেলে অনেক গুলো যন্ত্রাংশ জোড়া লাগালেই একটা 
পূর্ণ বাইসাইকেল তৈরী হয়। এজন্য আমাকে চাকা, সিট, ব্রেক সব কিছু আলাদা ভাবে তৈরী করে এনে তারপর জোড়া লাগাতে হবে। এখন আমি যদি ১০০ চাকা বানাতে চাই, তাহলে প্রথমে আমাকে চাকার বৈশিষ্ট ঠিক করে হবে যেমন চাকাটা কেমন ভারী হবে, স্পোক কতগুলো থাকবে, ব্যাস কতটুকু হবে।
চাকার এই সমস্ত বৈশিষ্ট ঠিক হলেই সেটা বানানো শুরু করা যাবে তার আগে নয়। চাকার এই বৈশিষ্ট গুলোর সমন্বয়কেই বলা হয় ক্লাস। আর ওই যে ১০০ টা চাকা বানাবো ওই গুলো হল অবজেক্ট। স্বাভাবিক ভাবেই ভাবুন মানুষ হল একটা ক্লাস আর মানুষের বৈশিষ্ট হল সে খায়, ঘুমায়। আর দুনিয়াতে রহিম, করিম যত মানুষ
আছে সবাই এক একটা অবজেক্ট। 

## আলোচনার বিষয়ঃ
* এনক্যাপসুলেশান
* ইনহেরিট্যান্স
* পলিমরফিজম
* অ্যাবস্ট্রাকশান


### এনক্যাপসুলেশান (Enacapsulation)
Enacapsulation এর অর্থ হল সংক্ষেপ বা পরিবেস্টন করে রাখা। যখন আমরা নির্দিষ্ট কোন ক্লাসের ডাটাকে private রাখা, getters ব্যবহার  করে ডাটা পড়া এবং setters ব্যবহার করে ডাটা সেভ করাটাই মুলত এনক্যাপসুলেশান। কোন ক্লাসে আমরা যদি ডাটা public করে রাখি 
তাহলে ওইটা অন্য যে কোন ক্লাস থেকে তার ভ্যালু ইচ্ছা মত পরিবর্তন করা যায়। এইটা রোধ করার জন্য আমরা তখন variable কে private করে রাখি। কিন্তু আমাদের যখন বাইরে থেকে value কে read এবং write করার দরকার হয় তখন আমরা getters এবং setters ব্যবহার করি।
ধরুন, জাতীয় পরিচয় পত্রে নাগরিকের বয়স হালনাগাদ বা যোগ করতে হবে আর যখন দরকার হবে তখন একটা মেথড কল করলে বয়সটা দেখতে পারা যাবে। কিন্তু এখানে একটা বিষয় মাথায় রাখতে হবে ১৮ বছরের কম বয়স দেওয়া যাবে না। তাহলে কোডটা এমন হবে

```Enacapsulation
public int getAge() {
	return age;
}

public void setAge(int age) {
	if(age>=18)
		this.age = age;
}
```

### ইনহেরিট্যান্স (Inheritance)
Inheritance এর অর্থ হল উত্তরাধিকার। সহজ কথায় আপনার বাবার সম্পত্তি যেমন উত্তরাধিকার সুত্রে আপনি পান, ঠিক একই ভাবে জাভা তে কোন class যদি অন্য একটা class কে extend করে তাহলে তাদের ভেতরে child-parent সম্পর্ক হয়ে যায়। ধরুন, Parent নামে
আমার একটা ক্লাস আছে তার ভেতরে কিছু variable এবং method আছে। তারপর একটা ক্লাস তৈরী করলাম Child নামে এবং Parent কে extend করলাম। তাহলে Parent এর সব variable এবং method গুলো Child পাবে। 

```Inheritance
public class Parent {
    private int age;

    public void eating() {
        System.out.println(getClass().getSimpleName() + " is eating.");
    }
}

public class Child extends Parent {

}
```

### পলিমরফিজম (Polymorphism)
Polymorphism অর্থ হল বহুরূপতা। সহজভাবে বলতে গেলে একটা জিনিসের বহুমুখী ব্যবহার থাকে সেটাই হল পলিমরফিজম। উদাহরনস্বরূপ - মোবাইল আমরা কথা বলা, ইন্টারনেট ব্যবহার, সময় দেখা বিভিন্ন কাজে ব্যবহার করি। পলিমরফিজম সাধারণত দুই প্রকারঃ
* Compile time Polymorphism / Overloading
* Runtime Polymorphism / Overriding

	#### Compile time Polymorphism / Overloading
	এটা বলতে বোঝায় যে পলিমরফিজম প্রোগ্রাম কম্পাইল হওয়ার সময় গঠিত হয় সেটাকেই আমরা compile time polymorphism বলি। Overloading হল তেমন একটা বিষয়। যখন একই নামে একাধিক মেথড একই ক্লাসে অবস্থান করে কিন্তু তাদের প্যারামিটার টাইপ অথবা সংখ্যা ভিন্ন হয় তখন সেটা হয় method overloading. ধরুন, আমার কাছে একটা ছুরি আছে সেই ছুরি আমি সবজি, কাগজ অথবা কাপড় কাটার কাজে ব্যবহার করতে পারি। যখন্ একই নামের method বিভিন্ন কাজ করে সেটাই হল Overloading.
		  
	```Overloading
	public void cutting(String things){
		System.out.println("Knife cuts " + things);
	}

	// Method Overloading By changing the data type
	public void cutting(int cuttingLength){
		System.out.println("Knife cuts " + cuttingLength + " centimeter");
	}
	// Method Overloading By changing number of arguments
	public void cutting(String things, int cuttingLength){
		System.out.println("Knife cuts " + things + " with " + cuttingLength + " centimeter");
	}

	```
		  
	#### Runtime Polymorphism / Overriding
	এটা বলতে বোঝায় যে পলিমরফিজম প্রোগ্রাম রান হওয়ার সময় গঠিত হয় সেটাকেই আমরা runtime polymorphism বলি। Overriding হল তেমন একটা বিষয়। যখন একই মেথড Parent ক্লাসে অবস্থান করে আবার Child ক্লাসে অবস্থান করে তখন সেটা হয় method overloading. উদাহরনসবরুপঃ আমি উত্তরাধিকারসুত্রে বাবার কাছ থেকে একটা পুরানো গাড়ি পেলাম এখন বাবার গাড়িটা পুরানো বলে আমি চালাতে সমস্যা হচ্ছে। এই অবস্থায় আমার উচিত হল গাড়িটিকে একটু আপডেট করা যেমন ইঞ্জিন পরিবর্তন, রং করা ইত্যাদি। এইটাই হল Overriding.
		 
	```Overriding
	class Parent {

		public void walking(){
			System.out.println("Parent is walking.");
		}
	}
	 
	class Child extends Parent {
	 
		// Method Overriding
		public void walking(){
			System.out.println("Child is walking.");
		}
	}
	```
	
### অ্যাবস্ট্রাকশান (Abstraction)	
Abstraction দরকার হয় যখন আমরা কোন মেথডের পুরা কোড লুকিয়ে রাখি আর শুধু মেথড ডিক্লেয়ার করে ওইটাই দেখাই। ধরা যাক, আমরা ইমেইল ব্যবহার করি কিন্তু শুধু ইমেইল আইডি আর মেসেজ লিখে ইমেইল সেন্ড করে দেই। কিন্তু ইমেইল সার্ভিসটা কিভাবে কাজ করে সেটা আমরা জানিনা অথবা সেই প্রসেসটা আমাদের দেখানো হয় না।
Abstract ক্লাস/মেথড abstract keyword ব্যবহার করে ডিক্লেয়ার করা হয়। পরে অন্য কোন ক্লাস তার প্রয়োজন অনুযায়ী extend করে নেয়। 

অ্যাবস্ট্রাকশান দুই ভাবে হয়ে থাকেঃ
* Abstract class
* Interface 

	#### Abstract class
	Abstract class অথবা method তৈরী করতে গেলে abstract keyword ব্যবহার করে করা যায়। Abstract class এর ভেতরে method abstract অথবা non abstract ও হতে পারে। Abstract ক্লাসের object তৈরী করা যায় না। অন্য ক্লাস Abstract ক্লাসকে extend করে  তার সুবিধা মত method implement করে নেয়। Child class কে অবশ্যই  abstract method কে implement করতে হবে না হলে error দিবে।
	
	```Abstract
	abstract class Shape {
		abstract double area();
    
		public String getColor() {
			return color;
		}
	}
	 
	class Circle extends Shape {

		@Override
		double area() {
			return Math.PI * Math.pow(radius, 2);
		}
	}
	```
	
	#### Interface
	Interface হল পুরোপুরি abstract করার একটা উপায়। একটা Interface এ শুধু abstract method এ থাকতে পারে। অন্য কোন ক্লাস Interface কে implement করে । 
	
	```Interface
	public interface Animal {
		public void getName();
	}
	 
	class Human implements Animal{

		@Override
		public void getName() {
			System.out.println("Human");
		}
	}
	```