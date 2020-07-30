# জাভা মাল্টিথ্রেডিং বিষয়বস্তু

### ১. মাল্টিথ্রেডিং উদাহরন     
যখন একাধিক থ্রেড পাশাপাশি চলতে থাকে তখন তাকে মাল্টিথ্রেডিং বলে। 

১. এখানে থ্রেড ক্লাস এক্সটেন্ড করে মাল্টিথ্রেডিং ডিজাইন করা হয়েছে। 

```Thread 
class Runner extends Thread {
    @Override
    public void run() {
        for (int i = 0; i < 5; i++) {
            System.out.println("Hello: " + i + " Thread: " + Thread.currentThread().getName());
            try {
                Thread.sleep(100);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}

public class ApplicationExtends {
    public static void main(String[] args) {
        Runner runner1 = new Runner();
        runner1.start();

        Runner runner2 = new Runner();
        runner2.start();
    }
}
```             

২. এখানে runnable ইন্টারফেস ইমপ্লিমেন্ট করে মাল্টিথ্রেডিং ডিজাইন করা হয়েছে। 

```Runnable       
class Runner implements Runnable {
    @Override
    public void run() {
        for(int i=0; i<5; i++) {
            System.out.println("Hello: " + i + " Thread: " + Thread.currentThread().getName());
            try {
                Thread.sleep(100);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}

public class ApplicationRunnable {
    public static void main(String[] args) {
        Thread thread1 = new Thread(new Runner());
        Thread thread2 = new Thread(new Runner());
        thread1.start();
        thread2.start();
    }
}
```      

৩. এখানে ল্যামডা ফাংশন ব্যবহার করে মাল্টিথ্রেডিং ডিজাইন করা হয়েছে। 

```annonymous      
public class Application {
    public static void main(String[] args) {

        Thread thread = new Thread(new Runnable() {
            @Override
            public void run() {
                for (int i = 0; i < 5; i++) {
                    System.out.println("Hello: " + i + " Thread: " + Thread.currentThread().getName());
                    try {
                        Thread.sleep(100);
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }
                }
            }
        });

        Runnable runnerLambda = () -> {
            for (int i = 0; i < 5; i++) {
                System.out.println("Hello: " + i + " Thread: " + Thread.currentThread().getName());
                try {
                    Thread.sleep(100);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        };

        thread.start();
        new Thread(runnerLambda).start();
    }
}
```              



### ২. ভোলাটাইল কি ওয়ার্ড (volatile)      

volatile কি ওয়ার্ড ব্যবহার করা হয় অবজেক্ট আর প্রিমিটিভ টাইপের জন্য। এটা ব্যবহার করা হয় বিভিন্ন থ্রেডে variable এর মান আপডেট করার ক্ষেত্রে। ক্লাসকে থ্রেড সেফ করার জন্য ও এটি ব্যবহার করা হয়। থ্রেড সেফ বলতে বোঝায় একাধিক থ্রেড একটা ক্লাসের মেথড এবং প্যারামিটার একই সময়ে এক্সেস করতে পারে।  volatile কি ওয়ার্ডের ভ্যালু লোকাল cache এ সেভ করে না, এটা সেভ হয় সরাসরি main memory তে। যদি আমরা এমন একটা প্রোগ্রাম লিখি যেখানে দুটি থ্রেড আছে একটি থ্রেড নির্দিষ্ট ভ্যারিয়েবলের ভ্যালু read করে আর অন্যটি write করে। এখানে যদি ভ্যারিয়েবল volatile না হয় তাহলে একটি থ্রেডে write হলে অন্যটিতে read করতে পারে না। 

