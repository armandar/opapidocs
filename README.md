# Api Reference
<div dir="rtl">
در مستند زیر می‌توانید نحوه استفاده از api پروژه op را مشاهده و از آن استفاده نمایید.
</div>

# Getting Started

## Login

<div dir="rtl">
برای ارسال درخواست ورود باید به لینک زیر درخواست بزنید.(این آدرس‌ها درست نیستند.)
</div>

### url: armandar.com/api/v1/login --- method: post

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



# Alerts
### url: armandar.com/api/v1/alerts  --- method: get


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

از Url می‌توانید برای ارسال کاربر به صفحه مربوطه که در سامانه موجود است استفاده کنید.
</div>


# Gauges
### url: armandar.com/api/v1/gauges/{year}/{orgtype?}/{page?}/{limit?}/{search?}  --- method: get

<div dir="rtl">
جهت نمایش گیج‌های ابتدای برنامه از این بخش استفاده کنید.
</div>

## year (required) {gauges}

<div dir="rtl">
سال جاری که کاربر در بخش تنظیمات مشخص نموده‌است با این درخواست و به عنوان پارامتر اول ارسال شود.
</div>

## orgtype (optional) {gauges}

<div dir="rtl">
نوع سازمان برای دریافت اطلاعات آن از طریق این پارامتر مقدار دهید می‌گردد. به صورت پیش‌فرض مقدار University دارد و نیاز به ارسال وجود ندارد ولی اگر نیاز به ست کردن آن برای دسترسی به پارامترهای بعدی را دارید به صورت دستی از همین مقدار University استفاده کنید.
</div>

default: University

## page (optional) {gauges}

<div dir="rtl">
با توجه به اینکه میزان اطلاعات ممکن است زیاد شود و هم زمان لود طول بکشد و هم UI از زیبایی خارج شود اطلاعات به صورت صفحه به صفحه می‌اید. این پارامتر شماره صفحه را برای دریافت اطلاعات آن صفحه مشخص می‌کند.
</div>

default:1

## limit (optional) {gauges}

<div dir="rtl">
تعداد رکوردهای مربوط به هر صفحه را نمایش می‌دهد. می‌توانید مشخص کنید که در هربار واکشی اطلاعات چه تعداد رکورد را برای شما بیاورد.
</div>

default: 10

## search (optional) {gauges}

<div dir="rtl">
برای جستجوی عبارت خاص در رکوردها از این پارامتر استفاده کنید. این پارامتر جهت استفاده در بخش‌های مختلف جستجو در دسترس است و در آدرس‌های مختلف به همین منظور قرار داده‌شده‌است.
</div>

default: ""

## Sample  {gauges}

<div dir="rtl">
نمونه نحوه ارسال درخواست با OkHttpClient در جاوا
</div>

```java
OkHttpClient client = new OkHttpClient();

Request request = new Request.Builder()
  .url("http://armandar.com/api/v1/gauges/1395/Univertsity/1/10/گیلان")
  .get()
  .addHeader("authorization", "Bearer gyXOAl0G4lg5LQYDa....")
  .addHeader("cache-control", "no-cache")
  .build();

Response response = client.newCall(request).execute();
```


<div dir="rtl">
و نتیجه دریافتی به صورت زیر خواهد بود.
</div>

```json
[
    {
        "Value": 40.66,
        "ScheduleValue": 97.5,
        "YearId": 1395,
        "DeviationFactor": -56.84,
        "OldScheduleValue": 0,
        "HeadOrganizationChartId": 69,
        "Title": "گیلان"
    }
]
```

Title: عنوان

Value: پیشرفت واقعی

ScheduleValue: پیشرفت برنامه‌ای

DeviationFactor: میرزان انحراف


<div dir="rtl">
بقیه اطلاعات نیز در حال حاضر مورد نیاز نیست و جایی نمایش داده نمی‌شود.
</div>



# Projects
### url: armandar.com/api/v1/projects/{year}/{page?}/{limit?}/{search?}  --- method: get

<div dir="rtl">
جهت نمایش پروژه‌ها از این بخش استفاده کنید.
</div>


## year (required) {projects}

<div dir="rtl">
سال جاری که کاربر در بخش تنظیمات مشخص نموده‌است با این درخواست و به عنوان پارامتر اول ارسال شود.
</div>

## page (optional) {projects}

<div dir="rtl">
با توجه به اینکه میزان اطلاعات ممکن است زیاد شود و هم زمان لود طول بکشد و هم UI از زیبایی خارج شود اطلاعات به صورت صفحه به صفحه می‌اید. این پارامتر شماره صفحه را برای دریافت اطلاعات آن صفحه مشخص می‌کند.
</div>

default:1

## limit (optional) {projects}

<div dir="rtl">
تعداد رکوردهای مربوط به هر صفحه را نمایش می‌دهد. می‌توانید مشخص کنید که در هربار واکشی اطلاعات چه تعداد رکورد را برای شما بیاورد.
</div>

