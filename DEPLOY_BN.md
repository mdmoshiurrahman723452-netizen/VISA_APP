# অনলাইনে প্রকাশ করার নির্দেশনা (বাংলা)

এই প্রজেক্টটি Docker-ভিত্তিকভাবে Render-এ প্রকাশ করার জন্য প্রস্তুত করা হয়েছে। এটি এখনো নিজে থেকে অনলাইনে প্রকাশিত নয়; প্রকাশের জন্য আপনার নিজের GitHub ও Render অ্যাকাউন্টে অনুমোদিত পদক্ষেপ নিতে হবে।

## প্রকাশের আগে
1. `templates/visa_template.docx` এবং তৈরি হওয়া PDF হাতে-কলমে তুলনা করুন। সব ফিল্ডের অবস্থান, আরবি লেখা, পৃষ্ঠা বিন্যাস এবং অফিসিয়াল অংশ যাচাই না করা পর্যন্ত বাস্তব ভিসা কাজে ব্যবহার করবেন না।
2. `For Official use only` অংশের ভিসা নম্বর, অনুমোদন নম্বর, অফিসিয়াল তারিখ ও কর্তৃপক্ষের তথ্য স্বয়ংক্রিয়ভাবে তৈরি করবেন না।
3. বাস্তব পাসপোর্ট তথ্যের আগে ডেটা অ্যাক্সেস, ব্যাকআপ, retention ও deletion নীতি ঠিক করুন।

## Render-এ প্রকাশ
1. GitHub-এ নতুন private repository তৈরি করুন।
2. এই ZIP extract করে এর ভেতরের সব ফাইল repository-তে upload/commit করুন। `visa_generator_starter` ফোল্ডারের ফাইলগুলো repository-র root-এ রাখুন।
3. Render-এ সাইন ইন করে **New + → Blueprint** বেছে নিয়ে GitHub repository সংযুক্ত করুন।
4. Render `render.yaml` পড়ে Docker service ও `/var/data` persistent disk সেটআপ করবে।
5. `VISA_APP_USERNAME` এবং `VISA_APP_PASSWORD` environment variable চাইলে দিন। শক্তিশালী, অনন্য পাসওয়ার্ড ব্যবহার করুন; এই ফাইল বা GitHub-এ secret লিখবেন না।
6. Deploy সম্পন্ন হলে Render একটি `https://...onrender.com` URL দেবে। সেটি ব্রাউজারে খুলুন।
7. Basic Authentication prompt-এ Render-এ সেট করা username/password দিন।

## ডেটা সংরক্ষণ
- SQLite database এবং তৈরি করা DOCX/PDF `/var/data`-তে থাকবে, যা Render persistent disk-এ মাউন্ট করা।
- Persistent disk সাধারণত paid service plan চাইতে পারে; Render-এর বর্তমান মূল্য ও disk availability প্রকাশের সময় যাচাই করুন। Free ephemeral filesystem-এ গুরুত্বপূর্ণ আবেদন ডেটা রাখবেন না।
- ডেটাবেজের নিরাপদ ব্যাকআপ আলাদা করে কনফিগার করতে হবে।

## সীমাবদ্ধতা
- এটি প্রথম deployable prototype, production security audit করা পণ্য নয়।
- HTTP Basic Auth সহজ access gate; বহু কর্মী, role-based permissions, audit log, rate limiting, CSRF protections, encrypted backups এবং retention policy দরকার হলে সেগুলো যোগ করতে হবে।
- Render account, GitHub connection বা deployment credential এখানে দেওয়ার দরকার নেই এবং চ্যাটে শেয়ার করবেন না।