```volatile                
public class ReaderWriterVolatile {
    private static volatile int counter;
    public static void main(String[] args) throws InterruptedException
    {
        Thread thread1 = new Thread(() -> {
            int temp = 0;
            while (true) {
                if (temp != counter) {
                    temp = counter;
                    System.out.println("reader: value of c = " + counter);
                }
            }
        });

        Thread thread2 = new Thread(() -> {
            for (int i = 0; i < 5; i++) {
                counter++;
                System.out.println("writer: changed value to = " + counter);
                try {
                    Thread.sleep(1000);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }

            // sleep enough time to allow reader thread to read pending changes (if it can!).
            try {
                Thread.sleep(5000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            //exit the program otherwise other threads will be keep waiting on c to change.
            System.exit(0);
        });

        thread1.start();
        thread2.start();
    }
}
```              

Output with volatile keyword

```             
writer: changed value to = 1
reader: value of c = 1
writer: changed value to = 2
reader: value of c = 2
writer: changed value to = 3
reader: value of c = 3
writer: changed value to = 4
reader: value of c = 4
reader: value of c = 5
writer: changed value to = 5
```             

Output without volatile keyword

```             
writer: changed value to = 1
reader: value of c = 1
writer: changed value to = 2
writer: changed value to = 3
writer: changed value to = 4
writer: changed value to = 5
```

### ৩. সিঙ্ক্রোনাইজ (Synchronized)          

মাল্টিথ্রেডিং এর ক্ষেত্রে একাধিক থ্রেড একটি নির্দিষ্ট মেথড একই সময়ে কল করে  তখন তাকে রেস কন্ডিশন(Race Condition) বলে। এইটাকে avoid করার জন্য সিঙ্ক্রোনাইজেশন করা হয়। সিঙ্ক্রোনাইজেশন করা হলে একটি মেথডে এক সময়ে একটি থ্রেড প্রবেশ করতে পারবে এবং কাজ শেষ হলে অন্যটা প্রবেশ করবে। সিঙ্ক্রোনাইজেশন করতে হলে কোন মেথডের আগে synchronized কি ওয়ার্ড ব্যবহার করতে হয়। 

```synchronize
public class Synchronization {

    private static int count = 0;

    public static synchronized void increment(){
        count++;
    }

    public static void main(String[] args) {

        Thread thread1 = new Thread(new Runnable() {
            public void run() {
                for (int i = 0; i < 10000; i++) {
                    increment();
                }
            }
        });
        thread1.start();

        Thread thread2 = new Thread(new Runnable() {
            public void run() {
                for (int i = 0; i < 10000; i++) {
                    increment();
                }
            }
        });
        thread2.start();

        try {
            thread1.join();
            thread2.join();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        System.out.println("Count is: " + count);
    }
}
```

### ৪. লক অবজেক্ট (Lock Objects)          
সিঙ্ক্রোনাইজেশনের জন্য লক অবজেক্ট প্রয়োজন হয়। যখন আমরা কোন একটা নির্দিষ্ট লাইন কোড সিঙ্ক্রোনাইজএশন করতে চাই তখন লক অবজেক্ট অবজেক্ট তৈরি করে আমরা কাজটা করি। যখন থ্রেড একটা লক অবজেক্ট পাবে তখন ওই লকের অন্তর্ভুক্ত কোড এক্সিকিউট করবে তারপর ওই লক অবজেক্ট রিলিজ হয়ে গেলে অন্য একটা লক অবজেক্টের কোড এক্সিকিউট হবে। এই লক অবজেক্ট অটোমেটিক ভাবে jvm রিলিজ করে দেয়।                        

