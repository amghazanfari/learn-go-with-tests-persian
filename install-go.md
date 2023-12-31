# نصب گو

آموزش رسمی نصب گو در [اینجا](https://golang.org/doc/install) موجود است.

## محیط گو

### ماژول‌های گو
گو در نسخه‌ی ۱.۱۱ [ماژول](https://github.com/golang/go/wiki/Modules) را معرفی کرد. از نسخه‌ی ۱.۱۶ این روش پیش‌فرض گو برای بیلد پروژه‌ها است پس بنابراین استفاده از `GOPATH` توصیه نمی‌شود.

ماژول‌ها برای حل مشکلات مربوط به وابستگی‌ها، انتخاب ورژن، و امکان بیلد در محیط‌های مختلف استفاده می‌شوند؛ همچنین آن‌ها این امکان را فراهم می‌کنند که کد خارج از `GOPATH` اجرا شود.

استفاده از ماژول بسیار ساده است، تنها کافیست یک دایرکتوری خارج از `GOPATH` را به عنوان روت پروژه انتخاب کنید، و با دستور `go mod init` یک ماژول جدید بسازید.

با زدن این دستور فایل `go.mod` ساخته می‌شود که شامل مسیر ماژول، ورژن گو، و ماژول‌های مورد نیاز برای اجرای ماژول مورد نظر است.

اگر مسیری برای ماژول مشخص نشود خود گو تلاش می‌کند با مسیر فعلی پروژه مسیر آن را تعریف کند همچنین می‌توانیم با وارد کردن یک آرگومان مسیر ماژول را مشخص کنیم.

```sh
mkdir my-project
cd my-project
go mod init <modulepath>
```
فایل `go.mod` می‌تواند اینگونه باشد:

```
module cmd

go 1.16

```
شما می‌توانید با زدن دستورات زیر ببینید چه دستوراتی برای `go mod` وجود دارد. 


```sh
go help mod
go help mod init
```

## پیدا کردن مشکلات دستوری گو

برای آنکه بتوانید مشکلات دستوری گو را پیدا کنید می‌توانید از  [GolangCI-Lint](https://golangci-lint.run). استفاده کنید.

برای تصب آن دستور زیر را وارد کنید:

```sh
brew install golangci-lint
```

## ری‌فکتور کردن و ابزارهای شما

یکی از اهداف این کتاب نشان دادن اهمیت ری‌فکتور می‌باشد.

ابزارهای شما می‌تواند به شما کمک کنند تا با خیال راحت‌تری ری‌فکتور کنید.

شما باید به قدری با ادیتور خود آشنا باشید که دستورات زیر را به راحتی وارد کنیپ:


- **پیدا کردن متغیرها**. شما باید یتوانید یک متغیر را به راحتی پیدا کنید و ببینید چگونه تعریف شده و چخ کارهایی با آن می‌شود.
- **پیدا کردن توابع**. شما باید بتوانید یک تابع را پیدا کنید تا بفهمید کجاها استفاده می‌شود و چگونه تعریف شده.
- **تعییر نام**. شما باید بتوانید به راحتی نام هر چیزی که خواستید را تعییر بدهید.
- **فرمت گو**. گو دستور `go fmt`. را دارد که می‌تواند فرمت کدنویسی شما در گو را تصحیح کند. ادیتور شما باید بتواند بعد از هر بار ذخیره‌ی فایل این دستور را اجرا کند..
- **اجرای تست‌ها**. شما باید قادر باشید بعد از انجام هر کدام از موارد بالا به سرعت تست‌های خود را اجرا کنید تا مطمئن باشید ری‌فکتور کردن کد شما را خراب نکرده است.

علاوه‌بر موارد بالا شما باید بتوانید کارهای زیر را هم انجام دهید.

- **دیدن امضای تابع**. شما باید ببینید که یک تابع را چگونه صدا بزنید و تابع چه متغیر یا متغیرهایی را برای شما برمی‌گرداند.
- **دیدن تعریف تابع**. اگر نمی‌دانید یک تابع چه کار می‌کند شما باید بتوانید به محل تعریف تابع بروید و کد را بخوانید.
- **فهمیدن فایده‌ی یک جز**. دیدن نحوه‌ی فراخوانی تابع می‌تواند به شما کمک کند که برای نحوه‌ی ری‌فکتور آن تصمیم گیری کنید.

داشتن مهارت در استفاده از ابزار به شما کمک می‌کند روی کارتان تمرکز کنید، و لازم نباشد کار با ابزار را یاد بگیرید.

## جمع‌بندی

تا به اینجا شما باید گو را نصب کرده باشید، یک ادیتور داشته باشید، و اگر می‌خواهید یک سری ابزار کمکی را نصب کرده باشید. گو ابزارهای فوق‌العاده‌ی زیادی دارد که می‌توانید یک سری از آن‌ها را در [https://awesome-go.com](https://awesome-go.com) ببینید.
