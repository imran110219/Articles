# Java Thread

### Java Thread কি?
থ্রেড হল একটা প্রক্রিয়া যা সহজে execute হয়। জাভার নিজস্ব support আছে multithreading programming এর জন্য। multithreading program একই সাথে দুই বা ততোধিক process চালাতে পারে। সহজভাবে যদি বলি আপনি যদি 
একই সাথে গান শোনা এবং বই পড়া চালিয়ে যাচ্ছেন বিষয় টা অনেকটা সেই রকম। 

### Java Thread Lifecycle (জীবনচক্র)
জাভাতে Thread এর একটি নির্দিষ্ট জীবন চক্র আছে। Thread এর জীবন চক্র ৫ টা ধাপে সম্পন্ন হয়ে থাকে।
1. **New** : যখন কোন Thread তৈরী করা হয় তখন্ এই পর্যায়ে থাকে। 
2. **Runnable** : Thread যখন run() হওয়ার জন্য প্রস্তুত থাকে।
3. **Running** : এইটা হল Thread এর চলমান অবস্থা।
4. **Non-Runnable (Blocked)** : যখন Thread কে চলমান অবস্থায় থামিয়ে দেওয়া হয়।
5. **Terminated** : এইটা হল যখন ফাইনালি Thread কে বন্ধ করে দেওয়া হয়।

### Java Thread built in methods
জাভাতে কিছু নিজস্ব method আছে যে গুলো Thread এর implementation এর জন্য ব্যবহার করা যায়ঃ

* **getName** Thread এর নাম return করে
* **getPriority** Thread এর priority return করে
* **isAlive** Thread চলমান আছে কিনা যাচাই করে
* **join** Thread এর শেষ হওইয়া পর্যন্ত অপেক্ষা করে
* **run** Thread শুরু হওয়ার মেথড
* **sleep**	Thread একটি নির্দিষ্ট সময় পর্যন্ত বন্ধ থাকে
* **start**	Thread শুরু হয় এই মেথড কল করলে

### Java Thread তৈরির উপায়
Thread মুলত দুইভাবে তৈরী করা যায়ঃ
* Runnable Interface কে  implement করে
* Thread class কে extend করে 

### Runnable Interface
1. প্রথমে একটা ক্লাস বানাতে হবে যেটা Runnable Interface এর run() মেথড কে implement করবে। 

```Runnable Interface
class RunnableImpl implements Runnable { 

	public void run() 
	{ 
		System.out.println("run"); 
	} 
} 
```

2. এরপর Thread এর একটা object তৈরী করতে হবে এবং RunnableImpl class কে constructor এ pass করতে হবে।

```Runnable Interface Thread Object
Thread thread = new Thread(new RunnableImpl());
```

3. তারপর আমাদেরকে thread object টা চালাতে হবে start() মেথড কল করে।

```Start Thread
thread.start(); 
```
	
### Thread Class
1. প্রথমে একটা ক্লাস বানাতে হবে যেটা Thread class কে extend করবে। 

```Thread Class
class ThreadImpl extends Thread { 

	public void run() 
	{ 
		System.out.println("run"); 
	} 
} 
```

2. এরপর Thread এর একটা object তৈরী করতে হবে।

```Thread Object
ThreadImpl thread = new ThreadImpl();
```

3. তারপর আমাদেরকে thread object টা চালাতে হবে start() মেথড কল করে।

```Start Thread
thread.start(); 
```

### Creating Multiple Thread 
একটি প্রোগ্রামের ভিতর আমরা যখন একাধিক থ্রেড তৈরী করে রান করি তখন সেটা হয় multithreading.

```Multithreading
public class MultiThreading extends Thread{
    public void run(){
        System.out.println(Thread.currentThread().getName() + " is running...");
    }
    public static void main(String args[]){
        MultiThreading t1=new MultiThreading();
        MultiThreading t2=new MultiThreading();
        MultiThreading t3=new MultiThreading();
        t1.start();
        t2.start();
        t3.start();
    }
}
```

[জাভা মাল্টিথ্রেডিং](Multithreading.md)  