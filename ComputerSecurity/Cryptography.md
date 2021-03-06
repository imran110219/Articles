# ক্রিপ্টোগ্রাফি (Cryptography)  
ক্রিপ্টোগ্রাফি হল এমন একটি প্রযুক্তি যার মাধ্যমে আমরা কোন তথ্য নিরাপদে এবং সুরক্ষিত ভাবে এক জায়গা থেকে অন্য জায়গায় পাঠানো যায়।  এই ক্ষেত্রে একজন যখন অন্য জনকে কোন তথ্য পাঠাবে সেই ক্ষেত্রে যার কাছে পাঠানো হচ্ছে তার কাছে একটি গোপন কোড থাকবে যা দ্বারা সে তথ্যটি পাবে। বিষয়টা কিছু টা তালা চাবি কনসেপ্টের মত অর্থাৎ কাছে চাবি থাকলেই সে মেসেজটা দেখে বুঝতে পারবে।    
বিষয় টা উদাহরনসহ ব্যাখ্যা করলে আরো পরিষ্কার হবে। ধরা যাক, রহিম নামক একজন ব্যাক্তি করিমকে একটি গোপন মেসেজ পাঠাতে চায় এবং সে চায় এইটা যেন কেউ না দেখুক। রহিম করিম কে মেসেজ পাঠাল কিন্তু একটি বিশেষ পদ্ধতি অবলম্বন করে। রহিম যে মেসেজটি পাঠাতে চায় সেটা হল "come to my home" কিন্তু সে পাঠাল "eqog vq oa jqog"। রহিম করিমকে আগেই বলে রেখেছিল যে সে যা মেসেজ পাঠাবে সেইটার প্রতিটি অক্ষরের আগের দুই অক্ষর হবে। সেই সুত্র অনুযায়ী করিম মেসেজটা উদ্ধার করতে পারলো। যেমন e এর দুই ঘর আগে c অর্থাৎ e->c, q->o, o->m, g->e, v->t, q->o, o->m, a->y j->h, q->o, o->m, g->e.   


**ক্রিপ্টোগ্রাফি বিষয়ক কি-ওয়ার্ডঃ**         
**Encrypt:** হল টেক্সট মেসেজকে গোপন কোডে পরিবর্তন করা।            
**Decrypt:** হল গোপন কোডেকে টেক্সট মেসেজ পরিবর্তন করা।       
**Plain Text:** হল প্রেরক আসল যে মেসেজটা পাঠায়।         
**Cipher Text:** হল Encrypt করা গোপন কোড।        
**Key:** এর সাহায্যে কোন মেসেজ Encrypt/Decrypt করা যায়।           


**ক্রিপ্টোগ্রাফির বৈশিষ্ট্যঃ**              
**1. Confidentiality:** তথ্য যার কাছে পাঠানো হয়েছে সেই শুধু পাবে এবং অন্য কেউ এটা বুঝতে পারবে না।                          
**2. Integrity:** প্রেরক এবং প্রাপকের তথ্য আদান প্রদানের মাঝখানে তথ্য কোনভাবেই পরিবর্তন হবে না।                    
**3. Non-repudiation:** তথ্যের প্রেরক কখনো অস্বীকার করতে পারবেন না যে উনি তথ্য পাঠান নি।                      
**4. Authentication:** তথ্য সবসময় প্রেরক এবং প্রাপকের মধ্যেই সীমাবদ্ধ থাকে।                       

**ক্রিপ্টোগ্রাফির ধরনঃ**       
**1. Symmetric Key Cryptography:**      
এই ক্রিপ্টোগ্রাফি সিস্টেমে প্রেরক এবং প্রাপক কোন তথ্য একই key দিয়ে encrypt এবং decrypt করে। এই পদ্ধতি দ্রুততম এবং সাধারন কিন্তু সমস্যা হচ্ছে প্রেরক ও প্রাপক একই key দিয়ে কাজ করবে। সুতরাং অন্য কেউ যদি key পেয়ে  যায় তাহলে মেসেজ পড়তে পারবে। Data Encryption System(DES) সবচেয়ে বেশি ব্যবহৃত হয়।                
**ব্যবহারঃ**        
1. Payment applications       

**List of Algorithm**  
* [Advanced Encryption Standard (AES)](Cryptography/AES.md)       
* [Data Encryption System (DES)](Cryptography/DES.md)      

**2. Hash Functions:**     
এই ক্রিপ্টোগ্রাফি সিস্টেমে encrypt করার জন্য কোন key এর দরকার হয় না। কোন টেক্সটকে hash করলে সেটা সময় নির্দিষ্ট সংখ্যক ভ্যালু হয় এবং কোন hash টেক্সটকে decrypt করা যায় না। এটা সবচেয়ে বেশি ব্যবহার করা হয় পাসওয়ার্ড hash করে রাখার জন্য।                
**ব্যবহারঃ**      

**List of Algorithm**   
* Message-Digest algorithm 5 (MD5)     
* Secure Hash Algorithm(SHA-1, SHA-2, SHA-3)


**3. Asymmetric Key Cryptography:**        
এই সিস্টেমে ২ টা আলাদা key ব্যবহার করা হয়। একটা encrypt করার জন্য public key আর অন্যটা decrypt করার জন্য private key। এই ক্ষেত্রে public key সবাই জেনে গেলেও কোন সমস্যা নাই কারন সেটা decrypt করা যাবে শুধু private key দিয়ে। এইটা Public Key Cryptography নামে ও পরিচিত।              
**ব্যবহারঃ**       
* Digital signatures

**List of Algorithm**   
* RSA
* Elliptic Curve Cryptography (ECC)


* https://www.tutorialspoint.com/cryptography/origin_of_cryptography.htm#:~:text=The%20first%20known%20evidence%20of,on%20behalf%20of%20the%20kings.   
* https://www.edureka.co/blog/what-is-cryptography/
* https://www.geeksforgeeks.org/cryptography-and-its-types/