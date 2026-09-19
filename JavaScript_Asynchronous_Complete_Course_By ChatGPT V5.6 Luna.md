# آموزش جامع و کامل Asynchronous JavaScript

> نسخه: Full / Expanded
>
> هدف: پوشش کامل و آموزشی تمام مباحثی که در بحث Asynchronous JavaScript مطرح شد؛ از مفاهیم پایه تا Event Loop، Promise، Cancellation، Retry، Concurrency، Queue، Backpressure، Streams، Workers، Testing، Security و معماری Async.

---

## فهرست مطالب

1. مقدمه و مدل اجرای JavaScript
2. Synchronous، Blocking و Non-Blocking
3. Asynchronous Programming
4. `setTimeout` و Timerها
5. Callbackها
6. Callback Hell و مشکلات Callback
7. Promise از پایه تا حرفه‌ای
8. Promise Chaining
9. `async` و `await`
10. مدیریت خطا در Async Code
11. Event Loop
12. Call Stack
13. Web APIs / Host APIs و Runtime
14. Task، Microtask و Job Queue
15. ترتیب اجرای عملیات Async
16. Promise Combinators
17. Sequential، Concurrent و Parallel
18. `fetch` و HTTP به صورت Async
19. Event Listener و Event-driven Programming
20. Browser Runtime در برابر Node.js Runtime
21. Closure در Async Programming
22. Thenable و Promise Resolution
23. Cancellation و `AbortController`
24. Timeout برای عملیات Async
25. Retry
26. Exponential Backoff و Jitter
27. Race Condition
28. Shared State و Data Consistency
29. Ordering و حفظ ترتیب
30. Debounce و Throttle
31. Concurrency Limit
32. Async Queue و Worker Pool
33. Producer / Consumer
34. Backpressure
35. Streams و Async Iteration
36. `for await...of`
37. Top-Level `await`
38. Dynamic `import()`
39. Async Initialization و Cleanup
40. Mutex و Semaphore
41. Web Worker و Worker Threads
42. Memory و Performance
43. Observability، Logging و Metrics
44. Testing کد Async
45. Debugging کد Async
46. Security در Async Applications
47. Anti-Patterns رایج
48. Structured Concurrency
49. معماری واقعی Async Application
50. پروژه نهایی: Async Data Platform
51. تمرین‌های مرحله‌ای
52. چک‌لیست تسلط
53. مسیر پیشنهادی یادگیری

---

# 1. مقدمه و مدل اجرای JavaScript

JavaScript زبانی است که در محیط‌های مختلف مانند Browser، Node.js، Deno و Runtimeهای دیگر اجرا می‌شود. خود زبان JavaScript مجموعه‌ای از قابلیت‌های زبان را تعریف می‌کند، اما قابلیت‌هایی مانند Timer، شبکه، فایل، DOM و Worker توسط Runtime/Host فراهم می‌شوند.

یکی از مهم‌ترین نکات این است که:

> Asynchronous بودن JavaScript به معنی این نیست که همه چیز هم‌زمان و موازی اجرا می‌شود.

باید بین این مفاهیم تفاوت بگذاریم:

- Synchronous
- Asynchronous
- Blocking
- Non-Blocking
- Concurrent
- Parallel
- Event-driven

---

# 2. Synchronous، Blocking و Non-Blocking

## 2.1 Synchronous

در اجرای Synchronous، دستورات به ترتیب پیش می‌روند.

```js
console.log("A");
console.log("B");
console.log("C");
```

خروجی:

```text
A
B
C
```

هر دستور قبل از ادامه مسیر اجرا می‌شود.

## 2.2 Blocking

Blocking یعنی مسیر اجرایی فعلی نتواند به کار بعدی برسد تا عملیات فعلی تمام شود.

مثال CPU-bound:

```js
function heavyWork() {
  let total = 0;

  for (let i = 0; i < 5_000_000_000; i++) {
    total += i;
  }

  return total;
}

console.log("start");
heavyWork();
console.log("end");
```

در Browser چنین کاری می‌تواند UI را برای مدتی متوقف کند.

## 2.3 Non-Blocking

در مدل Non-Blocking، یک عملیات I/O می‌تواند شروع شود و Runtime اجازه دهد جریان اصلی کارهای دیگری انجام دهد.

این مفهوم به‌خصوص برای:

- Network
- File I/O
- Database
- Timers
- User Input

مهم است.

---

# 3. Asynchronous Programming

Asynchronous Programming یعنی نتیجه یک عملیات در همان لحظه در دسترس نیست و برنامه باید برای دریافت نتیجه آینده آماده باشد.

نمونه:

```js
console.log("شروع");

setTimeout(() => {
  console.log("کار تمام شد");
}, 1000);

console.log("ادامه برنامه");
```

خروجی:

```text
شروع
ادامه برنامه
کار تمام شد
```

نکته مهم:

`setTimeout` برنامه را دقیقاً برای یک ثانیه متوقف نمی‌کند؛ حداقل زمان انتظار را تعیین می‌کند و Callback بعداً در صورت فراهم بودن شرایط اجرا می‌شود.

---

# 4. `setTimeout` و Timerها

## 4.1 مثال ساده

```js
setTimeout(() => {
  console.log("Hello");
}, 2000);
```

## 4.2 مقدار صفر

```js
console.log("A");

setTimeout(() => {
  console.log("B");
}, 0);

console.log("C");
```

خروجی معمولاً:

```text
A
C
B
```

صفر به معنی «همین الان» نیست.

## 4.3 `setInterval`

```js
const id = setInterval(() => {
  console.log("tick");
}, 1000);

setTimeout(() => {
  clearInterval(id);
}, 5000);
```

در برنامه‌های واقعی باید مراقب Intervalهای فراموش‌شده و Memory Leak بود.

---

# 5. Callbackها

Callback تابعی است که به تابع دیگری داده می‌شود تا بعداً اجرا شود.

```js
function loadData(callback) {
  setTimeout(() => {
    callback("Data loaded");
  }, 1000);
}

loadData((data) => {
  console.log(data);
});
```