```Lock
public class ObjectLock {
    private Random random = new Random();

    private Object lock1 = new Object();
    private Object lock2 = new Object();

    private List<Integer> list1 = new ArrayList<Integer>();
    private List<Integer> list2 = new ArrayList<Integer>();

    public void stageOne() {

        synchronized (lock1) {
            try {
                Thread.sleep(1);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }

            list1.add(random.nextInt(100));
        }

    }

    public void stageTwo() {

        synchronized (lock2) {
            try {
                Thread.sleep(1);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }

            list2.add(random.nextInt(100));
        }

    }

    public void process() {
        for (int i = 0; i < 1000; i++) {
            stageOne();
            stageTwo();
        }
    }

    public void run() {
        System.out.println("Starting ...");

        long start = System.currentTimeMillis();

        Thread t1 = new Thread(new Runnable() {
            public void run() {
                process();
            }
        });

        Thread t2 = new Thread(new Runnable() {
            public void run() {
                process();
            }
        });

        t1.start();
        t2.start();

        try {
            t1.join();
            t2.join();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        long end = System.currentTimeMillis();

        System.out.println("Time taken: " + (end - start));
        System.out.println("List1: " + list1.size() + "; List2: " + list2.size());
    }

    public static void main(String[] args) {
        ObjectLock objectLock = new ObjectLock();
        objectLock.run();
    }
}
```

### ৫. থ্রেড পুল (Thread Pools)       
যখন আমাদের একাধিক থ্রেড প্রয়োজন হয় তখন আমরা একটার পর একটা থ্রেড তৈরি করি। কিন্তু এভাবে আমরা একের পর এক থ্রেড তৈরি করতে থাকি তাহলে প্রোগ্রাম ধীরগতির হওয়ার সম্ভাবনা আছে। সুতরাং এই অবস্থায় আমাদের নির্দিষ্ট সংখ্যক থ্রেড তৈরি করবো এবং একটা থ্রেড ফ্রি হলে তাকে আবার ব্যবহার করবো। এর ফলে আমাদের থ্রেডের পারফরমেন্স ভাল হয়। থ্রেড পুল এই কাজটি করে থাকে।  এই জন্য আমাদের ExecutorService ইন্টারফেস ব্যবহার করতে হবে যা java.util.concurrent প্যাকেজের অন্তর্ভুক্ত। 

```ThreadPool
class Processor implements Runnable {

    private int id;

    public Processor(int id) {
        this.id = id;
    }

    public void run() {
        System.out.println("Starting: " + id);

        try {
            Thread.sleep(5000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        System.out.println("Completed: " + id);
    }
}

public class ThreadPool {

    public static void main(String[] args) {

        ExecutorService executor = Executors.newFixedThreadPool(2);

        for(int i=0; i<5; i++) {
            executor.submit(new Processor(i));
        }

        executor.shutdown();

        System.out.println("All tasks submitted.");

        try {
            executor.awaitTermination(1, TimeUnit.DAYS);
        } catch (InterruptedException e) {
        }

        System.out.println("All tasks completed.");
    }
}
```

### ৬. কাউন্টডাউন ল্যাচেস (Countdown Latches)    
কখনো কখনো আমাদের কোন একটা প্রোগ্রাম রান করার প্রয়োজন হয় যখন আমাদের নির্দিষ্ট কিছু টাস্ক অথবা প্রোগ্রাম শেষ হবার পর। ধরে নেই আমরা একটা সাইকেল বানানোর প্রোগ্রাম রান করাতে চাই। তো এখন সাইকেলে চেইন, গিয়ার, সিট, প্যাডেল এই গুলোকে ও যদি ছোট ছোট প্রোগ্রাম হিসেবে কল্পনা করি তাহলে এই প্রোগ্রাম শেষ হবার পরই একমাত্র আমরা সাইকেলের প্রোগ্রাম রান করাতে পারবো। এই ক্ষেত্রে আমরা কিভাবে বুঝবো ছোট ছোট প্রোগ্রাম গুলো সব এক্সিকিউট হয়ে গিয়েছে। এই কাজটার জন্য কাউন্টডাউন ল্যাচেস ব্যবহার করা যায়।  আমরা যদি ৫ টা থ্রেড তৈরি করি এবং এমনটা করতে চাই যে ৫ টা থ্রেড সম্পূর্ণ হওয়ার পর মেইন থ্রেড এক্সিকিউট হবে। তাহলে আমাদের CountDownLatch এর অবজেক্ট তৈরি করতে হবে এবং প্যারামিটার হিসেবে যাবে ৫। CountDownLatch এর countDown() মেথড আছে যেটা এটার ভ্যালু ৫ থেকে শুন্য পর্যন্ত আপডেট হতে থাকে। প্রতিটা থ্রেড শেষ হয় এবং এর ভ্যালু এক করতে কমতে থাকে। সব গুলো শেষ হলে মেইন থ্রেড এক্সিকিউট হয়। await() মেথড হচ্ছে ব্লকিং মেথড যেটা সবগুলো থ্রেড শেষ না হওয়া পর্যন্ত ব্লক করে রাখে। সব গুলো এক্সিকিউট হওয়ার পর এটি পরের স্টেপ যেতে দেয়।                                 

