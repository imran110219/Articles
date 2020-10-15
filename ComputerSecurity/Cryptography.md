# ক্রিপ্টোগ্রাফি (Cryptography)  
ক্রিপ্টোগ্রাফি হল এমন একটি প্রযুক্তি যার মাধ্যমে আমরা কোন তথ্য নিরাপদে এবং সুরক্ষিত ভাবে এক জায়গা থেকে অন্য জায়গায় পাঠানো যায়।  এই ক্ষেত্রে একজন যখন অন্য জনকে কোন তথ্য পাঠাবে সেই ক্ষেত্রে যার কাছে পাঠানো হচ্ছে তার কাছে একটি গোপন কোড থাকবে যা দ্বারা সে তথ্যটি পাবে। বিষয়টা কিছু টা তালা চাবি কনসেপ্টের মত অর্থাৎ কাছে চাবি থাকলেই সে মেসেজটা দেখে বুঝতে পারবে।    
বিষয় টা উদাহরনসহ ব্যাখ্যা করলে আরো পরিষ্কার হবে। ধরা যাক, রহিম নামক একজন ব্যাক্তি করিমকে একটি গোপন মেসেজ পাঠাতে চায় এবং সে চায় এইটা যেন কেউ না দেখুক। রহিম করিম কে মেসেজ পাঠাল কিন্তু একটি বিশেষ পদ্ধতি অবলম্বন করে। রহিম যে মেসেজটি পাঠাতে চায় সেটা হল "come to my home" কিন্তু সে পাঠাল "eqog vq oa jqog"। রহিম করিমকে আগেই বলে রেখেছিল যে সে যা মেসেজ পাঠাবে সেইটার প্রতিটি অক্ষরের আগের দুই অক্ষর হবে। সেই সুত্র অনুযায়ী করিম মেসেজটা উদ্ধার করতে পারলো। যেমন e এর দুই ঘর আগে c অর্থাৎ e->c, q->o, o->m, g->e, v->t, q->o, o->m, a->y j->h, q->o, o->m, g->e.   


**ক্রিপ্টোগ্রাফি বিষয়ক কি-ওয়ার্ডঃ**         
**Encrypt**    
**Decrypt**      
**Plain Text**     
**Cipher Text**       
**Key**    


**ক্রিপ্টোগ্রাফির বৈশিষ্ট্যঃ**              
**1. Confidentiality:** তথ্য যার কাছে পাঠানো হয়েছে সেই শুধু পাবে এবং অন্য কেউ এটা বুঝতে পারবে না।                          
**2. Integrity:** প্রেরক এবং প্রাপকের তথ্য আদান প্রদানের মাঝখানে তথ্য কোনভাবেই পরিবর্তন হবে না।                    
**3. Non-repudiation:** তথ্যের প্রেরক কখনো অস্বীকার করতে পারবেন না যে উনি তথ্য পাঠান নি।                      
**4. Authentication:** তথ্য সবসময় প্রেরক এবং প্রাপকের মধ্যেই সীমাবদ্ধ থাকে।                       

**ক্রিপ্টোগ্রাফির ধরনঃ**       
**Symmetric Key Cryptography:**     
এই ক্রিপ্টোগ্রাফি সিস্টেমে প্রেরক এবং প্রাপক কোন তথ্য একই key দিয়ে encrypt এবং decrypt করে। এই পদ্ধতি দ্রুততম এবং সাধারন কিন্তু সমস্যা হচ্ছে প্রেরক ও প্রাপক একই key দিয়ে কাজ করবে। সুতরাং অন্য কেউ যদি key পেয়ে  যায় তাহলে মেসেজ পড়তে পারবে। Data Encryption System(DES) সবচেয়ে বেশি ব্যবহৃত হয়।              
It is an encryption system where the sender and receiver of message use a single common key to encrypt and decrypt messages. Symmetric Key Systems are faster and simpler but the problem is that sender and receiver have to somehow exchange key in a secure manner. The most popular symmetric key cryptography system is Data Encryption System(DES).
**Hash Functions:**    

There is no usage of any key in this algorithm. A hash value with fixed length is calculated as per the plain text which makes it impossible for contents of plain text to be recovered. Many operating systems use hash functions to encrypt passwords.
**Asymmetric Key Cryptography:**
Under this system a pair of keys is used to encrypt and decrypt information. A public key is used for encryption and a private key is used for decryption. Public key and Private Key are different. Even if the public key is known by everyone the intended receiver can only decode it because he alone knows the private key. 


* https://www.tutorialspoint.com/cryptography/origin_of_cryptography.htm#:~:text=The%20first%20known%20evidence%20of,on%20behalf%20of%20the%20kings.   
* https://www.edureka.co/blog/what-is-cryptography/
* https://www.geeksforgeeks.org/cryptography-and-its-types/