## 5.1 Error-first Callback

الگوی سنتی در Node.js:

```js
function operation(callback) {
  setTimeout(() => {
    const error = null;
    const result = "OK";
    callback(error, result);
  }, 500);
}

operation((error, result) => {
  if (error) {
    console.error(error);
    return;
  }

  console.log(result);
});
```

---

# 6. Callback Hell و مشکلات Callback

نمونه کلاسیک:

```js
getUser(user => {
  getOrders(user.id, orders => {
    getOrderDetails(orders[0].id, details => {
      getInvoice(details.id, invoice => {
        sendEmail(invoice, result => {
          console.log(result);
        });
      });
    });
  });
});
```

مشکلات:

- تو در تو شدن کد
- دشواری Error Handling
- دشواری Cancellation
- دشواری تست
- دشواری حفظ ترتیب
- پیچیدگی Composition

Promise و `async/await` بسیاری از این مشکلات را کاهش می‌دهند.

---

# 7. Promise از پایه تا حرفه‌ای

Promise نماینده نتیجه آینده یک عملیات است.

سه وضعیت اصلی:

```text
pending
   |
   +--> fulfilled
   |
   +--> rejected
```

بعد از `fulfilled` یا `rejected`، Promise اصطلاحاً settled است.

## 7.1 ساخت Promise

```js
const promise = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve("موفق");
  }, 1000);
});
```

مصرف:

```js
promise
  .then((value) => console.log(value))
  .catch((error) => console.error(error))
  .finally(() => console.log("تمام شد"));
```

## 7.2 Reject

```js
const promise = new Promise((resolve, reject) => {
  reject(new Error("Operation failed"));
});
```

## 7.3 Promise فقط یک بار settle می‌شود

```js
new Promise((resolve, reject) => {
  resolve("first");
  resolve("second");
  reject(new Error("ignored"));
});
```

نتیجه فقط همان resolve اول خواهد بود.

## 7.4 Promiseهای آماده

```js
Promise.resolve(10);
Promise.reject(new Error("failed"));
```

---

# 8. Promise Chaining

```js
getUser()
  .then(user => getOrders(user.id))
  .then(orders => getOrderDetails(orders[0].id))
  .then(details => console.log(details))
  .catch(error => console.error(error));
```

هر `.then()` یک Promise جدید تولید می‌کند.

اگر Handler یک مقدار عادی برگرداند، آن مقدار برای مرحله بعد resolve می‌شود.

```js
Promise.resolve(10)
  .then(x => x * 2)
  .then(x => console.log(x));
```

اگر Promise برگردانیم، Chain منتظر آن می‌ماند:

```js
Promise.resolve(10)
  .then(x => Promise.resolve(x * 2))
  .then(console.log);
```

---

# 9. `async` و `await`

هر تابع `async` یک Promise برمی‌گرداند.

```js
async function hello() {
  return "Hello";
}
```

معادل مفهومی:

```js
function hello() {
  return Promise.resolve("Hello");
}
```

## 9.1 `await`

```js
async function load() {
  const data = await getData();
  return data;
}
```

`await` اجرای همان async function را تا تعیین تکلیف Promise متوقف می‌کند؛ کل Runtime یا Thread اصلی را متوقف نمی‌کند.

## 9.2 await روی مقدار عادی

```js
const value = await 42;
```

از نظر Promise Resolution، مقدار به شکل Promise پذیرفته می‌شود.

## 9.3 چند await پشت سر هم

```js
const a = await taskA();
const b = await taskB();
```

این دو عملیات از نظر شروع شدن sequential هستند.

اگر مستقل باشند:

```js
const promiseA = taskA();
const promiseB = taskB();

const [a, b] = await Promise.all([promiseA, promiseB]);
```

---

# 10. مدیریت خطا در Async Code

## 10.1 try/catch

```js
async function run() {
  try {
    const result = await operation();
    return result;
  } catch (error) {
    console.error("Operation failed:", error);
    throw error;
  }
}
```

## 10.2 finally

```js
async function run() {
  try {
    return await operation();
  } finally {
    console.log("cleanup");
  }
}
```

## 10.3 Propagation

```js
async function lowLevel() {
  throw new Error("DB failure");
}

async function service() {
  return lowLevel();
}

async function controller() {
  try {
    return await service();
  } catch (error) {
    console.error(error);
  }
}
```

## 10.4 Unhandled Rejection

Promiseهای reject شده باید در نقطه مناسب مدیریت شوند.

در Node.js همچنین می‌توان رویدادهای مربوط به Unhandled Rejection را برای Observability ثبت کرد، اما بهتر است علت اصلی را در طراحی برنامه حل کنیم نه فقط خطا را پنهان کنیم.

---

# 11. Event Loop

مدل مفهومی ساده:

```text
             JavaScript
                 |
             Call Stack
                 |
        +--------+--------+
        |                 |
    Host APIs        Runtime APIs
        |                 |
        +--------+--------+
                 |
        +--------+--------+
        |                 |
   Task Queue       Microtask Queue
        |                 |
        +--------+--------+
                 |
             Event Loop
                 |
             Call Stack
```

Event Loop کمک می‌کند کارهای آماده شده در زمان مناسب وارد مسیر اجرای JavaScript شوند.

---

# 12. Call Stack

Call Stack ساختاری LIFO است.

```js
function a() {
  b();
}

function b() {
  c();
}

function c() {
  console.log("hello");
}

a();
```

در زمان اجرای `c`، Stack مفهومی شبیه زیر است:

```text
c()
b()
a()
main()
```

Recursion بسیار عمیق می‌تواند باعث Stack Overflow شود.

---

# 13. Web APIs / Host APIs و Runtime

Timer و شبکه بخشی از خود Call Stack نیستند.

در Browser، قابلیت‌هایی مانند:

- DOM Events
- Fetch
- Timer
- WebSocket
- Web Worker

توسط Browser Runtime فراهم می‌شوند.

در Node.js نیز Runtime قابلیت‌هایی مانند:

- File System
- Network
- Timers
- Streams
- Worker Threads

فراهم می‌کند.