```countdownlatches
public class CountDownLatchDemo {
    private static final CountDownLatch COUNT_DOWN_LATCH = new CountDownLatch(5);
    public static void main(String[] args) {
        Thread run1 = new Thread(() -> {
            System.out.println("Doing some work..");
            try {
                Thread.sleep(2000);
                COUNT_DOWN_LATCH.countDown();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        });
        Thread run2 = new Thread(() -> {
            System.out.println("Doing some work..");
            try {
                Thread.sleep(2000);
                COUNT_DOWN_LATCH.countDown();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        });
        Thread run3 = new Thread(() -> {
            System.out.println("Doing some work..");
            try {
                Thread.sleep(2000);
                COUNT_DOWN_LATCH.countDown();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        });
        Thread run4 = new Thread(() -> {
            System.out.println("Doing some work..");
            try {
                Thread.sleep(2000);
                COUNT_DOWN_LATCH.countDown();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        });
        Thread run5 = new Thread(() -> {
            System.out.println("Doing some work..");
            try {
                Thread.sleep(3000);
                COUNT_DOWN_LATCH.countDown();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        });
        run1.start();
        run2.start();
        run3.start();
        run4.start();
        run5.start();
        try {
            COUNT_DOWN_LATCH.await();
        } catch (InterruptedException e) {
            //Handle when a thread gets interrupted.
        }
        System.out.println("All tasks have finished..");
    }
}
```

### ৭. ব্লকিংকিউ (BlockingQueue)               
BlockingQueue হচ্ছে java.util.concurrent প্যাকেজের একটা ইন্টারফেস। এটা এমন ধরনের কিউ যেটা থ্রেড সেফ। যখন কোন থ্রেড এই কিউ খালি অবস্থায় dequeue করতে চায় তখন এটাকে ব্লক করে রাখে যতক্ষণ পর্যন্ত অন্য থ্রেড ভ্যালু enqueue না করে অথবা কিউ পূর্ণ অবস্থায় enqueue করতে চায় তখন এটাকে ব্লক করে রাখে যতক্ষণ পর্যন্ত অন্য থ্রেড ভ্যালু dequeue না করে। এটা ব্যবহার করে আমরা producer-consumer সিস্টেম ডিজাইন করতে পারি। producer কোন কিছু produce করবে সেটা আবার consumer সেটা consume করবে। কিউ ফাঁকা থাকলে consumer অপেক্ষা করবে অর্থাৎ ব্লক করে রাখা হবে আর কিউ পূর্ণ থাকলে producer ব্লক থাকবে। 

```blockingqueue
public class ProducerConsumer {
    private static BlockingQueue<Integer> queue = new ArrayBlockingQueue<Integer>(10);

    public static void main(String[] args) throws InterruptedException {
        Thread t1 = new Thread(new Runnable() {
            public void run() {
                try {
                    producer();
                } catch (InterruptedException e) {
                    // TODO Auto-generated catch block
                    e.printStackTrace();
                }
            }
        });

        Thread t2 = new Thread(new Runnable() {
            public void run() {
                try {
                    consumer();
                } catch (InterruptedException e) {
                    // TODO Auto-generated catch block
                    e.printStackTrace();
                }
            }
        });

        t1.start();
        t2.start();

        t1.join();
        t2.join();
    }

    private static void producer() throws InterruptedException {
        Random random = new Random();

        while(true) {
            queue.put(random.nextInt(100));
        }
    }

    private static void consumer() throws InterruptedException {
        Random random = new Random();

        while(true) {
            Thread.sleep(100);

            if(random.nextInt(10) == 0) {
                Integer value = queue.take();

                System.out.println("Taken value: " + value + "; Queue size is: " + queue.size());
            }
        }
    }
}
```