default: 10

## search (optional) {projects}

<div dir="rtl">
برای جستجوی عبارت خاص در رکوردها از این پارامتر استفاده کنید. این پارامتر جهت استفاده در بخش‌های مختلف جستجو در دسترس است و در آدرس‌های مختلف به همین منظور قرار داده‌شده‌است.
</div>

default: ""

## Sample  {projects}

<div dir="rtl">
نمونه نحوه ارسال درخواست با OkHttpClient در جاوا
</div>

```java
OkHttpClient client = new OkHttpClient();

Request request = new Request.Builder()
  .url("http://armandar.com/api/v1/projects/1395/1/10/گیلان")
  .get()
  .addHeader("authorization", "Bearer gyXOAl0G4lg5LQYDa....")
  .addHeader("cache-control", "no-cache")
  .build();

Response response = client.newCall(request).execute();
```


<div dir="rtl">
و نتیجه دریافتی به صورت زیر خواهد بود.
</div>

```json
[
    {
        "Id": 2317,
        "Code": "P95-002317",
        "Title": "تست ۱",
        "OrganizationChartId": 690809,
        "OrganizationChartTitle": "گیلان",
        "StatusId": 2,
        "StatusTitle": "در حال انجام",
        "ScheduleValue": 98.76,
        "Value": 86,
        "YearId": 1395,
        "DeviationFactor": -12.76
    },
    {
        "Id": 2371,
        "Code": "P95-002371",
        "Title": "تست ۲",
        "OrganizationChartId": 690809,
        "OrganizationChartTitle": "گیلان",
        "StatusId": 2,
        "StatusTitle": "در حال انجام",
        "ScheduleValue": 99.75,
        "Value": 60,
        "YearId": 1395,
        "DeviationFactor": -39.75
    },...
]
```

Title: عنوان

Code: کد (حتماً کد را هم نمایش دهید)

OrganizationChartTitle: نام دانشگاه یا واحد

Value: پیشرفت واقعی

ScheduleValue: پیشرفت برنامه‌ای

DeviationFactor: میرزان انحراف

StatusTitle: وضعیت


<div dir="rtl">
بقیه اطلاعات نیز در حال حاضر مورد نیاز نیست و جایی نمایش داده نمی‌شود.
</div>




# Project Steps
### url: armandar.com/api/v1/steps/{project}/{search?}  --- method: get

<div dir="rtl">
جهت نمایش فعالیت‌های یک پروژه وفتی روی آن کلیک می‌شود از این بخش استفاده کنید. شناسه پروژه برای دریافت اطلاعات باید ارسال شود. در این متد ما به سال نیاز نداریم

با توجه به اینکه تعداد فعالیت‌ها معمولا خیلی زیاد نیست در این بخش ما صفحه‌بندی نداریم و تمام اطلاعات با یک درخواست قابل دریافت است.

</div>

>  با توجه به اینکه فعالیت‌ها ساختار درختی دارند به جیسان دریافتی دقت نموده و برای نمایش با ساختاری مشابه درختی تدبیری بیندیشید.



## project (required) {steps}

<div dir="rtl">
شناسه پروژه‌ای که کاربر انتخاب نموده است با استفاده از پارامتر اول ارسال شود.
</div>


## search (optional) {steps}

<div dir="rtl">
برای جستجوی عبارت خاص در رکوردها از این پارامتر استفاده کنید. این پارامتر جهت استفاده در بخش‌های مختلف جستجو در دسترس است و در آدرس‌های مختلف به همین منظور قرار داده‌شده‌است.
</div>

default: ""

## Sample  {steps}

<div dir="rtl">
نمونه نحوه ارسال درخواست با OkHttpClient در جاوا
</div>

```java
OkHttpClient client = new OkHttpClient();

Request request = new Request.Builder()
  .url("http://armandar.com/api/v1/steps/642")
  .get()
  .addHeader("authorization", "Bearer gyXOAl0G4lg5LQYDa....")
  .addHeader("cache-control", "no-cache")
  .build();

Response response = client.newCall(request).execute();
```


<div dir="rtl">
و نتیجه دریافتی به صورت زیر خواهد بود.
</div>