بنابراین باید بین ECMAScript Language و Host Environment تفاوت گذاشت.

---

# 14. Task، Microtask و Job Queue

مثال مهم:

```js
console.log("1");

setTimeout(() => console.log("2"), 0);

Promise.resolve().then(() => console.log("3"));

console.log("4");
```

خروجی معمولاً:

```text
1
4
3
2
```

چرا؟

1. `1` مستقیم اجرا می‌شود.
2. Timer برای Task بعدی برنامه‌ریزی می‌شود.
3. Promise reaction به Microtask تبدیل می‌شود.
4. `4` مستقیم اجرا می‌شود.
5. بعد از پایان اجرای فعلی، Microtask پردازش می‌شود.
6. سپس Task بعدی می‌تواند اجرا شود.

## `queueMicrotask`

```js
queueMicrotask(() => {
  console.log("microtask");
});
```

استفاده نادرست و بسیار زیاد از Microtaskها می‌تواند باعث گرسنگی Taskهای دیگر شود.

---

# 15. ترتیب اجرای عملیات Async

مثال پیچیده‌تر:

```js
console.log("A");

setTimeout(() => console.log("B"), 0);

Promise.resolve()
  .then(() => console.log("C"))
  .then(() => console.log("D"));

queueMicrotask(() => console.log("E"));

console.log("F");
```

ترتیب معمول:

```text
A
F
C
E
D
B
```

نکته مهم: جزئیات دقیق scheduling به Host وابسته است، اما قاعده اصلی این است که Microtaskها پس از پایان اجرای synchronous فعلی و پیش از Taskهای بعدی پردازش می‌شوند.

---

# 16. Promise Combinators

## 16.1 Promise.all

برای کارهایی که همگی باید موفق شوند:

```js
const [user, orders, settings] = await Promise.all([
  getUser(),
  getOrders(),
  getSettings()
]);
```

اگر یکی Reject شود، Promise حاصل Reject می‌شود.

نکته مهم: `Promise.all` عملیات دیگر را خودکار Cancel نمی‌کند.

## 16.2 Promise.allSettled

```js
const results = await Promise.allSettled([
  taskA(),
  taskB(),
  taskC()
]);

for (const result of results) {
  console.log(result.status);
}
```

مناسب زمانی است که نتیجه تک‌تک عملیات مهم است.

## 16.3 Promise.race

```js
const result = await Promise.race([
  primaryTask(),
  timeoutTask()
]);
```

اولین Promise که settled شود نتیجه را تعیین می‌کند.

## 16.4 Promise.any

```js
const result = await Promise.any([
  serverA(),
  serverB(),
  serverC()
]);
```

اولین Promise موفق را برمی‌گرداند. اگر همه Reject شوند، `AggregateError` رخ می‌دهد.

---

# 17. Sequential، Concurrent و Parallel

## Sequential

```js
const a = await taskA();
const b = await taskB();
```

اگر `taskB` به `taskA` وابسته نیست، ممکن است زمان اضافی ایجاد شود.

## Concurrent

```js
const aPromise = taskA();
const bPromise = taskB();

const [a, b] = await Promise.all([aPromise, bPromise]);
```

دو عملیات برای پیشرفت هم‌زمان در اختیار Runtime قرار گرفته‌اند.

## Parallel

Parallelism یعنی کار واقعاً در چند مسیر اجرایی مانند Workerها یا Coreهای مختلف CPU انجام شود.

پس:

```text
Concurrency != Parallelism
```

---

# 18. `fetch` و HTTP به صورت Async

```js
async function loadData(url) {
  const response = await fetch(url);

  if (!response.ok) {
    throw new Error(`HTTP ${response.status}`);
  }

  return response.json();
}
```

نکته مهم:

`fetch` معمولاً برای وضعیت‌هایی مانند 404 یا 500 به خودی خود Reject نمی‌شود؛ باید `response.ok` یا status را بررسی کرد.

## POST

```js
await fetch("/api/users", {
  method: "POST",
  headers: {
    "Content-Type": "application/json"
  },
  body: JSON.stringify({ name: "Ali" })
});
```

## Network Error

```js
try {
  const response = await fetch(url);
} catch (error) {
  console.error("Network-level failure", error);
}
```

---

# 19. Event Listener و Event-driven Programming

```js
button.addEventListener("click", async () => {
  try {
    const data = await loadData();
    console.log(data);
  } catch (error) {
    console.error(error);
  }
});
```

Event-driven Programming بر پایه Event و Handler است.

نمونه رویدادها:

- click
- input
- submit
- change
- message
- close
- error

## Cleanup

اگر Listener دیگر لازم نیست:

```js
function handleClick() {
  console.log("clicked");
}

button.addEventListener("click", handleClick);

button.removeEventListener("click", handleClick);
```

استفاده از تابع anonymous در جایی که بعداً به removal نیاز داریم می‌تواند مشکل‌ساز شود.

---

# 20. Browser Runtime در برابر Node.js Runtime

## Browser

تمرکز بیشتر بر:

- UI
- DOM
- User Events
- Rendering
- Network
- Web Workers

## Node.js

تمرکز بیشتر بر:

- Server
- File System
- Network
- Streams
- Processes
- Worker Threads

هر دو محیط JavaScript را اجرا می‌کنند، اما APIهای Host یکسان نیستند.

---

# 21. Closure در Async Programming

Closure باعث می‌شود تابع داخلی به متغیرهای Scope بیرونی دسترسی داشته باشد.

```js
function createCounter() {
  let count = 0;

  return () => {
    count++;
    return count;
  };
}

const counter = createCounter();
```

در Async Code باید مراقب Capture کردن state متغیرها باشیم.

```js
function createTasks() {
  const tasks = [];

  for (let i = 0; i < 3; i++) {
    tasks.push(() => Promise.resolve(i));
  }

  return tasks;
}
```

استفاده از `let` در این مثال باعث می‌شود هر iteration binding مناسب خود را داشته باشد.

---

# 22. Thenable و Promise Resolution

هر شیئی که قراردادی شبیه `then` داشته باشد می‌تواند در فرآیند Promise Resolution مهم باشد.

