

# 📘 Laravel 5.5 Full Project Guide (Lifecycle + Folder Structure + Term Description)

---

## 🔥 Laravel কীভাবে কাজ করে? (Lifecycle Step-by-Step)

### 1️⃣ **Entry Point: `public/index.php`**

👉 Laravel অ্যাপের সব Request শুরু হয় এখান থেকে। এটি Composer এর Autoload ফাইল এবং Laravel অ্যাপ বুটস্ট্র্যাপ করে।

### 2️⃣ **Autoload: `vendor/autoload.php`**

👉 Composer দ্বারা ইন্সটল করা সব প্যাকেজ ও ক্লাস এখানে রেজিস্টার থাকে।

### 3️⃣ **Bootstrap App: `bootstrap/app.php`**

👉 Laravel Application তৈরি করে এবং সার্ভিস প্রোভাইডার রেজিস্টার করে।

### 4️⃣ **HTTP Kernel: `app/Http/Kernel.php`**

👉 Laravel এর রিকোয়েস্ট-রেসপন্স লাইফসাইকেল পরিচালনা করে। এটি Middleware চালায়।

### 5️⃣ **Middleware**

👉 রিকোয়েস্ট ফিল্টার করার জন্য ব্যবহৃত হয় (যেমন: Auth, CSRF, Logging ইত্যাদি)।

### 6️⃣ **Routing: `routes/web.php`**

👉 কোন URL-এ কোন Controller বা Logic রান হবে, তা নির্ধারণ করে।

### 7️⃣ **Controller: `app/Http/Controllers/...`**

👉 ইউজারের অনুরোধ গ্রহণ করে, লজিক প্রসেস করে, ডেটা ফেচ করে এবং View রিটার্ন করে।

### 8️⃣ **Model: `app/...`**

👉 ডেটাবেজের টেবিলের সাথে অবজেক্ট রিলেশন তৈরি করে এবং ডেটা হ্যান্ডল করে।

### 9️⃣ **View: `resources/views/...`**

👉 Blade Template Engine ব্যবহার করে HTML রেন্ডার করে।

### 🔚 **Response**

👉 View, JSON বা অন্য ফরম্যাটে ব্রাউজারে রেসপন্স পাঠায়।

---

## 🗂️ Laravel 5.5 Folder Structure + Term Description

| 📁 Folder/File          | 🧾 Description                                                            |
| ----------------------- | ------------------------------------------------------------------------- |
| `app/`                  | মূল অ্যাপ কোড এখানে থাকে। Controller, Model, Middleware এই ফোল্ডারে থাকে। |
| └── `Http/Controllers/` | সব Controller ক্লাস রাখার জায়গা। ইউজারের অনুরোধ হ্যান্ডল করে।             |
| └── `Http/Middleware/`  | Request হ্যান্ডল করার আগেই যা ফিল্টার করে।                                |
| └── `Console/`          | কাস্টম Artisan কমান্ড রাখা হয় এখানে।                                      |
| `bootstrap/`            | অ্যাপ্লিকেশন বুটস্ট্র্যাপ (চালু) করার কোড।                                |
| └── `app.php`           | Laravel App এর instance তৈরি করে।                                         |
| `config/`               | সব কনফিগারেশন ফাইল এখানে থাকে (app.php, database.php ইত্যাদি)।            |
| `database/`             | মাইগ্রেশন, ফ্যাক্টরি, সিডার ফাইল রাখা হয়।                                 |
| `public/`               | ওয়েব সার্ভার এখান থেকে শুরু হয়। `index.php` Laravel এর entry point।       |
| `resources/views/`      | Blade টেমপ্লেট ফাইল (HTML) এখানে থাকে।                                    |
| `resources/assets/`     | CSS (SASS), JS ইত্যাদি ফ্রন্টএন্ড ফাইল।                                   |
| `routes/web.php`        | ওয়েব রাউট (URL -> Controller) সংজ্ঞায়িত করা হয়।                          |
| `storage/`              | ক্যাশ, লগ, আপলোড ফাইল ইত্যাদি থাকে।                                       |
| `tests/`                | অটোমেটেড টেস্ট ফাইল রাখা হয়।                                              |
| `vendor/`               | Composer প্যাকেজ গুলো এখানে থাকে। Laravel Framework সহ।                   |
| `.env`                  | এনভায়রনমেন্ট ভ্যারিয়েবল (DB, APP\_NAME, API\_KEY ইত্যাদি)।               |
| `artisan`               | Laravel এর CLI টুল। যেমন: `php artisan serve`, `php artisan migrate`      |
| `composer.json`         | PHP প্যাকেজ ডিপেন্ডেন্সি ডিফাইন করে।                                      |
| `package.json`          | JS/NPM ডিপেন্ডেন্সি সংজ্ঞা করে। (Bootstrap, jQuery ইত্যাদি)               |
| `webpack.mix.js`        | Laravel Mix কনফিগারেশন। SASS, JS Compile করার জন্য ব্যবহৃত হয়।            |

---

## 🛠️ Laravel + Bootstrap Entry Points

| 🔧 File                          | 📌 Function                                                             |
| -------------------------------- | ----------------------------------------------------------------------- |
| `resources/assets/sass/app.scss` | Bootstrap SCSS/CSS import করা হয় এখানে।                                 |
| `resources/assets/js/app.js`     | Bootstrap JS এবং jQuery লোড হয় এখান থেকে।                               |
| `webpack.mix.js`                 | JS/SASS Compile করে `public/css/app.css` ও `public/js/app.js` তৈরি করে। |

🔻 রান করার জন্য:

```bash
npm install
npm run dev   # বা production: npm run production
```

---

## 🔁 Laravel Lifecycle Recap (Flow Diagram)

```text
Browser Request
     ↓
public/index.php
     ↓
bootstrap/app.php
     ↓
app/Http/Kernel.php
     ↓
Middleware
     ↓
routes/web.php
     ↓
Controller
     ↓
Model → Database
     ↓
View (Blade)
     ↓
Response to Browser
```

---

## 🧪 Artisan CLI গুরুত্বপূর্ণ কমান্ড

| কমান্ড                                     | কাজ                               |
| ------------------------------------------ | --------------------------------- |
| `php artisan serve`                        | Laravel local server চালায়        |
| `php artisan make:controller MyController` | নতুন Controller তৈরি করে          |
| `php artisan make:model Post -m`           | Model ও Migration একসাথে তৈরি করে |
| `php artisan migrate`                      | DB মাইগ্রেশন চালায়                |
| `php artisan route:list`                   | সব route দেখায়                    |

---

## 🎯 উপসংহার

এই ডকুমেন্টেশনটি Laravel 5.5 এর:

* Full Lifecycle
* ফোল্ডার স্ট্রাকচার
* প্রতিটি ফোল্ডারের কাজ
* Bootstrap integration
* CLI কমান্ড