```json
[
    {
        "Id": 3105,
        "ProjectId": 642,
        "Title": "بررسی وضعیت موجود و تعداد نیروی انسانی شاغل",
        "WeightFactor": 20,
        "ParentId": null,
        "Level": 1,
        "Value": 90,
        "ScheduleValue": 0,
        "DeviationFactor": 0
    },
    {
        "Id": 31272,
        "ProjectId": 642,
        "Title": "تست1",
        "WeightFactor": 100,
        "ParentId": 3105,
        "Level": 2,
        "Value": 0,
        "ScheduleValue": 0,
        "DeviationFactor": 0
    },
    {
        "Id": 3106,
        "ProjectId": 642,
        "Title": "استخراج آخرین استانداردهای نیروی انسانی",
        "WeightFactor": 40,
        "ParentId": null,
        "Level": 1,
        "Value": 75,
        "ScheduleValue": 0,
        "DeviationFactor": 0
    },
    {
        "Id": 3103,
        "ProjectId": 642,
        "Title": "بررسی و مقایسه وضعیت موجود با استانداردها",
        "WeightFactor": 20,
        "ParentId": null,
        "Level": 1,
        "Value": 85,
        "ScheduleValue": 0,
        "DeviationFactor": 0
    },
    {
        "Id": 3108,
        "ProjectId": 642,
        "Title": "ارائه راه حل برای جبران کمبودها",
        "WeightFactor": 20,
        "ParentId": null,
        "Level": 1,
        "Value": 40,
        "ScheduleValue": 0,
        "DeviationFactor": 0
    },
    {
        "Id": 31273,
        "ProjectId": 642,
        "Title": "ururt",
        "WeightFactor": 100,
        "ParentId": 3108,
        "Level": 2,
        "Value": 0,
        "ScheduleValue": 0,
        "DeviationFactor": 0
    },
    {
        "Id": 31274,
        "ProjectId": 642,
        "Title": "ururt",
        "WeightFactor": 80,
        "ParentId": 31273,
        "Level": 3,
        "Value": 80,
        "ScheduleValue": 0,
        "DeviationFactor": 0
    },
    {
        "Id": 31275,
        "ProjectId": 642,
        "Title": "تست1",
        "WeightFactor": 20,
        "ParentId": 31273,
        "Level": 3,
        "Value": 80,
        "ScheduleValue": 0,
        "DeviationFactor": 0
    }
]
```

Title: عنوان

Value: پیشرفت

Level: سطح


<div dir="rtl">
بقیه اطلاعات نیز در حال حاضر مورد نیاز نیست و جایی نمایش داده نمی‌شود.


مقدار Level سطح تو رفتگی را در درخت نمایش خواهد داد.
</div>


# Actions
### url: armandar.com/api/v1/actions/{year}/{page?}/{limit?}/{search?}  --- method: get

<div dir="rtl">
برای نمایش لیست اقدامات جاری کاربر از این متد استفاده کنید.
</div>


## year (required) {actions}

<div dir="rtl">
سال جاری که کاربر در بخش تنظیمات مشخص نموده‌است با این درخواست و به عنوان پارامتر اول ارسال شود.
</div>

## page (optional) {actions}

<div dir="rtl">
با توجه به اینکه میزان اطلاعات ممکن است زیاد شود و هم زمان لود طول بکشد و هم UI از زیبایی خارج شود اطلاعات به صورت صفحه به صفحه می‌اید. این پارامتر شماره صفحه را برای دریافت اطلاعات آن صفحه مشخص می‌کند.
</div>

default:1

## limit (optional) {actions}

<div dir="rtl">
تعداد رکوردهای مربوط به هر صفحه را نمایش می‌دهد. می‌توانید مشخص کنید که در هربار واکشی اطلاعات چه تعداد رکورد را برای شما بیاورد.
</div>

default: 10

## search (optional) {actions}

<div dir="rtl">
برای جستجوی عبارت خاص در رکوردها از این پارامتر استفاده کنید. این پارامتر جهت استفاده در بخش‌های مختلف جستجو در دسترس است و در آدرس‌های مختلف به همین منظور قرار داده‌شده‌است.
</div>

default: ""


## Sample  {actions}

<div dir="rtl">
نمونه نحوه ارسال درخواست با OkHttpClient در جاوا
</div>

```java
OkHttpClient client = new OkHttpClient();

Request request = new Request.Builder()
  .url("http://armandar.com/api/v1/actions/1395")
  .get()
  .addHeader("authorization", "Bearer gyXOAl0G4lg5LQYDa....")
  .addHeader("cache-control", "no-cache")
  .build();

Response response = client.newCall(request).execute();
```


<div dir="rtl">
و نتیجه دریافتی به صورت زیر خواهد بود.
</div>

```json
[
  {
    "Id": 2366,
    "Title": "تهیه گزارش‌های ماهانه سال 95",
    "Code": "A95-002366",
    "YearId": 1395,
    "OrganizationChartTitle": "معاونت توسعه مدیریت و منابع ",
    "Value": 36.84,
    "ScheduleValue": 92.62
  },
  {
    "Id": 2707,
    "Title": "تهیه و انتشار ماهنامه تست",
    "Code": "A95-002707",
    "YearId": 1395,
    "OrganizationChartTitle": "دانشگاه تهران",
    "Value": 62.5,
    "ScheduleValue": 90.83
  }
]
```

Title: عنوان

Code: کد (حتماً نمایش داده شود.)

OrganizationChartTitle: نام دانشگاه یا واحد

Value: پیشرفت

ScheduleValue: پیشرفت برنامه‌ای

<div dir="rtl">
بقیه اطلاعات نیز در حال حاضر مورد نیاز نیست و جایی نمایش داده نمی‌شود.
</div>

<div dir="rtl">
</div>