```js
const thenable = {
  then(resolve) {
    resolve("done");
  }
};

Promise.resolve(thenable).then(console.log);
```

این نکته در درک عمیق Promise مهم است، زیرا `Promise.resolve()` صرفاً همیشه یک مقدار ساده را مستقیم wrap نمی‌کند؛ Promise Resolution Procedure را دنبال می‌کند.

---

# 23. Cancellation و `AbortController`

JavaScript Promise به تنهایی مکانیزم عمومی Cancellation ندارد.

برای APIهایی مانند Fetch می‌توان از `AbortController` استفاده کرد.

```js
const controller = new AbortController();

fetch(url, {
  signal: controller.signal
});

controller.abort();
```

## تشخیص Abort

```js
try {
  await fetch(url, { signal: controller.signal });
} catch (error) {
  if (error.name === "AbortError") {
    console.log("Request cancelled");
  } else {
    throw error;
  }
}
```

## یک Signal برای چند عملیات

```js
const controller = new AbortController();

const signal = controller.signal;

await Promise.all([
  fetch(url1, { signal }),
  fetch(url2, { signal }),
  fetch(url3, { signal })
]);
```

با abort کردن controller، عملیات‌هایی که Signal را پشتیبانی می‌کنند می‌توانند متوقف شوند.

---

# 24. Timeout برای عملیات Async

یک روش رایج استفاده از `AbortSignal.timeout` در محیط‌هایی است که آن را پشتیبانی می‌کنند:

```js
const response = await fetch(url, {
  signal: AbortSignal.timeout(5000)
});
```

روش عمومی‌تر با Controller:

```js
async function fetchWithTimeout(url, timeoutMs) {
  const controller = new AbortController();

  const timer = setTimeout(() => {
    controller.abort();
  }, timeoutMs);

  try {
    const response = await fetch(url, {
      signal: controller.signal
    });

    return response;
  } finally {
    clearTimeout(timer);
  }
}
```

Timeout باید با Cancellation هماهنگ باشد تا Timer اضافی باقی نماند.

---

# 25. Retry

Retry یعنی در صورت خطای موقت، عملیات دوباره امتحان شود.

نسخه ساده:

```js
async function retry(operation, attempts = 3) {
  let lastError;

  for (let i = 1; i <= attempts; i++) {
    try {
      return await operation();
    } catch (error) {
      lastError = error;
    }
  }

  throw lastError;
}
```

اما در سیستم واقعی باید مشخص کنیم کدام خطاها قابل Retry هستند.

مثلاً:

- Timeout موقت: ممکن است قابل Retry باشد.
- Network interruption: ممکن است قابل Retry باشد.
- Authentication failure: معمولاً Retry ساده راه‌حل نیست.
- Validation error: معمولاً Retry فایده‌ای ندارد.

---

# 26. Exponential Backoff و Jitter

به جای Retry فوری:

```text
100 ms
200 ms
400 ms
800 ms
1600 ms
```

می‌توان از Exponential Backoff استفاده کرد.

```js
function delay(ms) {
  return new Promise(resolve => setTimeout(resolve, ms));
}

async function retryWithBackoff(operation, attempts = 5) {
  let lastError;

  for (let attempt = 0; attempt < attempts; attempt++) {
    try {
      return await operation();
    } catch (error) {
      lastError = error;

      if (attempt === attempts - 1) {
        break;
      }

      const base = 200 * (2 ** attempt);
      const jitter = Math.random() * 100;
      await delay(base + jitter);
    }
  }

  throw lastError;
}
```

Jitter از هم‌زمان شدن تعداد زیادی Client برای Retry جلوگیری می‌کند.

---

# 27. Race Condition

Race Condition زمانی رخ می‌دهد که نتیجه برنامه به ترتیب یا زمان‌بندی اجرای چند عملیات وابسته شود.

مثال:

```js
let state = 0;

async function updateSlow() {
  const value = await slowOperation();
  state = value;
}

async function updateFast() {
  const value = await fastOperation();
  state = value;
}
```

اگر هر دو هم‌زمان اجرا شوند، ترتیب نهایی assignment ممکن است باعث نتیجه‌ای شود که از دید Business Logic نامطلوب باشد.

راهکارها:

- حذف Shared Mutable State
- Sequence کردن عملیات
- Request ID
- Versioning
- Mutex
- Cancellation
- Last-write-wins به صورت صریح

---

# 28. Shared State و Data Consistency

مثال خطرناک:

```js
let balance = 100;

async function withdraw(amount) {
  if (balance >= amount) {
    await delay(100);
    balance -= amount;
  }
}
```

اگر دو برداشت هم‌زمان شوند، check و update از هم جدا شده‌اند.

در سیستم‌های واقعی باید Atomicity و Consistency مناسب طراحی شود.

راهکار می‌تواند شامل:

- Lock
- Database Transaction
- Atomic operation
- Queue
- Version check
- Idempotency

باشد.

---

# 29. Ordering و حفظ ترتیب

اگر بخواهیم نتیجه‌ها به ترتیب ورودی باقی بمانند:

```js
const promises = items.map(item => processItem(item));
const results = await Promise.all(promises);
```

`Promise.all` خروجی‌ها را مطابق ترتیب Input می‌دهد، حتی اگر عملیات داخلی در زمان‌های مختلف تمام شوند.

در مقابل، اگر بخواهیم هر نتیجه را همان لحظه که آماده شد مصرف کنیم، به الگوی دیگری مانند Queue یا Async Iterator نیاز داریم.

---

# 30. Debounce و Throttle

## Debounce

برای زمانی که می‌خواهیم بعد از توقف رویدادها عملیات انجام شود.

مثلاً Search Box:

```js
function debounce(fn, wait) {
  let timer;

  return (...args) => {
    clearTimeout(timer);

    timer = setTimeout(() => {
      fn(...args);
    }, wait);
  };
}
```

استفاده:

```js
const search = debounce((query) => {
  console.log("search", query);
}, 300);
```

## Throttle

برای محدود کردن تعداد اجرا در یک بازه زمانی.