### ৮. ওয়েট - নোটিফাই (Wait and Notify)               
**wait()**       
wait() মেথড  কোন থ্রেডের ভেতর কল করলে সেই থ্রেড sleep() হয়ে যায়। এবং অন্য থ্রেড যখন notify() বা notifyAll() কল করে তখন পূর্বের থ্রেড আবার শুরু করে।              

**notify()**          
notify() মেথড কল করা হয় কোন থ্রেড কে চালু করার জন্য যেটা wait() মেথড কল করে sleep() করে দেওয়া হয়েছে। 

**notifyAll()**       
notifyAll() মেথড কল করা হয় কোন থ্রেড কে চালু করার জন্য যেটা wait() মেথড কল করে sleep() করে দেওয়া হয়েছে। notifyAll() সকল থ্রেড কে সক্রিয় করে যেগুলো wait() মেথড দ্বারা থামিয়ে দেওয়া হয়েছিল। 

```waitnotify
public class WaitNotify {
    public static void main(String[] args) throws InterruptedException {

        WaitNotify waitNotify = new WaitNotify();

        Thread t1 = new Thread(new Runnable() {
            @Override
            public void run() {
                try {
                    waitNotify.produce();
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        });

        Thread t2 = new Thread(new Runnable() {
            @Override
            public void run() {
                try {
                    waitNotify.consume();
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        });

        t1.start();
        t2.start();

        t1.join();
        t2.join();
    }

    public void produce() throws InterruptedException {
        synchronized (this) {
            System.out.println("Producer thread running ....");
            wait();
            System.out.println("Resumed.");
        }
    }

    public void consume() throws InterruptedException {
        Scanner scanner = new Scanner(System.in);
        Thread.sleep(2000);
        synchronized (this) {
            System.out.println("Waiting for return key.");
            scanner.nextLine();
            System.out.println("Return key pressed.");
            notify();
            Thread.sleep(5000);
        }
    }
}
```    

### ৯. Re-entrant Locks                  
ReentrentLock ক্লাস Lock ইন্টারফেস কে impliment করে। এইটার কাজ কিছুটা সিঙ্ক্রোনাইজেশনের মত। কোন মেথড কে সিঙ্ক্রোনাইজ না করেই ReentrentLock ব্যবহার করে একই ধরনের কাজ করা যায়। অর্থাৎ এটি ব্যবহার করে নির্দিষ্ট ব্লকে শুধুমাত্র একই সময়ে একটি থ্রেড প্রবেশ করবে এমন ব্যবস্থা করা যায়।  lock() মেথড লক করে নির্দিষ্ট অংশ এক্সিকিউট করে আর unlock() মেথড লক টা রিলিজ করে দেয় যাতে অন্য মেথড প্রবেশ করতে পারে।                                   

