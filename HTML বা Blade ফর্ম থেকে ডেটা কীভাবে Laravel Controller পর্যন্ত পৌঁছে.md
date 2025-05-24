 **"![how data save from blade form](https://github.com/user-attachments/assets/6a9efe72-a6f5-4b5f-b0c1-f02b0c6272f3)?"** সেটার ব্যাখ্যা নিচে বাংলায় ধাপে ধাপে দিলাম:

---

## 🧭 Step-by-Step: ফর্ম থেকে ডেটা কন্ট্রোলারে যাওয়ার প্রক্রিয়া (Laravel)

---

### 🧾 ১. ফর্ম তৈরি (HTML বা Blade)

```blade
<form action="{{ route('blog.store') }}" method="POST">
    <input type="hidden" name="_token" value="{{ csrf_token() }}">
    <input type="text" name="title" placeholder="Title" value="{{ old('title') }}">
    <textarea name="content" placeholder="Content">{{ old('content') }}</textarea>
    <button type="submit">Save</button>
</form>
```

#### 🔍 এখানে কী আছে:

* `method="POST"` → ডেটা পাঠানোর HTTP মেথড হচ্ছে POST
* `action="{{ route('blog.store') }}"` → Laravel এর রাউট `blog.store` কে লক্ষ্য করে
* `name="title"` আর `name="content"` → এগুলোর মাধ্যমে ইনপুট ফিল্ডের নাম নির্ধারিত হয়

---

### 📡 ২. ফর্ম সাবমিট হলে HTTP POST Request পাঠায়

* ইউজার যখন Save বাটনে ক্লিক করে,
* ব্রাউজার সেই ইনপুট ডেটা (যেমন title আর content) নিয়ে **POST** request পাঠায় `/store` URL-এ।

---

### 🌐 ৩. Laravel Route সেই URL ধরতে পারে

```php
Route::post('/store', 'BlogController@store')->name('blog.store');
```

#### ➤ কী হয় এখানে?

* Laravel দেখে `/store` URL এ POST রিকোয়েস্ট এসেছে
* সেটা রাউট `blog.store` এর সাথে ম্যাচ করে
* তাই `BlogController@store` মেথড কল হয়

---

### 📬 ৪. Controller মেথড `$request` অবজেক্ট পায়

```php
public function store(StoreBlogRequest $request)
{
    Blog::create($request->validated());
}
```

#### ➤ `$request` এর ভিতর কী থাকে?

* `title` আর `content` ফিল্ডে যেই ইনপুট দিয়েছিলে, সেটা `$request->input('title')` বা `$request->title` দিয়ে পাওয়া যায়
* Laravel internally এগুলোকে request body থেকে পড়েছে এবং `StoreBlogRequest` এর মাধ্যমে ভ্যালিড করেছে

---

### 🧠 অতিরিক্ত তথ্য: Request কিভাবে কাজ করে?

Laravel এই ইনপুট ডেটা নিচে থাকা রিকোয়েস্ট স্টেপের মাধ্যমে হ্যান্ডেল করে:

1. **Form Input** → ব্রাউজারে পাঠায় HTTP POST request
2. **Request Object** → Laravel `$request` এর মধ্যে সব ইনপুট ডেটা ধরে
3. **Validation** → `StoreBlogRequest` এর মাধ্যমে ইনপুট চেক করে
4. **Accessing Data**:

   * `$request->input('title')`
   * `$request->title`
   * `$request->only(['title', 'content'])`
5. **Then Save** → `Blog::create($request->validated())`

---

### 🔚 উপসংহার:

তুমি যখন Blade/HTML ফর্মে ইনপুট দাও এবং সাবমিট করো:

1. Browser → ডেটা পাঠায় `POST /store` এ
2. Laravel Route ধরে নেয় কোন Controller কাজ করবে
3. Controller সেই ইনপুট `$request` দিয়ে পায়
4. Validation হয় (FormRequest বা manual)
5. তারপর সেই ডেটা ডাটাবেজে সেভ হয়