مثلاً Scroll:

```js
function throttle(fn, wait) {
  let last = 0;

  return (...args) => {
    const now = Date.now();

    if (now - last >= wait) {
      last = now;
      fn(...args);
    }
  };
}
```

---

# 31. Concurrency Limit

اجرای هزار عملیات هم‌زمان ممکن است سیستم را تحت فشار قرار دهد.

مثلاً:

```js
const results = await Promise.all(
  items.map(item => process(item))
);
```

اگر `items` بسیار زیاد باشد، تعداد زیادی عملیات هم‌زمان شروع می‌شود.

Concurrency Limit یعنی مثلاً فقط 5 عملیات هم‌زمان باشند.

```js
async function mapWithConcurrency(items, worker, limit = 5) {
  const results = new Array(items.length);
  let nextIndex = 0;

  async function runWorker() {
    while (true) {
      const index = nextIndex++;

      if (index >= items.length) {
        return;
      }

      results[index] = await worker(items[index], index);
    }
  }

  const workers = Array.from(
    { length: Math.min(limit, items.length) },
    () => runWorker()
  );

  await Promise.all(workers);
  return results;
}
```

این الگو هم Concurrency را محدود می‌کند و هم ترتیب خروجی را حفظ می‌کند.

---

# 32. Async Queue و Worker Pool

Queue:

```text
Producer
   |
   v
+-------+
| Queue |
+-------+
   |
   +--> Worker 1
   +--> Worker 2
   +--> Worker 3
```

Worker Pool یعنی تعداد مشخصی Worker داشته باشیم و هر Worker از Queue کار بردارد.

کاربردها:

- پردازش فایل
- Image Processing
- ارسال درخواست
- پردازش Job
- Data Transformation

مزیت مهم:

> تعداد عملیات هم‌زمان قابل کنترل می‌شود.

---

# 33. Producer / Consumer

Producer داده تولید می‌کند و Consumer آن را مصرف می‌کند.

```text
Producer ---> Queue ---> Consumer
```

اگر Producer سریع‌تر از Consumer باشد، Queue رشد می‌کند.

پس باید Capacity و Backpressure در نظر گرفته شود.

---

# 34. Backpressure

Backpressure یعنی Consumer به Producer علامت دهد که سرعت تولید بیش از ظرفیت مصرف است.

مثال مفهومی:

```text
Producer: 1000 items/sec
Consumer: 100 items/sec
```

اگر هیچ محدودیتی نباشد، Buffer می‌تواند به سرعت رشد کند.

راهکارها:

- Bounded Queue
- Pause/Resume
- Batch Processing
- Rate Limit
- Concurrency Limit
- Drop Strategy در موارد مناسب

---

# 35. Streams و Async Iteration

Stream برای پردازش داده‌های پیوسته یا حجیم مناسب است.

به جای:

```text
Load entire file -> Memory -> Process
```

می‌توان:

```text
Chunk -> Process -> Chunk -> Process
```

را انجام داد.

این کار Memory Consumption را کاهش می‌دهد.

---

# 36. `for await...of`

برای Async Iterableها:

```js
async function* numbers() {
  for (let i = 1; i <= 3; i++) {
    await delay(100);
    yield i;
  }
}

for await (const number of numbers()) {
  console.log(number);
}
```

Async Generator می‌تواند داده را تدریجی تولید کند.

## Async Generator

```js
async function* fetchPages() {
  let page = 1;

  while (page <= 3) {
    const data = await fetchPage(page);
    yield data;
    page++;
  }
}
```

---

# 37. Top-Level `await`

در ES Modules می‌توان در سطح Module از `await` استفاده کرد.

```js
const config = await loadConfig();

export { config };
```

باید اثر آن بر Module Loading و Dependency Graph را در نظر گرفت.

استفاده بیش از حد از Initializationهای طولانی می‌تواند startup را کند کند.

---

# 38. Dynamic `import()`

```js
const module = await import("./feature.js");
```

کاربردها:

- Lazy Loading
- Code Splitting
- Feature-based loading
- کاهش startup cost

مثال:

```js
button.addEventListener("click", async () => {
  const { openEditor } = await import("./editor.js");
  openEditor();
});
```

---

# 39. Async Initialization و Cleanup

برنامه‌های واقعی اغلب نیاز دارند:

1. Config Load
2. Connection
3. Cache Initialization
4. Worker Startup
5. Application Start
6. Shutdown

نمونه:

```js
class App {
  async start() {
    await this.loadConfig();
    await this.connect();
  }

  async stop() {
    await this.closeConnections();
    await this.stopWorkers();
  }
}
```

Shutdown باید Idempotent باشد؛ یعنی اجرای چندباره آن نباید سیستم را به وضعیت خراب ببرد.

---

# 40. Mutex و Semaphore

## Mutex

Mutex اجازه می‌دهد یک بخش حساس فقط توسط یک عملیات در یک زمان اجرا شود.

مدل مفهومی:

```text
Task A -> Lock -> Critical Section -> Unlock
Task B --------> Wait --------------> Lock
```

یک Mutex ساده آموزشی:

```js
class Mutex {
  constructor() {
    this.locked = false;
    this.waiters = [];
  }

  async acquire() {
    if (!this.locked) {
      this.locked = true;
      return this.release.bind(this);
    }

    await new Promise(resolve => this.waiters.push(resolve));
    this.locked = true;
    return this.release.bind(this);
  }

  release() {
    const next = this.waiters.shift();

    if (next) {
      next();
    } else {
      this.locked = false;
    }
  }
}
```

استفاده:

```js
const mutex = new Mutex();

const release = await mutex.acquire();

try {
  await criticalOperation();
} finally {
  release();
}
```

## Semaphore

Semaphore اجازه می‌دهد تعداد مشخصی عملیات هم‌زمان وارد بخش شوند.

اگر ظرفیت 3 باشد:

```text
Task 1 -> allowed
Task 2 -> allowed
Task 3 -> allowed
Task 4 -> wait
```

---

# 41. Web Worker و Worker Threads