```reentrentLock
public class ReentrantLockExample {

    private ReentrantLock lock = new ReentrantLock(true);

    private int counter = 0;

    void perform() {

        lock.lock();
        System.out.println("Thread - " + Thread.currentThread().getName() + " acquired the lock");
        try {
            System.out.println("Thread - " + Thread.currentThread().getName() + " processing");
            counter++;
        } catch (Exception exception) {
            exception.printStackTrace();
        } finally {
            lock.unlock();
            System.out.println("Thread - " + Thread.currentThread().getName() + " released the lock");
        }
    }

    private void performTryLock() {

        System.out.println("Thread - " + Thread.currentThread().getName() + " attempting to acquire the lock");
        try {
            boolean isLockAcquired = lock.tryLock(2, TimeUnit.SECONDS);
            if (isLockAcquired) {
                try {
                    System.out.println("Thread - " + Thread.currentThread().getName() + " acquired the lock");

                    System.out.println("Thread - " + Thread.currentThread().getName() + " processing");
                    sleep(1000);
                } finally {
                    lock.unlock();
                    System.out.println("Thread - " + Thread.currentThread().getName() + " released the lock");

                }
            }
        } catch (InterruptedException exception) {
            exception.printStackTrace();
        }
        System.out.println("Thread - " + Thread.currentThread().getName() + " could not acquire the lock");
    }

    public ReentrantLock getLock() {
        return lock;
    }

    boolean isLocked() {
        return lock.isLocked();
    }

    boolean hasQueuedThreads() {
        return lock.hasQueuedThreads();
    }

    int getCounter() {
        return counter;
    }

    public static void main(String[] args) {

        final int threadCount = 2;
        final ExecutorService service = Executors.newFixedThreadPool(threadCount);
        final ReentrantLockExample object = new ReentrantLockExample();

        service.execute(object::perform);
        service.execute(object::performTryLock);

        service.shutdown();

    }
}
```

### ১১. ডেডলক (Deadlock)                    
ডেডলক (Deadlock) হল মাল্টিথ্রেডিং এর একটি গুরুত্বপূর্ণ বিষয়। যখন একটা থ্রেড কোন লক অবজেক্টের অপেক্ষায় থাকে অর্থাৎ উক্ত লক অবজেক্টটি মুক্ত হলে সে এক্সিকিউট হবে কিন্তু লক অবজেক্টটা আছে ২য় একটা থ্রেডের কাছে। আবার ২য় থ্রেডটি অপেক্ষা করে প্রথম থ্রেডের কাছে থাকা লক অবজেক্টের অপেক্ষায়। এই অবস্থায় দুটি থ্রেডই থেমে থাকে আর চলতে পারে না, এটাই হল ডেডলক।                                                                 

```
public class Account {
    private int balance = 10000;
    public void deposit(int amount) {
        balance += amount;
    }
    public void withdraw(int amount) {
        balance -= amount;
    }
    public int getBalance() {
        return balance;
    }
    public static void transfer(Account acc1, Account acc2, int amount) {
        acc1.withdraw(amount);
        acc2.deposit(amount);
    }
}
```

```
public class Runner {
    private Account acc1 = new Account();
    private Account acc2 = new Account();

    private Lock lock1 = new ReentrantLock();
    private Lock lock2 = new ReentrantLock();

    private void acquireLocks(Lock firstLock, Lock secondLock) throws InterruptedException {
        while(true) {
            boolean gotFirstLock = false;
            boolean gotSecondLock = false;

            try {
                gotFirstLock = firstLock.tryLock();
                gotSecondLock = secondLock.tryLock();
            }
            finally {
                if(gotFirstLock && gotSecondLock) {
                    return;
                }
                if(gotFirstLock) {
                    firstLock.unlock();
                }
                if(gotSecondLock) {
                    secondLock.unlock();
                }
            }
            Thread.sleep(1);
        }
    }

    public void firstThread() throws InterruptedException {
        Random random = new Random();
        for (int i = 0; i < 10000; i++) {
            acquireLocks(lock1, lock2);
            try {
                Account.transfer(acc1, acc2, random.nextInt(100));
            } finally {
                lock1.unlock();
                lock2.unlock();
            }
        }
    }

    public void secondThread() throws InterruptedException {
        Random random = new Random();
        for (int i = 0; i < 10000; i++) {
            acquireLocks(lock2, lock1);
            try {
                Account.transfer(acc2, acc1, random.nextInt(100));
            } finally {
                lock1.unlock();
                lock2.unlock();
            }
        }
    }

    public void finished() {
        System.out.println("Account 1 balance: " + acc1.getBalance());
        System.out.println("Account 2 balance: " + acc2.getBalance());
        System.out.println("Total balance: " + (acc1.getBalance() + acc2.getBalance()));
    }
}
```

