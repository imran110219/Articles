# জাভা লগিং                

**লগিং কি?**               
লগিং হল এমন একটি প্রক্রিয়া যখন কোন প্রোগ্রাম এক্সিকিউট হয় তখন নির্দিষ্ট একটা লগ ফাইলে লগ ম্যাসেজ গুলো লেখা হয়। লগিং এর ভেতরে report, error, warning এবং message লেখা হয় যে গুলো পরবর্তীতে অ্যানালাইসিস করে অ্যাপ্লিকেশনের অবস্থা সম্পর্কে বোঝা যায়। যে অবজেক্ট অ্যাপ্লিকেশন লগিং অপারেশন করে থাকে সেটাকে লগার বলা হয়ে থাকে।              

**কেন দরকার লগিং**                                  
জাভা অ্যাপ্লিকেশনে কোন ম্যাসেজ যদি ডেভোলপারের দেখার প্রয়োজন হয় তখন সাধারণভাবে System.out.println() দিয়ে console এ দেখতে পারে। কিন্তু এটা তো কোথাও সেভ হয়ে থাকে না। পরবর্তীতে কোন আলোচনা অথবা অ্যানালাইসিসের এই রিপোর্ট দরকার হয়।                    

**লগিং কম্পোনেন্ট**    
* Loggers কম্পোনেন্ট লগ রেকর্ড গুলোকে কালেক্ট করে এবং নির্দিষ্ট Appenders এ পৌঁছে দেয়।                          
* Appenders/Handlers কাজ হলো লগ ইভেন্ট destination এ রেকর্ড করে রাখা। লগ রেকর্ড আউটপুটে পৌঁছানোর আগে Formatters সেগুলোকে নির্দিষ্ট ফরম্যাটে নিয়ে আসে।                  
* Layouts/Formatters লগ ডেটার দেখতে কেমন হবে অর্থাৎ আউটলুক কেমন হবে সেটা ঠিক করে দেয়।             

**লগিং ফ্রেমওয়ার্ক**                 
* java.util.logging
* [Log4j](Log4j.md)
* [Logback](Logback.md)
* tinylog
* Logbook   

**java.util.logging**   
java.util.logging হল জাভার নিজস্ব প্যাকেজ। এই প্যাকেজের ভেতর কিছু ক্লাস এবং ইন্টারফেস আছে যেগুলো লগিং এর জন্য ব্যবহৃত হয়ে থাকে। নিচে এর বিস্তারিত বর্ণনা করা হলঃ              

**Logger**              
লগিং অপারেশন করার জন্য প্রথমেই লগার অবজেক্ট তৈরি করা হয়। এইটা java.util.logging.Logger প্যাকেজের অন্তর্ভুক্ত।       
```
import java.util.logging.Logger;

// assumes the current class is called LoggerExample
private final static Logger LOGGER = Logger.getLogger(LoggerExample.class.getName());
```

**Level**            
লগ লেভেল মেসেজের ধরন এবং গুরুত্ব নির্দেশ করে। লেভেল ক্লাস ঠিক করে দেয় কোন ধরনের মেসেজ লগের ভেতরে লেখা হবে। লগ লেভেল লিস্টগুলো হলঃ                          
* SEVERE (highest)
* WARNING
* INFO
* CONFIG
* FINE
* FINER
* FINEST                     
আরো দুইটা লগ লেভেল আছে সেগুলো হল OFF এবং ALL. OFF হলে লগ বন্ধ থাকবে আর ALL হলে সবকিছু লগ করে রাখবে।                
```
LOGGER.setLevel(Level.INFO);
```

**Handler**  
Handler হল জাভা লগিং ফ্রেমওয়ার্কের একটি কম্পোনেন্ট। লগ মেসেজ কোন নির্দিষ্ট জায়গায় রেখে দেয় এই কম্পোনেন্ট। লগ কনসোলে ও রাখা যায় আবার চাইলে কোন ফাইলে ও রাখা যায়। Handler একটি নির্দিষ্ট ফরম্যাটে ডাটা লগ রেকর্ডে ডাটা রাখে এবং টার্গেট ডেস্টিনেশনে পাঠিয়ে দেয়। java.util.logging প্যাকেজে সর্বমোট কয়েক ধরনের Handler আছে। সেগুলো হলঃ                     
* ConsoleHandler: এটি System.err এ লগ মেসেজ রেকর্ড করে রাখে। এটা লগারের ডিফল্ট হ্যান্ডলার।                  
* FileHandler: এটি কোন নির্দিষ্ট ফাইলে লগ মেসেজ রেকর্ড করে রাখে।
* StreamHandler: এটি OutputStream এ লগ মেসেজ পাবলিশ করে থাকে।
SocketHandler: এটি নেটওয়ার্ক stream connection এ লগ মেসেজ পাবলিশ করে থাকে।
MemoryHandler: এটি memory buffer এ লগ মেসেজ সেভ করে থাকে।                     
```
public class HandlerExample {
    private static final Logger LOGGER = Logger.getLogger(LoggerExample.class.getName());

    public static void main(String[] args) {

        Handler consoleHandler = null;
        Handler fileHandler = null;
        try {
            //Creating consoleHandler and fileHandler
            consoleHandler = new ConsoleHandler();
            fileHandler = new FileHandler("./util.handler.log");

            //Assigning handlers to LOGGER object
            LOGGER.addHandler(consoleHandler);
            LOGGER.addHandler(fileHandler);

            //Setting levels to handlers and LOGGER
            consoleHandler.setLevel(Level.ALL);
            fileHandler.setLevel(Level.ALL);
            LOGGER.setLevel(Level.ALL);

            LOGGER.config("Configuration done.");

            //Console handler removed
            LOGGER.removeHandler(consoleHandler);

            LOGGER.log(Level.FINE, "Finer logged");
        } catch (IOException exception) {
            LOGGER.log(Level.SEVERE, "Error occur in FileHandler.", exception);
        }
        LOGGER.finer("Finest example on LOGGER handler completed.");
    }
}
```

