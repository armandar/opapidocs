# مستندات
<div dir="rtl">
در مستند زیر می‌توانید نحوه استفاده از api پروژه op را مشاهده و از آن استفاده نمایید.
</div>

# شروع

## ورود

<div dir="rtl">
برای ارسال درخواست ورود باید به لینک زیر درخواست بزنید.(این آدرس‌ها درست نیستند.)
</div>

### url: armandar.com/api/v1/login

### method: post

<div dir="rtl">
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
نمونه کد ارسالی با استفاده از unirest در جاوا به صورت زیر است:
</div>

```java
HttpResponse<String> response = Unirest.post("http://armandar.com/api/v1/login")
  .header("content-type", "application/x-www-form-urlencoded")
  .header("cache-control", "no-cache")
  .body("grant_type=password&username=username&password=password")
  .asString();
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

<div dir="rtl">
در غیر این صورت و صحت نام کاربری و کلمه عبور، اطلاعاتی به این صورت دریافت خواهید کرد:
</div>

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


<div dir="rtl">
از access_token دریافتی میتوانید برای اتصال به api استفاده کنید. نحوه استفاده آن در بخش‌ بعدی توضیح داده خواهد شد.
</div>


## Authorization

<div dir="rtl">
تمام اطلاعات ارسالی از سمت کلاینت‌ها به سرور (به جز در هنگام لاگین) باید این هدر را داشته باشد.
</div>


```json
headers: {
    "authorization": "Bearer gyXOAl0G4lg5LQYDa-py4JyHcCaaChlYODpdwu1e8zKT05N...."
}
```


<div dir="rtl">
که عبارت‌است از کلمه Bearer  به علاوه یک Space و مقدار access_token که در هنگام ورود دریافت کرده‌اید.
</div>

Bearer {space} {access_token}


<div dir="rtl">
درصورتی که این هدر را نفرستید یا مقدار access_token آن اشتباه باشد با خطایی مشابه زیر موجه خواهید شد.
</div>

```json
{
  "Message": "Authorization has been denied for this request."
}
```



# هشدارها
## url: armandar.com/api/v1/alerts
## method: get


<div dir="rtl">
برای دریافت هشدارها از این آدرس استفاده کنید. نتیجه به این صورت خواهدبود.
</div>

```json
[
    {
        "Count": 8397,
        "Title": "مجموع",
        "Url": "#",
        "Order": 0,
        "EnTitle": "Count"
    },
    {
        "Count": 235,
        "Title": "پروژه ها با درصد انحراف بالا",
        "Url": "#",
        "Order": 1,
        "EnTitle": "AlertCount"
    },
    {
        "Count": 101,
        "Title": "پروژه های بدون مرحله",
        "Url": "/Shared/Alarm/ProjectStepIssue",
        "Order": 2,
        "EnTitle": "ProjectStepIssueCount"
    },
    {
        "Count": 29,
        "Title": "فاکتور وزنی مراحل پروژه",
        "Url": "/Shared/Alarm/ProjectWFIssue",
        "Order": 3,
        "EnTitle": "ProjectWFIssueCount"
    },
    {
        "Count": 2241,
        "Title": "مستندات مراحل پروژه",
        "Url": "/Shared/Alarm/ProjectFileIssue",
        "Order": 4,
        "EnTitle": "ProjectFileIssueCount"
    },
    {
        "Count": 2792,
        "Title": "لینک پروژه به چالش",
        "Url": "/Shared/Alarm/ProjectChallengeIssue",
        "Order": 5,
        "EnTitle": "ProjectChallengeIssueCount"
    },
    {
        "Count": 2951,
        "Title": "لینک پروژه به اهداف",
        "Url": "/Shared/Alarm/ProjectGoalIssue",
        "Order": 6,
        "EnTitle": "ProjectGoalIssueCount"
    },
    {
        "Count": 0,
        "Title": "اخبار جدید",
        "Url": "/Administration/News",
        "Order": 7,
        "EnTitle": "NewNewsCount"
    },
    {
        "Count": 48,
        "Title": "پروژه های متوقف شده",
        "Url": "#",
        "Order": 8,
        "EnTitle": "StopedProjectCount"
    }
]
```


<div dir="rtl">
همواره اولین آیتم مجموع است و بقیه آیتم‌ها در زیر آن با عنوان فارسی و تعداد  نمایش داده شده است.
</div>


<div dir="rtl">
</div>