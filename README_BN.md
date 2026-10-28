# Visa Application Form Generator — প্রাথমিক সংস্করণ

## কী আছে
- `templates/visa_template.docx`: আপনার Word ফাইল থেকে তৈরি টেমপ্লেট; আবেদনকারীর নির্ধারিত ফিল্ডে placeholder বসানো হয়েছে।
- `field_mapping.json`: ফিল্ড ও placeholder-এর তালিকা।
- `app.py`: FastAPI-ভিত্তিক প্রাথমিক ওয়েব অ্যাপ; যাত্রীর তথ্য সংরক্ষণ, PDF তৈরি, ডাউনলোড এবং আবেদন ইতিহাস।
- SQLite ডেটাবেজ প্রথম চালুতে স্বয়ংক্রিয়ভাবে তৈরি হবে।

## গুরুত্বপূর্ণ সীমা
- “For Official use only” অংশের ভিসা নম্বর, অনুমোদন নম্বর, অফিসিয়াল তারিখ ও কর্তৃপক্ষের তথ্য নতুন আবেদন অনুযায়ী স্বয়ংক্রিয়ভাবে তৈরি করা হয় না। টেমপ্লেট থেকে পুরোনো অফিসিয়াল নম্বরগুলো ফাঁকা রাখা হয়েছে। এগুলো কেবল অনুমোদিত কর্তৃপক্ষের মাধ্যমে পূরণ হওয়া উচিত।
- মূল DOCX-এ থাকা টেবিল/কলাম কাঠামো জটিল। বাস্তব ব্যবহারের আগে LibreOffice-এ তৈরি PDF-এর সঙ্গে মূল ফর্ম পাশাপাশি দেখে ফন্ট, আরবি লেখা, পৃষ্ঠা বিন্যাস ও প্রতিটি ফিল্ডের অবস্থান যাচাই করতে হবে।
- এই প্রাথমিক সংস্করণে পাসপোর্ট নম্বর দিয়ে যাত্রীকে চেনা হয়; বাস্তব ব্যবহারের আগে ডুপ্লিকেট পাসপোর্ট, সংশোধন ও অ্যাক্সেস লগের নীতি নির্ধারণ করা দরকার।
- এটি লোকাল পরীক্ষার starter, এখনই উন্মুক্ত ইন্টারনেটে প্রকাশ করবেন না। HTTPS, নিয়মিত নিরাপদ ব্যাকআপ, অনুমতি, ডেটা-রিটেনশন ও প্রোডাকশন সিকিউরিটি যাচাই প্রয়োজন।

## চালানোর পদ্ধতি
Python 3.11+ এবং LibreOffice ইনস্টল থাকতে হবে।

```bash
python -m venv .venv
# Windows:
.venv\\Scripts\\activate
# macOS/Linux:
source .venv/bin/activate
pip install -r requirements.txt

# Windows PowerShell:
$env:VISA_APP_USERNAME="operator"
$env:VISA_APP_PASSWORD="change-this-to-a-long-unique-password"
# macOS/Linux:
export VISA_APP_USERNAME="operator"
export VISA_APP_PASSWORD="change-this-to-a-long-unique-password"

uvicorn app:app --reload
```
তারপর `http://127.0.0.1:8000` খুলুন। ব্রাউজার Basic Authentication চাইলে উপরের username/password দিন।

## পরবর্তী পরীক্ষার ধাপ
1. আপনার আসল DOCX ও তৈরি হওয়া PDF পাশাপাশি তুলনা করুন।
2. দীর্ঘ নাম, আরবি পেশা, তারিখ ও পাসপোর্ট নম্বর দিয়ে পরীক্ষা করুন।
3. সব ফিল্ড ঠিক অবস্থানে বসলে তবেই অনলাইন সার্ভারে প্রকাশের পরিকল্পনা করুন।

## অনলাইনে প্রকাশ
Dockerfile ও `render.yaml` যোগ করা হয়েছে। অনলাইনে প্রকাশের জন্য `DEPLOY_BN.md` অনুসরণ করুন। এটি নিজে থেকে live website নয়; আপনার GitHub/Render account দিয়ে deploy করতে হবে।
