# تکرار

**[شما می‌توانید کدهای این بخش را اینجا ببینید](https://github.com/quii/learn-go-with-tests/tree/main/for)**

برای انجام کارهای تکراری در گو شما از `for` استفاده می‌کنید، در گو عبارات کلیدی `while`، `do`، و `until` وجود ندارد. تنها ابزار شما `for` می‌باشد که چیز خوبیست.

بیایید تابعی بنویسیم که یک حرف را پنج بار تکرار می‌کند.

چیز جدیدی در ایت زمینه وجود ندارد پس تلاش کنید خودتان بنویسید.

## ابتدا تست را می‌نویسیم

```go
package iteration

import "testing"

func TestRepeat(t *testing.T) {
	repeated := Repeat("a")
	expected := "aaaaa"

	if repeated != expected {
		t.Errorf("expected %q but got %q", expected, repeated)
	}
}
```

## تلاش می‌کنیم تست را اجرا کنیم

`./repeat_test.go:6:14: undefined: Repeat`

## کمترین میزان کد برای اجرای تست را می‌نویسیم که خطایی که تستمان می‌دهد را ببینیم

مراحل را به ترتیب انجام دهید شما چیز جدیدی لازم نیست بدانید که کاری کنید تست خطا بدهد.

تمام چیزی که لازم هست مقدار کافی کد هست که باعث کامپایل شدن تست بشود اما باعث پاس شدن آن نشود.

```go
package iteration

func Repeat(character string) string {
	return ""
}
```
خوب نیست که می‌دانید برای مسائل پایه‌ای چگونه تست گو بنویسید؟ این یعنی شما حالا می‌توانیدهرچقدر که می‌خواهید با پروداکشن کار کنید و خیالتان راحت باشد که همه چیز درست است یا نه.

`repeat_test.go:10: expected 'aaaaa' but got ''`

## به اندازه‌ی کافی کد بنویسید که پاس شود

سینتکس `for` به شدت شبیه زبان سی می‌باشد و چیز زیادی ندارد.

```go
func Repeat(character string) string {
	var repeated string
	for i := 0; i < 5; i++ {
		repeated = repeated + character
	}
	return repeated
}
```
برخلاف زبان‌های دیگر همچون سی، جاوا، و جاوااسکریپت، برای حلقه‌ نیازی به پرانتز نیست و گذاشتن کرلی براکت `{}` الزامی هست. شاید برایتان سوال باشد که خط پایین یعنی چه


```go
	var repeated string
```
قبلا ما برای ساخت یک متغیر از `:=` استفاده می‌کردیم که ابزاری برای ساختن و مقداردهی به یک متغیر بود و [دو کار را با هم انجام می‌داد](https://gobyexample.com/variables). در خط بالا ما تنها متغیر را می‌سازیم و به آن مقدار نمی‌دهیم. از `var` برای ساخت تابع هم می‌توان استفاده کرد که بعدا می‌بینیم.

تست را اجرا کنید الان باید پاس شود.

روش استفاده از for به شکل مفصل [اینجا](https://gobyexample.com/for) توضیح داده شده.

## ری‌فکتور

حالا زمان ری‌فکتور و معرفی یک اپراتور جدید است، `=+` .

```go
const repeatCount = 5

func Repeat(character string) string {
	var repeated string
	for i := 0; i < repeatCount; i++ {
		repeated += character
	}
	return repeated
}
```

`=+` که متغیر اضافه کردن و مقداردهی است. کار آن این است که مقدار سمت راست اپراتور را با مقدار سمت چپ جمع کند و پاسخ را در متغیر سمت چپ بریزد. این با انواع دیگری همچون اعداد صحیح هم کار می‌کند.

### محک

نوشتن [محک](https://golang.org/pkg/testing/#hdr-Benchmarks) یکی دیگر از ویژگی‌های مهم گو هست و همچون تست نوشتن می‌ماند.

```go
func BenchmarkRepeat(b *testing.B) {
	for i := 0; i < b.N; i++ {
		Repeat("a")
	}
}
```

همانطور که می‌بینید محک‌نویسی مثل تست‌نویسی می‌ماند.

The `testing.B` gives you access to the cryptically named `b.N`.

When the benchmark code is executed, it runs `b.N` times and measures how long it takes.

The amount of times the code is run shouldn't matter to you, the framework will determine what is a "good" value for that to let you have some decent results.

To run the benchmarks do `go test -bench=.` (or if you're in Windows Powershell `go test -bench="."`)

```text
goos: darwin
goarch: amd64
pkg: github.com/quii/learn-go-with-tests/for/v4
10000000           136 ns/op
PASS
```

What `136 ns/op` means is our function takes on average 136 nanoseconds to run \(on my computer\). Which is pretty ok! To test this it ran it 10000000 times.

_NOTE_ by default Benchmarks are run sequentially.

## Practice exercises

* Change the test so a caller can specify how many times the character is repeated and then fix the code
* Write `ExampleRepeat` to document your function
* Have a look through the [strings](https://golang.org/pkg/strings) package. Find functions you think could be useful and experiment with them by writing tests like we have here. Investing time learning the standard library will really pay off over time.

## Wrapping up

* More TDD practice
* Learned `for`
* Learned how to write benchmarks