**Formatter**            
এই কম্পোনেন্ট লগ রেকর্ডকে নির্দিষ্ট ফরম্যাটে সেভ করে।  হ্যান্ডলার ডেস্টিনেশনে ডাটা সেভ হওয়ার আগে Formatter তাকে ফরম্যাট দেয়। Formatter দুই রকমেরঃ               
SimpleFormatter: মেসেজ টেক্সট আকারে সেভ হয়।         
XMLFormatter: মেসেজ এক্সএমএল আকারে সেভ হয়।                         
```
public class FormatterExample {
    private static final Logger LOGGER = Logger.getLogger(LoggerExample.class.getName());

    public static void main(String[] args) {

        Handler fileHandler = null;
        SimpleFormatter simpleFormatter = null;
        try {
            // Creating FileHandler
            fileHandler = new FileHandler("./util.formatter.log");

            // Creating SimpleFormatter
            simpleFormatter = new SimpleFormatter();

            // Assigning handler to logger
            LOGGER.addHandler(fileHandler);

            // Logging message of Level info (this should be publish in the default format i.e. XMLFormat)
            LOGGER.info("Finnest message: Logger with DEFAULT FORMATTER");

            // Setting formatter to the handler
            fileHandler.setFormatter(simpleFormatter);

            // Setting Level to ALL
            fileHandler.setLevel(Level.ALL);
            LOGGER.setLevel(Level.ALL);

            // Logging message of Level finest (this should be publish in the simple format)
            LOGGER.finest("Finnest message: Logger with SIMPLE FORMATTER");
        } catch (IOException exception) {
            LOGGER.log(Level.SEVERE, "Error occur in FileHandler.", exception);
        }
    }
}
```

**Filter**          
Filter হল java.util.logging প্যাকেজের একটা ইন্টারফেস। এটা হ্যান্ডলা্রের মেসেজ কন্ট্রোল করে। লগার আর হ্যান্ডলার Filter ব্যবহার করতে পারে। Filter এর isLoggable মেথড থাকে যেটা boolean রিটার্ন করে। মেসেজ পাবলিশ করার আগে Logger/Handler isLoggable মেথডটি কল করে, যদি true রিটার্ন করে তাহলে মেসেজ পাবলিশ হয় অন্যথায় পাবলিশ করা থেকে বিরত থাকে।      

```
public class FilterExample implements Filter {
    private static final Logger LOGGER = Logger.getLogger(LoggerExample.class.getName());
    public static void main(String[] args) {
        //Setting filter FilterExample
        LOGGER.setFilter(new FilterExample());
        //Since this message string does not contain the word important. Despite of being the Level SEVERE this will be ignored
        LOGGER.severe("This is SEVERE message");
        //This will get published
        LOGGER.warning("This is important warning message");
    }

    // This method will return true only if the LogRecord object contains the message which contains the word important
    @Override
    public boolean isLoggable(LogRecord record) {
        if(record == null)
            return false;

        String message = record.getMessage()==null?"":record.getMessage();

        if(message.contains("important"))
            return true;

        return false;
    }
}
```     

**Configuration**            
লগার অবজেক্টে কনফিগারেশন প্রোপার্টিজ লিখে দেওয়া যায়। লগার অবজেক্ট কনফিগারেশন ফাইল ব্যবহার করে। ডিফল্ট কনফিগারেশন রিমুভ করে একে সুবিধামত কনফিগার করা যায়। LogManager এই সুবিধা দিয়ে থাকে।          

```
public class ConfigurationExample {
    private static final LogManager logManager = LogManager.getLogManager();
    private static final Logger LOGGER = Logger.getLogger("confLogger");
    static{
        try {
            logManager.readConfiguration(new FileInputStream("./src/main/resources/util.configuration.properties"));
        } catch (IOException exception) {
            LOGGER.log(Level.SEVERE, "Error in loading configuration",exception);
        }
    }
    public static void main(String[] args) {
        LOGGER.fine("Fine message logged");
    }
}
```