```
public class DeadLock {
    public static void main(String[] args) throws Exception {

        final Runner runner = new Runner();

        Thread t1 = new Thread(new Runnable() {
            public void run() {
                try {
                    runner.firstThread();
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        });

        Thread t2 = new Thread(new Runnable() {
            public void run() {
                try {
                    runner.secondThread();
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        });
        t1.start();
        t2.start();
        t1.join();
        t2.join();
        runner.finished();
    }
}
```

### ১২. সেমাফোর (Semaphores)                    
যখন একটা কমন প্রোগ্রাম থাকে যেটাতে বিভিন্ন থ্রেডের প্রবেশ করতে হয়। তবে সব গুলো থ্রেড একবারে না একটা একটা করে অথবা নির্দিষ্ট সংখ্যক করে। সেমাফোর এই থ্রেডের এই অ্যাক্সেস নিয়ন্ত্রন করে। এটা নির্দিষ্ট করে দেয় সর্বোচ্চ কতটা থ্রেড ওই নির্দিষ্ট ব্লকে প্রবেশ করতে পারবে।    

```
public class Connection {
    private static Connection instance = new Connection();

    private Semaphore sem = new Semaphore(10, true);

    private int connections = 0;

    private Connection() {

    }

    public static Connection getInstance() {
        return instance;
    }

    public void connect() {
        try {
            sem.acquire();
        } catch (InterruptedException e1) {
            e1.printStackTrace();
        }

        try {
            doConnect();
        } finally {
            sem.release();
        }
    }

    public void doConnect() {

        synchronized (this) {
            connections++;
            System.out.println("Current connections: " + connections);
        }

        try {
            Thread.sleep(2000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        synchronized (this) {
            connections--;
        }

    }
}
```

```
public class SemaphoreExample {
    public static void main(String[] args) throws Exception {

        ExecutorService executor = Executors.newCachedThreadPool();

        for(int i=0; i < 200; i++) {
            executor.submit(new Runnable() {
                public void run() {
                    Connection.getInstance().connect();
                }
            });
        }

        executor.shutdown();

        executor.awaitTermination(1, TimeUnit.DAYS);
    }
}
```

### ১৩. কলএবল ও ফিউচার (Callable and Future)                              
থ্রেড ইমপ্লিমেন্ট করা যায় ২ টি উপায়ে Thread ক্লাস ও Runnable ইন্টারফেস ব্যবহার করে। কিন্তু এইভাবে থ্রেড তৈরি করলে এরা কোন ভ্যালু রিটার্ন করে না। Callable ইন্টারফেস ইমপ্লিমেন্ট করলে সেটাতে আমরা ভ্যালু রিটার্ন করতে পারি। এর call() মেথডকে ইমপ্লিমেন্ট করতে হয় এবং এর অবজেক্ট সেভ করে রাখা হয় Future ক্লাসের অবজেক্ট তৈরি করে।                                          

```
public class CallableAndFuture {
    public static void main(String[] args) {
        ExecutorService executor = Executors.newCachedThreadPool();

        Future<Integer> future = executor.submit(new Callable<Integer>() {

            @Override
            public Integer call() throws Exception {
                Random random = new Random();
                int duration = random.nextInt(4000);

                if(duration > 2000) {
                    throw new IOException("Sleeping for too long.");
                }

                System.out.println("Starting ...");

                try {
                    Thread.sleep(duration);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }

                System.out.println("Finished.");

                return duration;
            }

        });

        executor.shutdown();

        try {
            System.out.println("Result is: " + future.get());
        } catch (InterruptedException e) {
            e.printStackTrace();
        } catch (ExecutionException e) {
            IOException ex = (IOException) e.getCause();
            System.out.println(ex.getMessage());
        }
    }
}
```

### ১৪. Interrupting Threads
