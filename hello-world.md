# سلام دنیا

**[شما می‌توانید کدهای این بخش را اینجا ببینید](https://github.com/quii/learn-go-with-tests/tree/main/hello-world)**

یک رسم قدیمی است که اولین مسئله‌ی برنامه‌نویسی در یک زبان [Hello, World یا سلام‌ دنیا](https://en.m.wikipedia.org/wiki/%22Hello,_World!%22_program) باشد.

- هر جا که می‌خواهید یک فولدر بسازید
- فایل `hello.go` را ایجاد کنید و محتوای زیر را در آن بنویسید

```go
package main

import "fmt"

func main() {
	fmt.Println("Hello, world")
}
```

برای اجرای آن دستور  `go run hello.go` را بزنید.

## نحوه‌ی کار

زمانی که شما یک کد گو می‌نویسید، شما یک بسته‌ی `main` دارید که در آن تابع `main` تعریف شده است. شما می‌توانید کدهای مرتبط به هر بخش را در بسته‌ی خاص خود بگذارید.

برای تعریف تابع شما از کلمه‌ی کلیدی `func` باید استفاده کنید و بعد از آن نام تابع را بنویسید.

با دستور `import "fmt"` ما می‌توانیم از یک بسته که دارای تابع`Println` هست استفاده کنیم.

## چگونه تست کنیم

چگونه جنین چیزی را می‌توان تست کرد؟ خوب است که کدهای «دامنه» را از دنیای بیرون جدا کرد. `fmt.Println` مربوط به دامنه‌ی شما نیست. اما رشته‌ای که می‌فرستیم جزو دامنه‌ی کد ما هست.

پس می‌توان این دو را از هم جدا کرد.


```go
package main

import "fmt"

func Hello() string {
	return "Hello, world"
}

func main() {
	fmt.Println(Hello())
}
```
ما دوباره یک تابع جدید ساختیم اما این بار پس از تعریف تابع از کلمه‌ی کلیدی `string` استفاده کردیم که یعنی وظیفه‌ی تابع بازگرداندن یک رشته است.

حال یک فایل جدید با نام `hello_test.go` می‌سازیم که در آن تست‌های مربوط به تابغ `Hello` را می‌نویسیم.


```go
package main

import "testing"

func TestHello(t *testing.T) {
	got := Hello()
	want := "Hello, world"

	if got != want {
		t.Errorf("got %q want %q", got, want)
	}
}
```

## ماژول‌های گو؟

گام بعدی اجرای تست است. دستور `go test` را در ترمینال بزنید. اگر تست‌ها پاس شد احتمالا دارید از نسخه‌های قدیمی‌تر گو استفاده می‌کنید. اگر از نسخه‌ی ۱.۱۶ یا جدیدتر استفاده می‌کنید پس احتمالا کد شما اصلا اجرا نمی‌شود، و شما چنین خطابب در ترمینال می‌بینید:


```shell
$ go test
go: cannot find main module; see 'go help modules'
```

مشکل چیست? اگر بخواهیم در یک کلمه مشکل را بگوییم، مشکل, [ماژول‌ها](https://blog.golang.org/go116-module-changes) هستند. خوشبحتانه راه حل آن ساده است. دستور `go mod init hello` را در ترمینال وارد کنید. این دستور فایلی با محتوای زیر برای شما تولید می‌کند:

```
module hello

go 1.16
```
این فایل به `go` اطلاعات اساسی مربوط به کد شما را می‌دهد. اگر تصمیم دارید برنامه‌ی خود را به دیگران بدهید، شما هم باید بگویید که کد را از کجا بگیرد، هم اینکه این کد چه نیازمندی‌هایی برای اجرا دارد. در حال حاضر ماژول شما حداقل‌ها را دارد، و فعلا می‌تواند اینگونه باشد. برای آنکه اطلاعات بیشتری درباره‌ی ماژول داشته باشید [می‌توانید به مستندات گو در مورد ماژول مراجعه کنید](https://golang.org/doc/modules/gomod-ref). حالا که تست می‌تواند اجرا شود به سراغ ادامه‌ی کار می‌رویم.

در بخش‌های بعدی بخاطر داشته باشید فبل از دستورات `go test` و `go build` باید ابتدا دستور `go mod init SOMENAME‍` را بزنید تا ماژول ساخته شود.


## بازگشت به تست

حالا اگر `go test` را بزنید تست شما باید موفق باشد، برای اینکه مطمئن‌تر باشید، می‌توانید رشته‌ی موجود در `want` را تغییر دهید؛ تست باید خطا بدهد.

اگر متوجه شده باشید ما نیازی به نصب فریمورک برای تست کدمان نداریم، در گو خود زبان امکان تست را برای شما فراهم کرده و با همون دستور زبان گو می‌توان تست نوشت.

### نوشتن تست

نوشتن تست مانند نوشتن تابع هست، فقط باید چند شرط را رعایت کرد.

* نام فایلی که تست در آن نوشته می‌شود باید به شکل `xxx_test.go` باشد
* نام تابع تست باید با   `Test` شروع شود
* تابع تست تنها یک آرگومان می‌گیرد و آن  `t *testing.T` است
* برای استفاده از `*testing.T` شما نیاز دارید با زدن `import testing`, کتابخانه‌ی مربوط به تست را در کد خود ایمپورت کنید.

فعلا کافیست بدانید که `t` که از نوع `*testing.T` بود درواقع یک رابط برای صحبت با فریمورک تست هست و می‌توان دستوراتی همچون `()t.Fail` را وارد کرد.


ما یک سری دستورات جدید را دیدیم:

#### `دستور if`
دستور `if` در زبان گو مانند همین دستور در دیگر زبان‌ها می‌شد
#### تعریف متغیر

ما با دستور `varName := value` یک متغیر جدید تعریف می‌کنیم که به ما اجازه می‌دهد از یک سری مغادیر چندن بار استفاده کنیم تا خوانایی کد بالا برود.


#### `دستور t.Errorf`

ما متد `Errorf` را که برای `t` تعریف شده صدا می‌زنیم تا به وسیله‌ی آن اعلام کنیم که تست ما موفق نبوده. حرف `f` از کلمه‌ی فرمت گرفته شده که به ما اجازه می‌دهد یک رشته داشته باشیم که به جای `%q` مقدار متغیر را در آن بگذاریم، این باعث می‌شود متن خطای ما خوانا باشد، تا در صورت داشتن خطا مشکل را سریع‌تر بفهمیم.

 شما می‌توانید در مورد این مدل کار با رشته در [مستندات گو](https://golang.org/pkg/fmt/#hdr-Printing) بیشتر بخوانید. برای تست استفاده از `%q` بسیار مناسب است چرا که مقدار متغبر را داخل دابل کوتیشن می‌گذارد.

ما جلوتر به تفاوت تابع و متد می‌پردازیم.

### مستندات گو

یکی دیگر از ویژگی‌های ممتاز گو مستندات آن هست شما می‌توانید با زدن دستور `godoc -http :8000` مستندات گو را در سیستم خود داشته باشید. اگر به آدرس [localhost:8000/pkg](http://localhost:8000/pkg) بروید شما تمام بسته‌های نصب شده روی سیستم خود را می‌بینید.

بیشتر کتابخانه‌های استاندارد گو مستندات عالی‌ای دارند که همراه مثال هست. بد نیست به آدرس [http://localhost:8000/pkg/testing/](http://localhost:8000/pkg/testing/)  بروید و در مستندات مربوط به کتابخانه‌ی تست چرخی بزنید.

اگر در سیستمتان دستور `godoc` را ندارید احتمالا بخاطر آن است که از نسخه‌های جدیدتر گو استفاده می‌کنید. شما می‌توانید با زدن دستور `go install golang.org/x/tools/cmd/godoc@latest` برنامه‌ی نشان دادن مستندات را نصب کنید.

### سلام بر تو

جالا که تست ما کار می‌کند می‌توانیم خیالمان از بابت امنیت کدمان راحت باشد.

در آخرین مثالمان ما تست را بعد از نوشتن کد اصلی  نوشتیم، تا نگاهی داشته باشیم به چگونگی کارکرد تست. از اینجا به بعد ما تست را قبل از نوشتن کد تابع اصلی می‌نویسیم.

در گام بعدی می‌بینیم که چگونه نام شخص را موقع سلام کردن مشخص کنیم.

بیایید ابتدا نیازمندی خود را در تست مشخص کنیم. این یک برنامه‌نویس تست محور مقدماتی هست و به ما اجازه می‌دهد تا مطمئن شویم تست ما واقعا چیزی که ما می‌خواهیم را تست می‌کند. گاهی اوقات هنگام کد نوشتن تست شما حتا اگر با خطا هم مواجه باشد موفق است، در این مواقع شما به درستی تست نمی‌کنید. باید مطمئن شوید که تستتان در صورت وجود مشکل خطا بدهد.

```go
package main

import "testing"

func TestHello(t *testing.T) {
	got := Hello("Chris")
	want := "Hello, Chris"

	if got != want {
		t.Errorf("got %q want %q", got, want)
	}
}
```
حال دستور `go test` را بزنید شما باید خطای زمان کامپایل بگیرید

```text
./hello_test.go:6:18: too many arguments in call to Hello
    have (string)
    want ()
```

وقتی با یک زبان برنامه‌نویسی ایستا (Statically typed programming languages) مانند گو سروکار دارید، بهتر است به حرف کامپایلر گوش کنید، در این زیان‌ها کامپایلر می‌داند کد چگونه کار می‌کند تا شما مجبور نباشید آن را بدانید.

در اینجا کامپایلر به شما می‌گوید نیاز دارید چه تغییری بدهید تا کد درست کار کند، ما باید تابع `Hello` را تغییر دهیم تا یک آرگومان بگیرد.


تابع `Hello` را به شکل زیر تغییر دهید تا یک آرگومان بگیرد.

```go
func Hello(name string) string {
	return "Hello, world"
}
```

اگر دوباره تست خود را اجرا کنید خطا می‌گیرید چرا که هنگام صدا زدن تابع `Hello` باید یک آرگومان هم وارد کنید.

```go
func main() {
	fmt.Println(Hello("world"))
}
```

حالا موقع اجرای تست چنین پیامی باید ببینید
```text
hello_test.go:10: got 'Hello, world' want 'Hello, Chris''
```

بالاخره کد ما قابل تست شد اما باز هم تست موفقیت‌آمیز نبود.

حال وقت آن است که با تغییر تابع `Hello` کاری کنیم که نتیجه‌ی مقبول ما را بدهد.

```go
func Hello(name string) string {
	return "Hello, " + name
}
```

حالا وقتی تست را اجرا کنیم تست با موفقیت پاس می‌شود. براساس چرخه‌ی برنامه‌نویسی تست محور حالا وقت ری‌فکتور می‌باشد.

### بادداشتی برای استفاده از سورس کنترل

در این نقطه اگر از یک سورس کنترل استفاده می‌کنید(که باید بکنید) بهتر است کد خود را `commit` کنید چرا که در این نقطه ما یک نرم‌افزار قابل اجرا داریم که تست هم برای آن نوشته شده.

البته من بنا ندارم کد را به مخزن بفرستم چراکه می‌خواهم آن را ری‌فکتور کنم. ولی بهتر است تغییرات را کامیت کنید که اگر هنگام ری‌فکتور به مشکل خوردید به راحتی به ورژن موفق قبلی برگردید.

چیز خیلی زیادی برای زی‌فکتور کردن نیست اما بد نیست اینجا با مفهوم ثابت‌ها آشنا شوید.

### ثابت‌ها

ثابت‌ها مانند زیر تعریف می‌شوند.

```go
const englishHelloPrefix = "Hello, "
```

حالا ما می‌توانیم کد خود را ری‌فکتور کنیم

```go
const englishHelloPrefix = "Hello, "

func Hello(name string) string {
	return englishHelloPrefix + name
}
```

بعد از ری‌فکتور کردن یک بار دیگر تست‌ها را اجرا کنید تا مطمئن شوید چیزی خراب نشده باشد.

خوب است کمی درباره‌ی ساختن ثابت فکر کنید تا کاربرد آن در برنامه و حتا پرفورمنس را بهتر درک کنید.

## سلام دنیا...دوباره

خوب است در گام بعدی کاری کنیم که اگر یک رشته‌ی خالی به کد دادیم به ما «Hello, World» تحویل دهد نه «Hello, »

کارمان را با نوشتن تست جدید شروع می‌کنیم

```go
func TestHello(t *testing.T) {
	t.Run("saying hello to people", func(t *testing.T) {
		got := Hello("Chris")
		want := "Hello, Chris"

		if got != want {
			t.Errorf("got %q want %q", got, want)
		}
	})
	t.Run("say 'Hello, World' when an empty string is supplied", func(t *testing.T) {
		got := Hello("")
		want := "Hello, World"

		if got != want {
			t.Errorf("got %q want %q", got, want)
		}
	})
}
```

حالا ما یک مفهوم دیگر را معرفی می‌کنیم، زیر مجموعه‌ها. گاهی حوب است که تست‌هایمان را حول یک چیز گروه‌بندی کنیم و بعد یک زیرمجموعه داشته باشیم که سناریوهای متقاوت از آن چیز را تست کند.

خوبی این روش این است که شما می‌توانید یک بخش از کد را به اشتراک بگذارید تا در دیگر تست‌ها از آن استفاده شود.

حالا بیایید با استفاده از `if` کاری کنیم تستمان درست کار کند.


```go
const englishHelloPrefix = "Hello, "

func Hello(name string) string {
	if name == "" {
		name = "World"
	}
	return englishHelloPrefix + name
}
```
حالا اگر تست‌های خود را اجرا کنیم باید ببینیم که تست‌ها موفق هستند، و چیزی خراب نشده.

مهم هست که تست‌های شما به شکل شفاف هر آنچه مورد نیاز هست را تست کرده باشد. اما این موضوع باعث تکرار کردن در کد می‌شود.

ری‌فکتور تنها برای کد اصلی نیست!

جالا که تست‌ها موفق هستند، خوب است که خود تست‌ها را ری‌فکتور کنیم

```go
func TestHello(t *testing.T) {
	t.Run("saying hello to people", func(t *testing.T) {
		got := Hello("Chris")
		want := "Hello, Chris"
		assertCorrectMessage(t, got, want)
	})

	t.Run("empty string defaults to 'world'", func(t *testing.T) {
		got := Hello("")
		want := "Hello, World"
		assertCorrectMessage(t, got, want)
	})

}

func assertCorrectMessage(t testing.TB, got, want string) {
	t.Helper()
	if got != want {
		t.Errorf("got %q want %q", got, want)
	}
}
```

ما اینجا چه کار کردیم؟

ما بخشی از کد را که چند بار تکرار می‌شد، در یک تابع مجزا گذاشتیم، از این پس هر وقت خواستیم برابری دو رشته برای تست را بسنجیم، این تابع را صدا می‌زنیم.

For helper functions, it's a good idea to accept a `testing.TB` which is an interface that `*testing.T` and `*testing.B` both satisfy, so you can call helper functions from a test, or a benchmark (don't worry if words like "interface" mean nothing to you right now, it will be covered later).

`t.Helper()` is needed to tell the test suite that this method is a helper. By doing this when it fails the line number reported will be in our _function call_ rather than inside our test helper. This will help other developers track down problems easier. If you still don't understand, comment it out, make a test fail and observe the test output. Comments in Go are a great way to add additional information to your code, or in this case, a quick way to tell the compiler to ignore a line. You can comment out the `t.Helper()` code by adding two forward slashes `//` at the beginning of the line. You should see that line turn grey or change to another color than the rest of your code to indicate it's now commented out.

### Back to source control

Now we are happy with the code I would amend the previous commit so we only check in the lovely version of our code with its test.

### Discipline

Let's go over the cycle again

* Write a test
* Make the compiler pass
* Run the test, see that it fails and check the error message is meaningful
* Write enough code to make the test pass
* Refactor

On the face of it this may seem tedious but sticking to the feedback loop is important.

Not only does it ensure that you have _relevant tests_, it helps ensure _you design good software_ by refactoring with the safety of tests.

Seeing the test fail is an important check because it also lets you see what the error message looks like. As a developer it can be very hard to work with a codebase when failing tests do not give a clear idea as to what the problem is.

By ensuring your tests are _fast_ and setting up your tools so that running tests is simple you can get in to a state of flow when writing your code.

By not writing tests you are committing to manually checking your code by running your software which breaks your state of flow and you won't be saving yourself any time, especially in the long run.

## Keep going! More requirements

Goodness me, we have more requirements. We now need to support a second parameter, specifying the language of the greeting. If a language is passed in that we do not recognise, just default to English.

We should be confident that we can use TDD to flesh out this functionality easily!

Write a test for a user passing in Spanish. Add it to the existing suite.

```go
	t.Run("in Spanish", func(t *testing.T) {
		got := Hello("Elodie", "Spanish")
		want := "Hola, Elodie"
		assertCorrectMessage(t, got, want)
	})
```

Remember not to cheat! _Test first_. When you try and run the test, the compiler _should_ complain because you are calling `Hello` with two arguments rather than one.

```text
./hello_test.go:27:19: too many arguments in call to Hello
    have (string, string)
    want (string)
```

Fix the compilation problems by adding another string argument to `Hello`

```go
func Hello(name string, language string) string {
	if name == "" {
		name = "World"
	}
	return englishHelloPrefix + name
}
```

When you try and run the test again it will complain about not passing through enough arguments to `Hello` in your other tests and in `hello.go`

```text
./hello.go:15:19: not enough arguments in call to Hello
    have (string)
    want (string, string)
```

Fix them by passing through empty strings. Now all your tests should compile _and_ pass, apart from our new scenario

```text
hello_test.go:29: got 'Hello, Elodie' want 'Hola, Elodie'
```

We can use `if` here to check the language is equal to "Spanish" and if so change the message

```go
func Hello(name string, language string) string {
	if name == "" {
		name = "World"
	}

	if language == "Spanish" {
		return "Hola, " + name
	}
	return englishHelloPrefix + name
}
```

The tests should now pass.

Now it is time to _refactor_. You should see some problems in the code, "magic" strings, some of which are repeated. Try and refactor it yourself, with every change make sure you re-run the tests to make sure your refactoring isn't breaking anything.

```go
	const spanish = "Spanish"
	const englishHelloPrefix = "Hello, "
	const spanishHelloPrefix = "Hola, "

	func Hello(name string, language string) string {
		if name == "" {
			name = "World"
		}

		if language == spanish {
			return spanishHelloPrefix + name
		}
		return englishHelloPrefix + name
	}
```

### French

* Write a test asserting that if you pass in `"French"` you get `"Bonjour, "`
* See it fail, check the error message is easy to read
* Do the smallest reasonable change in the code

You may have written something that looks roughly like this

```go
func Hello(name string, language string) string {
	if name == "" {
		name = "World"
	}

	if language == spanish {
		return spanishHelloPrefix + name
	}
	if language == french {
		return frenchHelloPrefix + name
	}
	return englishHelloPrefix + name
}
```

## `switch`

When you have lots of `if` statements checking a particular value it is common to use a `switch` statement instead. We can use `switch` to refactor the code to make it easier to read and more extensible if we wish to add more language support later

```go
func Hello(name string, language string) string {
	if name == "" {
		name = "World"
	}

	prefix := englishHelloPrefix

	switch language {
	case "French":
		prefix = frenchHelloPrefix
	case "Spanish":
		prefix = spanishHelloPrefix
	}

	return prefix + name
}
```

Write a test to now include a greeting in the language of your choice and you should see how simple it is to extend our _amazing_ function.

### one...last...refactor?

You could argue that maybe our function is getting a little big. The simplest refactor for this would be to extract out some functionality into another function.

```go

const (
	french  = "French"
	spanish = "Spanish"

	englishHelloPrefix = "Hello, "
	spanishHelloPrefix = "Hola, "
	frenchHelloPrefix  = "Bonjour, "
)

func Hello(name string, language string) string {
	if name == "" {
		name = "World"
	}

	return greetingPrefix(language) + name
}

func greetingPrefix(language string) (prefix string) {
	switch language {
	case french:
		prefix = frenchHelloPrefix
	case spanish:
		prefix = spanishHelloPrefix
	default:
		prefix = englishHelloPrefix
	}
	return
}
```

A few new concepts:

* In our function signature we have made a _named return value_ `(prefix string)`.
* This will create a variable called `prefix` in your function.
  * It will be assigned the "zero" value. This depends on the type, for example `int`s are 0 and for `string`s it is `""`.
    * You can return whatever it's set to by just calling `return` rather than `return prefix`.
  * This will display in the Go Doc for your function so it can make the intent of your code clearer.
* `default` in the switch case will be branched to if none of the other `case` statements match.
* The function name starts with a lowercase letter. In Go, public functions start with a capital letter and private ones start with a lowercase. We don't want the internals of our algorithm to be exposed to the world, so we made this function private.
* Also, we can group constants in a block instead of declaring them each on their own line. It's a good idea to use a line between sets of related constants for readability.

## Wrapping up

Who knew you could get so much out of `Hello, world`?

By now you should have some understanding of:

### Some of Go's syntax around

* Writing tests
* Declaring functions, with arguments and return types
* `if`, `const` and `switch`
* Declaring variables and constants

### The TDD process and _why_ the steps are important

* _Write a failing test and see it fail_ so we know we have written a _relevant_ test for our requirements and seen that it produces an _easy to understand description of the failure_
* Writing the smallest amount of code to make it pass so we know we have working software
* _Then_ refactor, backed with the safety of our tests to ensure we have well-crafted code that is easy to work with

In our case we've gone from `Hello()` to `Hello("name")`, to `Hello("name", "French")` in small, easy to understand steps.

This is of course trivial compared to "real world" software but the principles still stand. TDD is a skill that needs practice to develop, but by breaking problems down into smaller components that you can test, you will have a much easier time writing software.
