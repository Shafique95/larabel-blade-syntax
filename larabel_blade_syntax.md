Here's a comprehensive guide to **Laravel Blade syntax** with small examples for each category:

---

## 🔹 1. **Echoing Data**

### ✅ Basic Echo:

```blade
{{ $name }}
```

### ✅ Escaped (default, safe HTML):

```blade
{{ $html }}  {{-- escapes --}}
```

### ✅ Unescaped (dangerous if user input):

```blade
{!! $html !!}
```

---

## 🔹 2. **Control Structures**

Blade provides convenient shorthand for PHP control structures.

### ✅ If / Elseif / Else:

```blade
@if($age > 18)
    You are an adult.
@elseif($age == 18)
    Just turned adult.
@else
    You are a minor.
@endif
```

### ✅ Unless (opposite of if):

```blade
@unless($isAdmin)
    You are not an admin.
@endunless
```

### ✅ Isset:

```blade
@isset($title)
    <h1>{{ $title }}</h1>
@endisset
```

### ✅ Empty:

```blade
@empty($posts)
    No posts available.
@endempty
```

---

## 🔹 3. **Loops**

### ✅ For Loop:

```blade
@for($i = 0; $i < 5; $i++)
    <p>{{ $i }}</p>
@endfor
```

### ✅ Foreach:

```blade
@foreach($users as $user)
    <p>{{ $user->name }}</p>
@endforeach
```

### ✅ Forelse (with empty handling):

```blade
@forelse($tasks as $task)
    <li>{{ $task }}</li>
@empty
    <p>No tasks found.</p>
@endforelse
```

### ✅ While:

```blade
@while($i <= 3)
    <p>{{ $i++ }}</p>
@endwhile
```

---

## 🔹 4. **Include & Component**

### ✅ Include a partial:

```blade
@include('partials.header')
```

### ✅ Passing data:

```blade
@include('partials.user', ['user' => $user])
```

---

## 🔹 5. **Extending Layouts**

### ✅ Master Layout (`layouts/app.blade.php`)

```blade
<html>
<body>
    @yield('content')
</body>
</html>
```

### ✅ Child View:

```blade
@extends('layouts.app')

@section('content')
    <h1>Hello World</h1>
@endsection
```

---

## 🔹 6. **Components (Blade 7+)**

### ✅ Component:

```blade
<x-alert type="danger" :message="$message" />
```

---

## 🔹 7. **Sections and Yields**

### ✅ Define Section:

```blade
@section('title', 'Home Page')
```

### ✅ Use Section with content:

```blade
@section('content')
    <p>This is the content.</p>
@endsection
```

---

## 🔹 8. **Stacks & Push**

Useful for adding scripts/styles dynamically.

### ✅ In layout:

```blade
@stack('scripts')
```

### ✅ In child view:

```blade
@push('scripts')
    <script src="custom.js"></script>
@endpush
```

---

## 🔹 9. **Switch Case**

```blade
@switch($role)
    @case('admin')
        <p>Admin Panel</p>
        @break

    @case('user')
        <p>User Dashboard</p>
        @break

    @default
        <p>Guest</p>
@endswitch
```

---

## 🔹 10. **CSRF & Method Field**

### ✅ CSRF Token (Form security):

```blade
<form method="POST" action="/save">
    @csrf
    ...
</form>
```

### ✅ Spoofing PUT, PATCH, DELETE:

```blade
@method('PUT')
```

---

## 🔹 11. **Comment in Blade**

```blade
{{-- This is a Blade comment --}}
```

---

## 🔹 12. **Translation**

```blade
{{ __('Welcome') }}
{{ trans('messages.welcome') }}
```

---

Would you like a PDF cheat sheet of this with visuals?




**Laravel Blade** is called a **template engine** because it helps you write dynamic HTML pages easily by combining static HTML with dynamic content from your Laravel application.

Let me break it down in **Bangla with examples** so you understand it better:

---

### 🔧 Template Engine কী?

একটি **template engine** এমন একটি টুল, যা **HTML + ডায়নামিক ডেটা** একসাথে মিক্স করে সহজে ওয়েবপেজ তৈরি করতে সাহায্য করে।

---

### 🤖 Laravel Blade কী?

**Blade** হলো Laravel-এর নিজস্ব template engine। এটা `.blade.php` এক্সটেনশনে কাজ করে।

---

### ✅ Blade কীভাবে কাজ করে?

Blade আপনাকে PHP কোড সহজভাবে HTML-এর মধ্যে লিখতে দেয়।

#### উদাহরণ ১:

```blade
<!-- resources/views/welcome.blade.php -->
<html>
<body>
    <h1>Welcome, {{ $name }}!</h1>
</body>
</html>
```

Controller থেকে যদি পাঠানো হয়:

```php
return view('welcome', ['name' => 'Shafiqul']);
```

তাহলে এই Blade ফাইল HTML রেন্ডার করবে:

```html
<h1>Welcome, Shafiqul!</h1>
```

---

### 🔁 Loop, Condition ইত্যাদি সহজ করে Blade

#### If Condition:

```blade
@if($user->isAdmin)
    <p>Welcome, Admin!</p>
@else
    <p>Welcome, User!</p>
@endif
```

#### Loop:

```blade
@foreach($products as $product)
    <li>{{ $product->name }}</li>
@endforeach
```

---

### 📂 Blade Folder Structure (Laravel default):

```
resources/
└── views/
    ├── welcome.blade.php
    ├── layout.blade.php
    └── home.blade.php
```


### 🛠 Behind the Scene:

Blade ফাইলগুলো **PHP কোডে কম্পাইল** হয়ে `storage/framework/views` ফোল্ডারে গিয়ে রান হয়। তাই খুব দ্রুত লোড হয় এবং কোনো পারফরম্যান্স সমস্যা হয় না।



### 🤔 কেন Blade?

* HTML আর PHP আলাদা রাখতে সাহায্য করে
* কোড ক্লিন ও মেইনটেইনেবল হয়
* Reusable component (like layout, @include) সহজ হয়



### 📌 তাই Blade কে template engine বলা হয় কারণ:

1. এটা static HTML + dynamic PHP মিক্স করে
2. HTML templating সহজ ও ক্লিন করে
3. Laravel app এর ভিউ গুলো efficiently serve করতে সাহায্য করে