برای CPU-bound Work، Async API به تنهایی کافی نیست.

در Browser می‌توان از Web Worker استفاده کرد.

```text
Main Thread
     |
     +---- Worker
     |
     +---- Worker
```

در Node.js می‌توان از `worker_threads` استفاده کرد.

اصل مهم:

> Async I/O با CPU Parallelism یکی نیست.

اگر محاسبه CPU بسیار سنگین است، انتقال آن به Worker می‌تواند از Block شدن مسیر اصلی جلوگیری کند.

---

# 42. Memory و Performance

## مشکل 1: Promiseهای زیاد

ایجاد تعداد بسیار زیاد Promise می‌تواند Memory Pressure ایجاد کند.

## مشکل 2: Queue نامحدود

```text
Producer >>>>>>>>>>> Consumer
```

Queue رشد می‌کند.

## مشکل 3: Listener Leak

Listenerهایی که حذف نمی‌شوند می‌توانند Objectها را زنده نگه دارند.

## مشکل 4: Timer Leak

Intervalهای بدون cleanup می‌توانند به فعالیت برنامه ادامه دهند.

## مشکل 5: Closureهای بزرگ

Closure ممکن است به داده‌های Scope بیرونی دسترسی داشته باشد و باعث طولانی شدن عمر آن‌ها شود.

بهینه‌سازی باید بر اساس اندازه‌گیری باشد، نه حدس.

---

# 43. Observability، Logging و Metrics

یک Async System حرفه‌ای باید بتواند بفهمد:

- چه زمانی عملیات شروع شد؟
- چه زمانی تمام شد؟
- چند بار Retry شد؟
- چقدر طول کشید؟
- چند عملیات شکست خورد؟
- Timeout چقدر بود؟
- Queue چقدر رشد کرد؟

نمونه ساده:

```js
async function tracedOperation(operation) {
  const started = performance.now();

  try {
    return await operation();
  } finally {
    const elapsed = performance.now() - started;
    console.log(`operation took ${elapsed.toFixed(2)} ms`);
  }
}
```

برای سیستم‌های بزرگ‌تر باید Correlation ID و Structured Logging نیز در نظر گرفته شود.

---

# 44. Testing کد Async

تست Async باید منتظر نتیجه بماند.

مثال مفهومی:

```js
test("loads data", async () => {
  const result = await loadData();
  expect(result).toEqual({ ok: true });
});
```

## Fake Timer

برای Timerها بهتر است در تست از Fake Timerهای Framework تست استفاده شود تا تست سریع و Deterministic باشد.

## تست Error

```js
await expect(loadFailingData()).rejects.toThrow();
```

## تست Timeout

باید بررسی شود که:

- timeout رخ می‌دهد
- عملیات cancel می‌شود
- resource cleanup می‌شود

---

# 45. Debugging کد Async

روش‌های مفید:

1. ثبت timestamp
2. ثبت Request ID
3. ثبت شروع و پایان عملیات
4. ثبت Retry count
5. بررسی Promise chain
6. استفاده از Debugger
7. بررسی Network tab
8. بررسی Call Stack
9. بررسی Memory
10. بررسی Unhandled Rejection

مثال Logging:

```js
console.log("[request] started", requestId);

try {
  const result = await operation();
  console.log("[request] completed", requestId);
  return result;
} catch (error) {
  console.error("[request] failed", requestId, error);
  throw error;
}
```

---

# 46. Security در Async Applications

Asynchronous بودن به خودی خود Security ایجاد نمی‌کند.

باید موارد زیر را بررسی کرد:

- Input Validation
- Authentication
- Authorization
- Secret Management
- SSRF در Server-side Fetch
- Rate Limiting
- Resource Exhaustion
- Denial of Service
- Unsafe Dynamic Import
- Untrusted URLs
- Unbounded Concurrency

## Resource Exhaustion

مثلاً اگر API اجازه دهد یک User میلیون‌ها Job ایجاد کند، Async Queue می‌تواند Memory را مصرف کند.

راهکارها:

- Queue limit
- Rate limit
- Maximum payload size
- Timeout
- Cancellation
- Authentication
- Authorization

---

# 47. Anti-Patterns رایج

## Anti-pattern 1: `await` پشت سر هم برای کارهای مستقل

بد:

```js
const a = await taskA();
const b = await taskB();
```

در صورت استقلال:

```js
const [a, b] = await Promise.all([
  taskA(),
  taskB()
]);
```

## Anti-pattern 2: Promise.all روی میلیون‌ها Job

```js
await Promise.all(items.map(process));
```

اگر `items` بسیار زیاد باشد، بهتر است Concurrency Limit داشته باشیم.

## Anti-pattern 3: swallow کردن خطا

```js
try {
  await operation();
} catch {
}
```

این کار می‌تواند خطاهای مهم را مخفی کند.

## Anti-pattern 4: Retry بدون Backoff

Retry فوری می‌تواند فشار روی سرویس خراب را افزایش دهد.

## Anti-pattern 5: Timeout بدون Cancellation

اگر فقط Timeout داخلی ایجاد شود ولی عملیات اصلی ادامه پیدا کند، ممکن است منابع همچنان مصرف شوند.

## Anti-pattern 6: Shared Mutable State بدون Synchronization

می‌تواند Race Condition ایجاد کند.

---

# 48. Structured Concurrency

Structured Concurrency یک رویکرد معماری است که عمر Child Tasks را به Scope والد مرتبط می‌کند.

ایده مفهومی:

```text
Parent Scope
  |
  +-- Child A
  +-- Child B
  +-- Child C
```

وقتی Scope والد تمام می‌شود، باید تکلیف Childها مشخص باشد:

- موفقیت
- خطا
- Cancellation
- Cleanup

JavaScript استاندارد یک Structured Concurrency Framework واحد برای تمام Runtimeها ارائه نمی‌کند، اما می‌توان اصول آن را با:

- AbortController
- Task Groups در Libraryها
- Scope management
- Promise composition

پیاده کرد.

---

# 49. معماری واقعی Async Application

یک معماری نمونه:

```text
                    Client
                      |
                      v
                 API Layer
                      |
                      v
                Service Layer
                      |
          +-----------+-----------+
          |                       |
       Cache                    Queue
          |                       |
          |                 +-----+-----+
          |                 |           |
          |              Worker A   Worker B
          |                 |           |
          +---------> Database <-------+
```

## لایه‌های مهم

### API Layer

- Request validation
- Authentication
- Timeout
- Response mapping

### Service Layer

- Business logic
- Orchestration
- Retry policy
- Cancellation policy

### Queue Layer

- Buffering
- Backpressure
- Retry
- Dead-letter handling در سیستم‌های مناسب

### Worker Layer

- Job processing
- Concurrency control
- Idempotency

### Persistence Layer

- Transaction
- Consistency
- Connection pool

---

# 50. پروژه نهایی: Async Data Platform

هدف: ساخت یک برنامه که چند منبع داده را دریافت، پردازش و ذخیره کند.

## نیازمندی‌ها

1. دریافت هم‌زمان چند API
2. Timeout
3. Retry
4. Exponential Backoff
5. Jitter
6. Cancellation
7. Concurrency Limit
8. Queue
9. Worker Pool
10. Error Handling
11. Logging
12. Metrics
13. Cache
14. Graceful Shutdown
15. Testing

## معماری

```text
                 +-------------+
                 | API Sources |
                 +------+------+ 
                        |
                 Fetch / Retry
                        |
                +-------v--------+
                | Concurrency    |
                | Controller     |
                +-------+--------+
                        |
                     Queue
                        |
          +-------------+-------------+
          |             |             |
       Worker 1      Worker 2      Worker 3
          |             |             |
          +-------------+-------------+
                        |
                     Storage
```

## مرحله 1: Delay

```js
function delay(ms) {
  return new Promise(resolve => setTimeout(resolve, ms));
}
```

## مرحله 2: Fetch با Timeout

```js
async function fetchJson(url, timeoutMs = 5000) {
  const controller = new AbortController();
  const timer = setTimeout(() => controller.abort(), timeoutMs);

  try {
    const response = await fetch(url, {
      signal: controller.signal
    });

    if (!response.ok) {
      throw new Error(`HTTP ${response.status}`);
    }

    return await response.json();
  } finally {
    clearTimeout(timer);
  }
}
```

## مرحله 3: Retry

```js
async function retry(operation, attempts = 3) {
  let lastError;

  for (let i = 0; i < attempts; i++) {
    try {
      return await operation();
    } catch (error) {
      lastError = error;
    }
  }

  throw lastError;
}
```

## مرحله 4: ترکیب

```js
async function loadSource(url) {
  return retry(
    () => fetchJson(url, 5000),
    3
  );
}
```

## مرحله 5: اجرای محدودشده

```js
async function loadAll(urls) {
  return mapWithConcurrency(
    urls,
    url => loadSource(url),
    5
  );
}
```

## مرحله 6: Cleanup

```js
async function shutdown() {
  console.log("Stopping workers...");
  await stopWorkers();

  console.log("Closing resources...");
  await closeResources();

  console.log("Shutdown complete");
}
```

---

# 51. تمرین‌های مرحله‌ای

## تمرین 1: Timer

برنامه‌ای بنویسید که:

1. Start چاپ کند.
2. بعد از 2 ثانیه پیام چاپ کند.
3. End را قبل از آن چاپ کند.

## تمرین 2: Callback

تابعی بنویسید که پس از 1 ثانیه یک مقدار را به Callback بدهد.

## تمرین 3: Promise

همان برنامه را با Promise بازنویسی کنید.

## تمرین 4: async/await

Promise را با `async/await` مصرف کنید.

## تمرین 5: Error Handling

یک Promise بسازید که Reject شود و خطا را با `try/catch` مدیریت کنید.

## تمرین 6: Event Loop

خروجی این برنامه را قبل از اجرا پیش‌بینی کنید:

```js
console.log("A");

setTimeout(() => console.log("B"), 0);

Promise.resolve().then(() => console.log("C"));

queueMicrotask(() => console.log("D"));

console.log("E");
```

## تمرین 7: Promise.all

سه API فرضی را هم‌زمان اجرا کنید.

## تمرین 8: allSettled

نتیجه همه APIها را حتی در صورت خطا گزارش کنید.

## تمرین 9: Timeout

Fetch را پس از 3 ثانیه Abort کنید.

## تمرین 10: Retry

Retry را با حداکثر 4 تلاش پیاده‌سازی کنید.

## تمرین 11: Backoff

زمان انتظار را به شکل Exponential افزایش دهید.

## تمرین 12: Jitter

Random Jitter اضافه کنید.

## تمرین 13: Race Condition

برنامه‌ای بسازید که دو update هم‌زمان داشته باشد و مشکل را مشاهده کنید.

## تمرین 14: Debounce

Search Box با Debounce بسازید.

## تمرین 15: Throttle

Scroll Handler با Throttle بسازید.

## تمرین 16: Concurrency Limit

100 کار را با حداکثر 5 Worker اجرا کنید.

## تمرین 17: Queue

یک Queue ساده بسازید.

## تمرین 18: Producer/Consumer

Producer و Consumer با ظرفیت محدود بسازید.

## تمرین 19: Async Generator

داده‌ها را یکی‌یکی تولید کنید.

## تمرین 20: Worker

یک محاسبه CPU-heavy را به Worker منتقل کنید.

---

# 52. چک‌لیست تسلط

اگر می‌خواهید بگویید Asynchronous JavaScript را در سطح عملی یاد گرفته‌اید، باید بتوانید این موارد را توضیح دهید:

- [ ] Synchronous چیست؟
- [ ] Blocking چیست؟
- [ ] Non-Blocking چیست؟
- [ ] Asynchronous چیست؟
- [ ] Callback چیست؟
- [ ] Callback Hell چیست؟
- [ ] Promise چیست؟
- [ ] Promise State چیست؟
- [ ] `then` چگونه کار می‌کند؟
- [ ] `catch` چگونه کار می‌کند؟
- [ ] `finally` چه کاربردی دارد؟
- [ ] Promise Chaining چیست؟
- [ ] `async` چه می‌کند؟
- [ ] `await` چه می‌کند؟
- [ ] چرا await کل Runtime را Block نمی‌کند؟
- [ ] Event Loop چیست؟
- [ ] Call Stack چیست؟
- [ ] Task چیست؟
- [ ] Microtask چیست؟
- [ ] چرا Promise callback معمولاً قبل از Timer اجرا می‌شود؟
- [ ] Promise.all چیست؟
- [ ] Promise.allSettled چیست؟
- [ ] Promise.race چیست؟
- [ ] Promise.any چیست؟
- [ ] Sequential چیست؟
- [ ] Concurrent چیست؟
- [ ] Parallel چیست؟
- [ ] Fetch چه زمانی Error می‌دهد؟
- [ ] AbortController چیست؟
- [ ] Timeout چگونه طراحی می‌شود؟
- [ ] Retry چه زمانی مناسب است؟
- [ ] Backoff چیست؟
- [ ] Jitter چیست؟
- [ ] Race Condition چیست؟
- [ ] Shared Mutable State چرا خطرناک است؟
- [ ] Debounce چیست؟
- [ ] Throttle چیست؟
- [ ] Concurrency Limit چیست؟
- [ ] Queue چیست؟
- [ ] Worker Pool چیست؟
- [ ] Producer/Consumer چیست؟
- [ ] Backpressure چیست؟
- [ ] Stream چیست؟
- [ ] Async Iterator چیست؟
- [ ] Async Generator چیست؟
- [ ] `for await...of` چیست؟
- [ ] Top-Level await چیست؟
- [ ] Dynamic import چیست؟
- [ ] Graceful Shutdown چیست؟
- [ ] Mutex چیست؟
- [ ] Semaphore چیست؟
- [ ] Worker چیست؟
- [ ] CPU-bound و I/O-bound چه تفاوتی دارند؟
- [ ] Memory Leak در Async Code چگونه رخ می‌دهد؟
- [ ] Observability چرا مهم است؟
- [ ] Async Code چگونه تست می‌شود؟
- [ ] Async Code چگونه Debug می‌شود؟
- [ ] Async Application چگونه Secure می‌شود؟
- [ ] Anti-patternهای اصلی چیست؟
- [ ] Structured Concurrency چیست؟

---

# 53. مسیر پیشنهادی یادگیری

## سطح 1 — پایه

1. Synchronous
2. Blocking
3. Non-Blocking
4. Timer
5. Callback

## سطح 2 — Promise

6. Promise
7. then/catch/finally
8. Chaining
9. async/await
10. Error Handling

## سطح 3 — Runtime

11. Call Stack
12. Event Loop
13. Task
14. Microtask
15. Host APIs

## سطح 4 — Composition

16. Promise.all
17. allSettled
18. race
19. any
20. Sequential/Concurrent

## سطح 5 — Production

21. Fetch
22. Timeout
23. Cancellation
24. Retry
25. Backoff
26. Jitter

## سطح 6 — Concurrency

27. Race Condition
28. Shared State
29. Mutex
30. Semaphore
31. Concurrency Limit
32. Queue

## سطح 7 — Data Flow

33. Producer/Consumer
34. Backpressure
35. Streams
36. Async Iteration
37. Async Generators

## سطح 8 — Runtime و Performance

38. Workers
39. Memory
40. Performance
41. Observability
42. Debugging
43. Testing

## سطح 9 — Architecture

44. Structured Concurrency
45. Graceful Shutdown
46. Async Service Architecture
47. Queue-based Architecture
48. Production Patterns

---

# جمع‌بندی نهایی

Asynchronous JavaScript را نباید فقط با `async/await` مساوی دانست.

برای درک واقعی آن باید زنجیره زیر را بفهمید:

```text
Synchronous Execution
        |
        v
Call Stack
        |
        v
Host APIs
        |
        v
Tasks / Microtasks
        |
        v
Event Loop
        |
        v
Callbacks / Promise Reactions
        |
        v
async / await
        |
        v
Concurrency
        |
        v
Cancellation / Timeout
        |
        v
Retry / Backoff / Jitter
        |
        v
Queues / Workers / Backpressure
        |
        v
Streams / Async Iteration
        |
        v
Testing / Debugging / Observability
        |
        v
Production Async Architecture
```

مهم‌ترین اصل عملی این است:

> کد Async خوب فقط کدی نیست که «کار کند»؛ باید بتواند خطا، Timeout، Cancellation، Retry، Concurrency، Ordering، Resource Cleanup، Memory Pressure و Shutdown را نیز به شکل کنترل‌شده مدیریت کند.

---

# پروژه نهایی پیشنهادی

برای تثبیت همه مطالب، یک **Enterprise Async Data Processing Platform** بسازید که دارای اجزای زیر باشد:

```text
                    +----------------+
                    | HTTP/API Input |
                    +-------+--------+
                            |
                            v
                    +---------------+
                    | Validation    |
                    +-------+-------+
                            |
                            v
                    +---------------+
                    | Concurrency   |
                    | Controller    |
                    +-------+-------+
                            |
                            v
                    +---------------+
                    | Bounded Queue |
                    +-------+-------+
                            |
               +------------+------------+
               |            |            |
               v            v            v
            Worker 1     Worker 2     Worker 3
               |            |            |
               +------------+------------+
                            |
                            v
                    +---------------+
                    | Persistence   |
                    +---------------+

        Cross-cutting:
        Timeout | Retry | Backoff | Jitter
        Cancellation | Logging | Metrics
        Testing | Security | Graceful Shutdown
```

این پروژه تقریباً تمام مفاهیم این درس را در یک سیستم واحد ترکیب می‌کند.

---

# پایان درس

این نسخه، نسخه توسعه‌یافته و یکپارچه درس است و صرفاً فهرست عنوان‌ها نیست؛ برای هر مبحث، مفهوم، نکات مهم، مثال کد، الگوی استفاده و در موارد لازم خطاها و Anti-patternهای مرتبط را پوشش می‌دهد.
