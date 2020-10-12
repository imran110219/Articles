# ক্রিপ্টোগ্রাফি (Cryptography)  
ক্রিপ্টোগ্রাফি হল এমন একটি প্রযুক্তি যার মাধ্যমে আমরা কোন তথ্য নিরাপদে এবং সুরক্ষিত ভাবে এক জায়গা থেকে অন্য জায়গায় পাঠানো যায়।  এই ক্ষেত্রে একজন যখন অন্য জনকে কোন তথ্য পাঠাবে সেই ক্ষেত্রে যার কাছে পাঠানো হচ্ছে তার কাছে একটি গোপন কোড থাকবে যা দ্বারা সে তথ্যটি পাবে। বিষয়টা কিছু টা তালা চাবি কনসেপ্টের মত অর্থাৎ কাছে চাবি থাকলেই সে মেসেজটা দেখে বুঝতে পারবে।    
বিষয় টা উদাহরনসহ ব্যাখ্যা করলে আরো পরিষ্কার হবে। ধরা যাক, রহিম নামক একজন ব্যাক্তি করিমকে একটি গোপন মেসেজ পাঠাতে চায় এবং সে চায় এইটা যেন কেউ না দেখুক। রহিম করিম কে মেসেজ পাঠাল কিন্তু একটি বিশেষ পদ্ধতি অবলম্বন করে। রহিম যে মেসেজটি পাঠাতে চায় সেটা হল "come to my home" কিন্তু সে পাঠাল "eqog vq oa jqog"। রহিম করিমকে আগেই বলে রেখেছিল যে সে যা মেসেজ পাঠাবে সেইটার প্রতিটি অক্ষরের আগের দুই অক্ষর হবে। সেই সুত্র অনুযায়ী করিম মেসেজটা উদ্ধার করতে পারলো। যেমন e এর দুই ঘর আগে c অর্থাৎ e->c, q->o, o->m, g->e, v->t, q->o, o->m, a->y j->h, q->o, o->m, g->e. 

ক্রিপ্টোগ্রাফির কিছু বৈশিষ্ট্য আছে। সেগুলো হলঃ        
1. Confidentiality:
Information can only be accessed by the person for whom it is intended and no other person except him can access it.
2. Integrity:
Information cannot be modified in storage or transition between sender and intended receiver without any addition to information being detected.
3. Non-repudiation:
The creator/sender of information cannot deny his or her intention to send information at later stage.
4. Authentication:
The identities of sender and receiver are confirmed. As well as destination/origin of information is confirmed.    

ক্রিপ্টোগ্রাফির ধরনঃ    


* https://www.tutorialspoint.com/cryptography/origin_of_cryptography.htm#:~:text=The%20first%20known%20evidence%20of,on%20behalf%20of%20the%20kings.   
* https://www.edureka.co/blog/what-is-cryptography/
* https://www.geeksforgeeks.org/cryptography-and-its-types/