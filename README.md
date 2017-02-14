<div dir="rtl">

# مستندات api برای پروژه op
در مستند زیر می‌توانید نحوه استفاده از api پروژه op را مشاهده و از آن استفاده نمایید.


# Getting Started
## Login
برای ارسال درخواست ورود باید به لینک زیر درخواست بزنید.(این آدرس‌ها درست نیستند.)


[http://armandar.com/api/v1/login](http://armandar.com/api/v1/login)

و موارد زیر را به هدر  درخواست خود اضافه نمایید.(Header)

</div>


```json
headers: {
    "content-type": "application/x-www-form-urlencoded",
    "cache-control": "no-cache"
}
```



<div dir="rtl">
دیتای ارسالی به آدرس نیز باید به این شرح باشد.:
</div>


```json
data: {
    "grant_type": "password",
    "username": "username",
    "password": "password"
}
```


<div dir="rtl">
نمونه کد ارسالی با استفاده از OkHttpClient در جاوا به صورت زیر است:
</div>


```java
OkHttpClient client = new OkHttpClient();

MediaType mediaType = MediaType.parse("application/x-www-form-urlencoded");
RequestBody body = RequestBody.create(mediaType, "grant_type=password&username=username&password=password");
Request request = new Request.Builder()
  .url("http://armandar.com/api/v1/login")
  .post(body)
  .addHeader("content-type", "application/x-www-form-urlencoded")
  .addHeader("cache-control", "no-cache")
  .build();

Response response = client.newCall(request).execute();
```


<div dir="rtl">
اگر نام کاربری یا کلمه عبور نادرست باشد این خطا را دریافت خواهید کرد:
</div>


```json
{
  "error": "invalid_grant",
  "error_description": "نام کاربری یا کلمه عبور اشتباه است."
}
```

otherwise responce will be like this:
```json
{
  "access_token": "r0WYlR82ArN5PnrM6wg............",
  "token_type": "bearer",
  "expires_in": 12959999,
  "userName": "username",
  ".issued": "Tue, 14 Feb 2017 14:07:57 GMT",
  ".expires": "Fri, 14 Jul 2017 14:07:57 GMT"
}
```

You mus