# مرجع جامع انواع داده در ۲۰ زبان برنامه‌نویسی

**نسخه:** ۱٫۰ — شهریور ۱۴۰۵ (سپتامبر ۲۰۲۶)
**دامنه:** Python · JavaScript/TypeScript · Java · C# · C++ · C · Go · Rust · Kotlin · Swift · Dart · Ruby · PHP · Scala · Erlang · Elixir · Zig · Carbon · Gleam · Haskell

---

## فهرست مطالب

1. [چارچوب مفهومی: انواع داده را چگونه طبقه‌بندی کنیم؟](#۱-چارچوب-مفهومی)
2. [جداول مقایسه‌ای عرضی](#۲-جداول-مقایسهای-عرضی)
3. [بررسی زبان‌به‌زبان](#۳-بررسی-زبانبهزبان)
   - [۳٫۱ Python](#۳۱-python)
   - [۳٫۲ JavaScript و TypeScript](#۳۲-javascript-و-typescript)
   - [۳٫۳ Java](#۳۳-java)
   - [۳٫۴ C#](#۳۴-c)
   - [۳٫۵ C](#۳۵-c)
   - [۳٫۶ C++](#۳۶-c-1)
   - [۳٫۷ Go](#۳۷-go)
   - [۳٫۸ Rust](#۳۸-rust)
   - [۳٫۹ Kotlin](#۳۹-kotlin)
   - [۳٫۱۰ Swift](#۳۱۰-swift)
   - [۳٫۱۱ Dart](#۳۱۱-dart)
   - [۳٫۱۲ Ruby](#۳۱۲-ruby)
   - [۳٫۱۳ PHP](#۳۱۳-php)
   - [۳٫۱۴ Scala](#۳۱۴-scala)
   - [۳٫۱۵ Erlang](#۳۱۵-erlang)
   - [۳٫۱۶ Elixir](#۳۱۶-elixir)
   - [۳٫۱۷ Zig](#۳۱۷-zig)
   - [۳٫۱۸ Carbon](#۳۱۸-carbon)
   - [۳٫۱۹ Gleam](#۳۱۹-gleam)
   - [۳٫۲۰ Haskell](#۳۲۰-haskell)
4. [مباحث عرضی و عمیق](#۴-مباحث-عرضی-و-عمیق)
5. [الگوهای انتخاب نوع داده در عمل](#۵-الگوهای-انتخاب-نوع-داده-در-عمل)
6. [جمع‌بندی](#۶-جمعبندی)
7. [منابع](#۷-منابع)

---

## ۱. چارچوب مفهومی

پیش از ورود به جزئیات هر زبان، لازم است محورهایی را بشناسیم که تفاوت‌های واقعی بین سیستم‌های نوع را توضیح می‌دهند. بیشتر سردرگمی‌ها («چرا `tuple` در پایتون با `tuple` در Rust فرق دارد؟») از نادیده‌گرفتن همین محورها ناشی می‌شود.

### ۱٫۱ محور اول: بدوی (Primitive) در برابر مرکب (Composite)

| رده | تعریف | مثال‌ها |
|---|---|---|
| **بدوی / اسکالر** | نوعی که به اجزای کوچک‌تر تجزیه نمی‌شود و معمولاً نگاشت مستقیم به ثبات‌های CPU دارد | `int32`, `float64`, `bool`, `char` |
| **مرکب محصولی (Product)** | ترکیب هم‌زمان چند مقدار؛ «این **و** آن» | `struct`, `record`, `tuple`, `class` |
| **مرکب جمعی (Sum)** | یکی از چند حالت ممکن؛ «این **یا** آن» | `enum` در Rust/Swift, `sealed interface` در Java, `union` در TypeScript |
| **مجموعه‌ای (Collection)** | نگهدارنده تعداد نامعین از عناصر | `Array`, `List`, `Map`, `Set`, `Deque` |
| **ارجاعی/نشانگر** | ارجاع به محل داده | `*T` در C, `&T` در Rust, `Reference` در Java |
| **تابعی** | تابع به‌عنوان مقدار درجه‌یک | `Func<T>` در C#, `fn` در Rust, `lambda` در Python |

نکته کلیدی: **Tuple یک نوع محصولی بی‌نام (anonymous product) است** و `struct` یک نوع محصولی نام‌دار با فیلدهای نام‌دار. Map هم یک مجموعه است، نه نوع محصولی — حتی اگر در زبان‌های داینامیک مثل JavaScript برای شبیه‌سازی struct از آن استفاده شود.

### ۱٫۲ محور دوم: مقداری (Value) در برابر ارجاعی (Reference)

- **معنای مقداری:** انتساب و پاس‌دادن، کپی می‌سازد. `struct` در C/C++/Go/Rust/Swift/C#، همه انواع در Zig.
- **معنای ارجاعی:** انتساب، دو نام برای یک شیء می‌سازد. `class` در Java/C#/Python/Ruby/Dart، `slice`/`map` در Go.
- **موارد دوگانه:** Swift با `struct` مقداری + CoW، C# با `class`/`struct`، Kotlin با `data class` ارجاعی اما `value class` مقداری.

این محور بر سه چیز اثر مستقیم دارد: هزینه کپی، قابلیت اشتراک بین ریسمان‌ها (thread)، و معنای تساوی.

### ۱٫۳ محور سوم: تغییرپذیری (Mutability)

| الگو | زبان‌ها | توضیح |
|---|---|---|
| تغییرپذیر به‌صورت پیش‌فرض | Python (list/dict/set), Java, C#, Go, C/C++ | تغییرناپذیری با انتخاب نوع یا کلیدواژه (`final`, `const`, `readonly`) |
| تغییرناپذیر به‌صورت پیش‌فرض | Rust (`let` بدون `mut`), Kotlin (`val`), Scala, Swift (`let`) | تغییرپذیری صریح است |
| تغییرناپذیری کامل داده | Erlang, Elixir, Haskell, Gleam, Clojure | هیچ داده‌ای پس از ساخت تغییر نمی‌کند؛ «به‌روزرسانی» یعنی ساخت نسخه جدید با اشتراک ساختار |

تغییرناپذیری کامل، امنیت هم‌زمانی رایگان می‌دهد و قیمتش فشار بیشتر بر تخصیص حافظه و GC است — که در BEAM (Erlang/Elixir) با GC هر-فرایندی و در Haskell با nursery نسلی جبران می‌شود.

### ۱٫۴ محور چهارم: زمان بررسی نوع

- **ایستا (Static):** Java, C#, C, C++, Go, Rust, Kotlin, Swift, Scala, Haskell, Zig, Carbon, Gleam, TypeScript (زمان کامپایل).
- **پویا (Dynamic):** Python, Ruby, JavaScript, Erlang, Elixir (نوع‌ها به مقدار می‌چسبند نه به متغیر).
- **تدریجی (Gradual):** TypeScript روی JavaScript، type hints در Python، `declare(strict_types=1)` در PHP، Sorbet در Ruby، dialyzer/typespec در Erlang/Elixir.

### ۱٫۵ محور پنجم: تطابق نوع نامی (Nominal) در برابر ساختاری (Structural)

- **نامی:** دو `struct` با فیلدهای یکسان اما نام متفاوت، سازگار **نیستند** (Java, C#, Rust, Swift, Go برای struct نام‌دار).
- **ساختاری:** شکل داده تعیین‌کننده است (TypeScript, OCaml برای object، Go برای `interface`، Scala با refinement types).

### ۱٫۶ محور ششم: مدیریت نبودِ مقدار (Nullability)

| نسل | راهکار | زبان‌ها |
|---|---|---|
| نسل اول | `null` همه‌جا مجاز | Java (قبل از annotations), C#(قبل از ۸), JS, Python (`None`) |
| نسل دوم | نوع Option/Maybe در سیستم نوع | Rust (`Option<T>`), Haskell (`Maybe a`), Swift (`T?`), Scala (`Option[T]`), Gleam (`Option(a)`) |
| نسل سوم | null-safety در سطح کامپایلر با سازگاری عقب‌رو | Kotlin (`T?`), C# 8+ (NRT), Dart 2.12+ (sound null safety), TypeScript (`strictNullChecks`) |

اصطلاح معروف تونی هور، «اشتباه میلیارد دلاری»، به همین `null` اشاره دارد؛ روند تکاملی زبان‌ها در ۱۵ سال گذشته، حرکت آشکار به سمت نسل دوم و سوم بوده است.

---

## ۲. جداول مقایسه‌ای عرضی

### ۲٫۱ نگاشت نام‌ها: «یک مفهوم، بیست اسم»

| مفهوم | Python | JS/TS | Java | C# | C++ | Go | Rust |
|---|---|---|---|---|---|---|---|
| آرایه با طول ثابت | — | — | `int[5]` | `int[5]` | `std::array<int,5>` | `[5]int` | `[i32; 5]` |
| آرایه رشدپذیر | `list` | `Array` | `ArrayList<T>` | `List<T>` | `std::vector<T>` | `[]T` (slice) | `Vec<T>` |
| نگاشت کلید-مقدار | `dict` | `Map`/`object` | `HashMap<K,V>` | `Dictionary<K,V>` | `std::unordered_map` | `map[K]V` | `HashMap<K,V>` |
| نگاشت مرتب | — (dict ترتیب درج) | `Map` (ترتیب درج) | `TreeMap` | `SortedDictionary` | `std::map` | — | `BTreeMap` |
| مجموعه | `set`/`frozenset` | `Set` | `HashSet<T>` | `HashSet<T>` | `std::unordered_set` | `map[T]struct{}` | `HashSet<T>` |
| چندگانه (Tuple) | `tuple` | `[A, B]` در TS | `Record`/کتابخانه | `(A, B)` | `std::tuple` | — (چند بازگشتی) | `(A, B)` |
| نوع محصولی نام‌دار | `dataclass` | `interface`/`class` | `record` | `record` | `struct` | `struct` | `struct` |
| نوع جمعی (ADT) | `Union`/`Enum` | union type | `sealed interface` | — (با inheritance) | `std::variant` | — | `enum` |
| نوع اختیاری | `Optional[T]` | `T \| undefined` | `Optional<T>` | `T?` | `std::optional<T>` | `*T` | `Option<T>` |
| نتیجه/خطا | استثنا | استثنا | استثنا | استثنا | استثنا/`expected` | `(T, error)` | `Result<T,E>` |
| صف دوسر | `deque` | `Array` | `ArrayDeque` | `Deque`/`LinkedList` | `std::deque` | slice | `VecDeque` |

| مفهوم | Kotlin | Swift | Dart | Ruby | PHP | Scala | Haskell |
|---|---|---|---|---|---|---|---|
| آرایه رشدپذیر | `MutableList<T>` | `Array<T>` | `List<T>` | `Array` | `array` | `ArrayBuffer`/`List` | `[a]` / `Vector a` |
| نگاشت | `Map<K,V>` | `Dictionary<K,V>` | `Map<K,V>` | `Hash` | `array` انجمنی | `Map[K,V]` | `Data.Map.Map k v` |
| مجموعه | `Set<T>` | `Set<T>` | `Set<T>` | `Set` | `SplObjectStorage` | `Set[T]` | `Data.Set.Set a` |
| Tuple | `Pair`/`Triple` | `(A, B)` | `(A, B)` (Dart 3+) | `Array`/`Struct` | `array`/`list()` | `(A, B)` | `(a, b)` |
| محصولی نام‌دار | `data class` | `struct` | `class`/`record` | `Struct`/`Data` | `class` | `case class` | `data` با فیلد نام‌دار |
| نوع جمعی | `sealed class` | `enum` با payload | `sealed class` | — | `enum` (۸٫۱+) | `sealed trait`/`enum` | `data` با چند سازنده |
| اختیاری | `T?` | `T?` (`Optional<T>`) | `T?` | `nil` | `?T` | `Option[T]` | `Maybe a` |
| نتیجه | `Result<T>` | `Result<S,F>` | — | — | — | `Either`/`Try` | `Either e a` |

| مفهوم | Erlang | Elixir | Zig | Carbon | Gleam | C |
|---|---|---|---|---|---|---|
| لیست | `[1,2,3]` | `[1,2,3]` | — | — | `List(a)` | — |
| آرایه/برش | `array` module | — | `[N]T` / `[]T` | `array(T, N)` | — | `T[N]`, `T*` |
| نگاشت | `#{k => v}` | `%{k => v}` | `std.AutoHashMap` | (کتابخانه) | `Dict(k, v)` | — |
| مجموعه | `sets`/`ordsets` | `MapSet` | `std.AutoHashMap(T,void)` | (کتابخانه) | `Set(a)` | — |
| Tuple | `{a, b}` | `{a, b}` | `struct { A, B }` بی‌نام | `(A, B)` | `#(A, B)` | — |
| محصولی نام‌دار | `record` (ماکرو) | `defstruct` | `struct` | `class` | `type X { X(f: T) }` | `struct` |
| نوع جمعی | تطبیق الگو روی atom | همان | `union(enum)` | `choice` | `type` با چند variant | `union` + tag دستی |
| اختیاری | `undefined` atom | `nil` | `?T` | `Optional(T)` | `Option(a)` | `NULL` |
| نتیجه | `{ok,V}`/`{error,R}` | همان | `!T` (error union) | (در طراحی) | `Result(a, e)` | کد بازگشتی |

### ۲٫۲ انواع عددی: پهنا و محدوده

| نوع منطقی | C/C++ | Java | C# | Go | Rust | Swift | Zig/Carbon |
|---|---|---|---|---|---|---|---|
| صحیح ۸ بیتی علامت‌دار | `int8_t` | `byte` | `sbyte` | `int8` | `i8` | `Int8` | `i8` |
| صحیح ۸ بیتی بی‌علامت | `uint8_t` | — | `byte` | `uint8` | `u8` | `UInt8` | `u8` |
| صحیح ۱۶ بیتی | `int16_t` | `short` | `short` | `int16` | `i16` | `Int16` | `i16` |
| صحیح ۳۲ بیتی | `int32_t` | `int` | `int` | `int32` | `i32` | `Int32` | `i32` |
| صحیح ۶۴ بیتی | `int64_t` | `long` | `long` | `int64` | `i64` | `Int64` | `i64` |
| صحیح ۱۲۸ بیتی | `__int128` | — | `Int128` (.NET 7+) | — | `i128` | `Int128` (۶٫۰+) | `i128` |
| هم‌اندازه اشاره‌گر | `intptr_t` | — | `nint` | `int`/`uintptr` | `isize`/`usize` | `Int` | `isize`/`usize` |
| ممیز شناور ۳۲ | `float` | `float` | `float` | `float32` | `f32` | `Float` | `f32` |
| ممیز شناور ۶۴ | `double` | `double` | `double` | `float64` | `f64` | `Double` | `f64` |
| ممیز شناور ۱۶ | `_Float16` | — | `Half` | — | `f16` (ناپایدار) | `Float16` | `f16` |
| اعشاری دقیق | — | `BigDecimal` | `decimal` | `big.Float` | `rust_decimal` | `Decimal` (Foundation) | — |
| صحیح نامحدود | GMP | `BigInteger` | `BigInteger` | `big.Int` | `num-bigint` | (کتابخانه) | — |

زبان‌های با **صحیح نامحدود پیش‌فرض:** Python (`int`)، Ruby (`Integer`)، Erlang/Elixir، Haskell (`Integer`)، Scala (`BigInt` اختیاری)، PHP (سرریز به `float`)، JavaScript (`BigInt` جدا از `Number`).

### ۲٫۳ رفتار سرریز عدد صحیح — تفاوتی که اغلب نادیده می‌ماند

| زبان | حالت علامت‌دار | حالت بی‌علامت |
|---|---|---|
| C / C++ | **رفتار نامعین (UB)** | پیچش پیمانه‌ای (تعریف‌شده) |
| Java / C# (unchecked) | پیچش مکمل دو | پیچش |
| C# (`checked`) | استثنا `OverflowException` | استثنا |
| Go | پیچش تعریف‌شده | پیچش |
| Rust (debug) | **panic** | panic |
| Rust (release) | پیچش (با `wrapping_*`, `checked_*`, `saturating_*` صریح) | همان |
| Swift | **trap و توقف برنامه** (مگر `&+`) | همان |
| Zig | **خطای زمان اجرا** در حالت safe؛ UB در ReleaseFast؛ عملگرهای `+%` برای پیچش | همان |
| Carbon | علامت‌دار: خطای برنامه‌نویسی — در build توسعه گرفته می‌شود، در performance بهینه‌ساز فرض عدم وقوع می‌کند، در hardened برنامه abort می‌شود یا نتیجه نادرست می‌دهد؛ بی‌علامت: پیچش | پیچش |
| Python/Ruby/Erlang/Haskell(`Integer`) | سرریز وجود ندارد (ارتقا به دقت نامحدود) | — |

مأخذ رفتار Zig و Carbon: [مستندات زبان Zig](https://ziglang.org/documentation/master/) و [مستندات طراحی Carbon](https://docs.carbon-lang.dev/docs/design/).

### ۲٫۴ نمایش رشته و واحد کاراکتر

| زبان | نوع رشته | کدگذاری داخلی | واحد ایندکس | نوع کاراکتر |
|---|---|---|---|---|
| Python 3 | `str` (تغییرناپذیر) | UTF-32/16/8 تطبیقی (PEP 393) | code point | `str` طول ۱ |
| JavaScript | `String` | UTF-16 | code unit | — (`string` طول ۱) |
| Java | `String` | UTF-16 (با Compact Strings: Latin-1 یا UTF-16) | `char` (UTF-16) | `char` ۱۶ بیتی |
| C# | `string` | UTF-16 | `char` | `char` ۱۶ بیتی، `Rune` برای code point |
| C | `char*` | بایت خام، خاتمه با `\0` | بایت | `char` |
| C++ | `std::string`, `u8string`, `u16string`, `u32string` | بسته به نوع | بایت/واحد | `char`, `char8_t`, `char16_t`, `char32_t` |
| Go | `string` (تغییرناپذیر) | بایت‌های UTF-8 | **بایت** | `rune` = `int32` (code point), `byte` = `uint8` |
| Rust | `String`/`&str` | **UTF-8 تضمین‌شده** | بایت (برش باید روی مرز باشد) | `char` = یک Unicode scalar، ۴ بایت |
| Kotlin | `String` | UTF-16 (JVM) | `Char` | `Char` |
| Swift | `String` | UTF-8 (از Swift 5) | **Character** = extended grapheme cluster | `Character` (خوشه گرافیمی) |
| Dart | `String` | UTF-16 | code unit | — (`runes` برای code point) |
| Ruby | `String` (تغییرپذیر) | بایت + برچسب Encoding | کاراکتر بر اساس encoding | `String` طول ۱ |
| PHP | `string` | بایت خام | بایت | — |
| Erlang/Elixir | `binary`/`bitstring` | UTF-8 در Elixir | بایت (Elixir: `String.at` گرافیمی) | code point صحیح |
| Haskell | `String = [Char]`, `Text` | لیست پیوندی / UTF-16 یا UTF-8 در `text-2` | `Char` | `Char` = code point |
| Zig | `[]const u8` | بایت (قرارداد UTF-8) | بایت | `u8`/`u21` |
| Gleam | `String` | UTF-8 | گرافیم با API | — (`UtfCodepoint`) |

**Swift تنها زبان پرکاربردی است که `count` رشته را بر حسب خوشه گرافیمی می‌شمارد**؛ به همین دلیل `"👨‍👩‍👧‍👦".count == 1` در Swift اما `7` در JavaScript و `11` در Go (`len`).

### ۲٫۵ ماتریس قابلیت انواع مجموعه‌ای

| قابلیت | Python | JS | Java | C# | Go | Rust | Swift | Elixir |
|---|---|---|---|---|---|---|---|---|
| دسترسی O(1) با اندیس | ✅ list | ✅ | ✅ ArrayList | ✅ List | ✅ slice | ✅ Vec | ✅ Array | ❌ لیست پیوندی |
| نگاشت با ترتیب درج | ✅ dict | ✅ Map | ✅ LinkedHashMap | ✅ (بی‌ضمانت) | ❌ | ✅ IndexMap (crate) | ✅ OrderedDictionary | ❌ |
| نگاشت مرتب‌شده | ❌ | ❌ | ✅ TreeMap | ✅ SortedDictionary | ❌ | ✅ BTreeMap | ✅ (کتابخانه) | ❌ |
| مجموعه تغییرناپذیر | ✅ frozenset | ❌ | ✅ Set.of | ✅ ImmutableHashSet | ❌ | ❌ | ❌ | ✅ (همه) |
| هش‌مقاوم به DoS | ✅ (str) | تا حدی | ❌ | ❌ | ✅ (map seed) | ✅ SipHash پیش‌فرض | ✅ | ✅ |
| کلید چندنوعی | ✅ | ✅ | ✅ | ✅ | محدود به قابل‌مقایسه | نیازمند `Hash+Eq` | `Hashable` | ✅ |
| صف اولویت | ✅ heapq | ❌ | ✅ PriorityQueue | ✅ PriorityQueue | ✅ container/heap | ✅ BinaryHeap | ✅ (کتابخانه) | ✅ :gb_trees |
| ساختار پایدار (persistent) | ❌ | ❌ | ❌ | ✅ Immutable* | ❌ | ✅ `im` crate | ❌ | ✅ بومی |

---

## ۳. بررسی زبان‌به‌زبان

### ۳٫۱ Python

**فلسفه نوع:** پویا، با تایپ اردکی (duck typing) در زمان اجرا و type hints اختیاری برای ابزارهای ایستا (mypy، pyright). همه چیز شیء است؛ حتی کلاس‌ها و توابع.

#### انواع بدوی و اسکالر

| نوع | مشخصات |
|---|---|
| `int` | صحیح با **دقت نامحدود** — محدودیت فقط حافظه. متدهایی مانند `bit_length()`, `bit_count()`, `to_bytes()`, `as_integer_ratio()` دارد ([مستندات Python](https://docs.python.org/3/library/stdtypes.html)) |
| `float` | معمولاً `double` زبان C، یعنی IEEE-754 binary64. `float.hex()`, `is_integer()` |
| `complex` | عدد مختلط با دو جزء شناور، `z.real` و `z.imag`، بدون ترتیب‌پذیری |
| `bool` | **زیرکلاس `int`** — `True == 1` و `False == 0` در محاسبات |
| `NoneType` | تک‌نمونه `None` |
| `Ellipsis` | تک‌نمونه `...`، در type annotation و placeholder |
| `NotImplemented` | بازگشتی از عملگرها برای انواع پشتیبانی‌نشده |
| `decimal.Decimal` | ممیز شناور اعشاری با دقت قابل تنظیم؛ برای محاسبات پولی |
| `fractions.Fraction` | عدد گویا دقیق |

#### انواع دنباله‌ای

| نوع | تغییرپذیر؟ | نکته |
|---|---|---|
| `list` | ✅ | آرایه پویا از اشاره‌گرها؛ `append` سرشکن O(1)، `insert(0, x)` برابر O(n)؛ `sort()` پایدار (Timsort) |
| `tuple` | ❌ | دنباله تغییرناپذیر، معمولاً برای داده ناهمگن؛ `(x,)` برای تک‌عضوی؛ قابل هش اگر اعضا قابل هش باشند |
| `range` | ❌ | دنباله عددی با حافظه ثابت؛ فقط `start`, `stop`, `step` را ذخیره می‌کند |
| `str` | ❌ | دنباله code point یونیکد |
| `bytes` | ❌ | دنباله تغییرناپذیر بایت |
| `bytearray` | ✅ | نسخه تغییرپذیر `bytes` |
| `memoryview` | — | نمای بدون کپی روی بافر (پروتکل بافر) |

#### نگاشت و مجموعه

```python
# dict — از Python 3.7 ترتیب درج بخشی از مشخصات زبان است
d: dict[str, int] = {"a": 1, "b": 2}
d.setdefault("c", 3)
merged = d | {"d": 4}          # عملگر ادغام، 3.9+
match_key = d.get("z", 0)

# set و frozenset
s = {1, 2, 3}
fs = frozenset(s)              # قابل هش، قابل استفاده به‌عنوان کلید dict
s | {4}; s & {2}; s - {1}; s ^ {3}
```

- `dict`: جدول هش با پیاده‌سازی compact (کلید/مقدار در آرایه فشرده + آرایه اندیس). سربار حافظه کمتر از CPython 3.6 به بعد.
- کلیدها باید **قابل هش** باشند (`__hash__` و `__eq__`). `list` قابل هش نیست، `tuple` از عناصر قابل هش هست.
- `collections`: `defaultdict`, `OrderedDict` (با `move_to_end`), `Counter`, `ChainMap`, `deque` (صف دوسر O(1) در دو انتها), `namedtuple`.

#### انواع محصولی و جمعی

```python
from dataclasses import dataclass
from typing import NamedTuple, TypedDict, Literal
from enum import Enum, StrEnum, Flag, auto

@dataclass(frozen=True, slots=True)   # تغییرناپذیر + بهینه حافظه
class Point:
    x: float
    y: float

class Pair(NamedTuple):               # tuple نام‌دار، typed
    key: str
    value: int

class Config(TypedDict):              # شکل dict در سطح نوع
    host: str
    port: int

class Color(Enum):
    RED = auto()
    GREEN = auto()

type Shape = Circle | Square          # نوع جمعی، سینتکس 3.12+
Mode = Literal["r", "w", "a"]         # نوع لیترال
```

- `@dataclass` با `frozen=True` نوع محصولی تغییرناپذیر و قابل هش می‌سازد؛ `slots=True` دیکشنری نمونه را حذف می‌کند و مصرف حافظه را چشمگیر کم می‌کند.
- `match`/`case` (3.10+) تطبیق الگوی ساختاری روی dataclass، tuple، dict و نوع‌های جمعی می‌دهد — نزدیک‌ترین چیز به ADT در پایتون.
- `Protocol` تطابق نوع **ساختاری** را به سیستم تایپ اختیاری پایتون می‌آورد.

#### انواع عددی تخصصی اکوسیستم

`numpy` مجموعه کاملی از انواع با پهنای دقیق (`np.int8` … `np.uint64`, `np.float16/32/64/128`, `np.complex128`, `np.datetime64`, `np.bool_`) به‌همراه `ndarray` چندبُعدی و `dtype` ساختاریافته می‌دهد که در پایتون خالص وجود ندارد.

---

### ۳٫۲ JavaScript و TypeScript

#### انواع بدوی JavaScript (۷ عدد + شیء)

| نوع | مشخصات |
|---|---|
| `number` | **IEEE-754 binary64 برای همه اعداد** — صحیح ایمن تا \(2^{53}-1\) (`Number.MAX_SAFE_INTEGER`). `NaN`, `Infinity`, `-0` |
| `bigint` | صحیح با دقت نامحدود، لیترال `123n`. **با `number` قابل ترکیب در عملگر نیست** |
| `string` | تغییرناپذیر، UTF-16؛ `length` بر حسب code unit |
| `boolean` | `true`/`false` |
| `undefined` | مقدار پیش‌فرض متغیر تعریف‌نشده |
| `null` | نبود مقدار عمدی؛ `typeof null === "object"` (باگ تاریخی) |
| `symbol` | شناسه یکتا برای کلید خصوصی و پروتکل‌ها (`Symbol.iterator`) |
| `object` | هر چیز دیگر: Array، Function، Date، Map، Set، RegExp، Promise… |

#### مجموعه‌های استاندارد

```js
const arr = [1, 2, 3];               // آرایه پویا، ناهمگن، اندیس عددی
const map = new Map([["a", 1]]);      // کلید هر نوعی، ترتیب درج حفظ می‌شود
const set = new Set([1, 2, 2]);       // مقادیر یکتا، ترتیب درج
const wm  = new WeakMap();            // کلید شیء، ارجاع ضعیف — مانع GC نمی‌شود
const ws  = new WeakSet();
const ta  = new Int32Array(10);       // TypedArray روی ArrayBuffer
const buf = new ArrayBuffer(1024);
const dv  = new DataView(buf);        // خواندن/نوشتن با endianness مشخص
```

- `Object` به‌عنوان نگاشت: کلیدها فقط `string` یا `symbol`؛ کلید عددی به رشته تبدیل می‌شود. برای نگاشت واقعی `Map` بهتر است (کلید هر نوعی، `size` مستقیم، تکرار ترتیبی، بدون آلودگی prototype).
- `TypedArray`ها: `Int8Array`, `Uint8Array`, `Uint8ClampedArray`, `Int16/32`, `Uint16/32`, `Float16Array`, `Float32/64Array`, `BigInt64Array`, `BigUint64Array` — نمای نوع‌دار روی `ArrayBuffer` / `SharedArrayBuffer`.
- `Record`/`Tuple` (پیشنهاد تغییرناپذیر عمیق) پس از سال‌ها بررسی در TC39 به مرحله پیاده‌سازی نرسید؛ برای ساختار پایدار از Immutable.js یا `Object.freeze` استفاده می‌شود.

#### سیستم نوع TypeScript

TypeScript یک لایه نوع **ساختاری، تدریجی و پاک‌شدنی (erased)** روی JavaScript است؛ در زمان اجرا هیچ اثری از انواع نمی‌ماند.

```ts
// انواع پایه و ویژه
let a: number; let b: string; let c: boolean;
let u: unknown;      // ایمن — پیش از استفاده باید narrow شود
let n: never;        // نوع تهی؛ تابعی که هرگز برنمی‌گردد
let v: void;
let x: any;          // فرار از سیستم نوع

// نوع محصولی و tuple
type Point = { readonly x: number; y?: number };
type Pair  = [string, number];                 // tuple
type Named = [name: string, age: number];      // tuple با برچسب
type Rest  = [string, ...number[]];            // tuple با بخش متغیر

// نوع جمعی و تفکیک‌شده (discriminated union)
type Shape =
  | { kind: "circle"; r: number }
  | { kind: "rect"; w: number; h: number };

function area(s: Shape): number {
  switch (s.kind) {                 // narrowing کامل
    case "circle": return Math.PI * s.r ** 2;
    case "rect":   return s.w * s.h;
  }
}

// انواع سطح-نوع (type-level)
type Keys = keyof Shape;
type Ro<T> = { readonly [K in keyof T]: T[K] };       // mapped type
type Ret<T> = T extends (...a: any) => infer R ? R : never;  // conditional + infer
type Greet = `hello ${string}`;                        // template literal type

// enum و جایگزین ترجیحی
enum Dir { Up, Down }                 // مقدار زمان اجرا تولید می‌کند
const Dir2 = { Up: "up", Down: "down" } as const;
type Dir2 = typeof Dir2[keyof typeof Dir2];
```

- **تفکیک‌شده‌های union (discriminated unions)** جایگزین عملی ADT هستند و با `switch` بررسی جامع (exhaustiveness) می‌دهند.
- `readonly`, `as const`, `Readonly<T>`, `ReadonlyArray<T>` تغییرناپذیری را فقط در زمان کامپایل تضمین می‌کنند.
- انواع کمکی داخلی: `Partial`, `Required`, `Pick`, `Omit`, `Record<K,V>`, `Exclude`, `Extract`, `NonNullable`, `Awaited`, `ReturnType`, `Parameters`.
- `satisfies` (۴٫۹+) بررسی انطباق بدون از دست دادن استنباط دقیق.
- برندسازی نوع (`type UserId = string & { __brand: "UserId" }`) برای جبران ساختاری‌بودن و ساختن نوع‌های نامی مصنوعی.

---

### ۳٫۳ Java

**فلسفه:** ایستا، نامی، شیء‌گرا با تمایز سخت بین انواع **بدوی** (روی پشته/در ثبات) و انواع **ارجاعی** (روی heap).

#### هشت نوع بدوی

| نوع | پهنا | محدوده | پیش‌فرض |
|---|---|---|---|
| `byte` | ۸ | −۱۲۸ … ۱۲۷ | `0` |
| `short` | ۱۶ | −۳۲۷۶۸ … ۳۲۷۶۷ | `0` |
| `int` | ۳۲ | \(-2^{31}\) … \(2^{31}-1\) | `0` |
| `long` | ۶۴ | \(-2^{63}\) … \(2^{63}-1\) | `0L` |
| `float` | ۳۲ | IEEE-754 binary32 | `0.0f` |
| `double` | ۶۴ | IEEE-754 binary64 | `0.0d` |
| `char` | ۱۶ | واحد کد UTF-16، بی‌علامت ۰…۶۵۵۳۵ | `'\u0000'` |
| `boolean` | تعریف‌نشده | `true`/`false` | `false` |

Java **نوع صحیح بی‌علامت ندارد**؛ به‌جای آن متدهای ایستا مانند `Integer.toUnsignedLong`, `Long.divideUnsigned`, `Integer.compareUnsigned` ارائه شده است. هر بدوی یک کلاس پوششی دارد (`Integer`, `Long`, …) با autoboxing خودکار و کش `Integer` برای بازه −۱۲۸…۱۲۷ (منبع باگ‌های `==` روی `Integer`).

#### مجموعه‌ها — چارچوب Collections

```
Iterable
└── Collection
    ├── List      → ArrayList, LinkedList, Vector, CopyOnWriteArrayList, List.of()
    ├── Set       → HashSet, LinkedHashSet, TreeSet (SortedSet/NavigableSet), EnumSet
    ├── Queue     → ArrayDeque, PriorityQueue, LinkedList
    │   └── Deque → ArrayDeque, LinkedList
    └── (Map جدا) → HashMap, LinkedHashMap, TreeMap, EnumMap,
                     ConcurrentHashMap, WeakHashMap, IdentityHashMap, Hashtable
```

| کلاس | پیچیدگی/ویژگی |
|---|---|
| `ArrayList` | آرایه پویا، دسترسی O(1)، درج وسط O(n) |
| `LinkedList` | لیست دوپیوندی، درج O(1) با iterator، دسترسی O(n) |
| `HashMap` | سطل‌های هش؛ از Java 8 سطل پرجمعیت به درخت سرخ-سیاه تبدیل می‌شود (O(log n) بدترین حالت) |
| `LinkedHashMap` | ترتیب درج (یا دسترسی، برای LRU با `removeEldestEntry`) |
| `TreeMap` | درخت سرخ-سیاه، مرتب، `floorKey`/`ceilingKey`/`subMap` |
| `EnumMap`/`EnumSet` | آرایه/بیت‌ماسک پشت صحنه؛ بسیار سریع و کم‌حجم برای کلید enum |
| `ConcurrentHashMap` | قطعه‌بندی/CAS، `compute`, `merge` اتمی |
| `List.of` / `Map.of` | مجموعه‌های تغییرناپذیر، پرتاب `UnsupportedOperationException` |

#### امکانات نوین سیستم نوع (Java 14 تا 25)

```java
// record — نوع محصولی نام‌دار تغییرناپذیر با equals/hashCode/toString خودکار
record Point(double x, double y) {
    Point {                                  // سازنده فشرده برای اعتبارسنجی
        if (Double.isNaN(x)) throw new IllegalArgumentException();
    }
}

// sealed interface + record = نوع جبری (ADT)
sealed interface Shape permits Circle, Rect {}
record Circle(double r) implements Shape {}
record Rect(double w, double h) implements Shape {}

double area(Shape s) {
    return switch (s) {                      // بررسی جامع در زمان کامپایل
        case Circle c            -> Math.PI * c.r() * c.r();
        case Rect(var w, var h)  -> w * h;    // تخریب الگوی record
    };
}

Optional<String> name = Optional.ofNullable(maybeNull);   // نوع اختیاری
var stream = list.stream().map(...).toList();             // Stream + استنباط var
```

- `Optional<T>` برای مقدار بازگشتی طراحی شده، نه برای فیلد یا پارامتر.
- `sealed` + `record` + `switch pattern matching` ترکیبی است که Java را از نظر مدل‌سازی داده به زبان‌های ML-محور نزدیک کرده است.
- **انواع مقداری (Value Classes)** در پروژه Valhalla در مسیر استاندارد شدن است و مرز بدوی/ارجاعی را محو خواهد کرد.
- `BigInteger`, `BigDecimal` (با `MathContext` و `RoundingMode`) برای دقت دلخواه؛ `java.time` (`Instant`, `LocalDate`, `ZonedDateTime`, `Duration`, `Period`) برای زمان.

---

### ۳٫۴ C#

#### انواع مقداری داخلی

| رده | انواع |
|---|---|
| صحیح | `sbyte`, `byte`, `short`, `ushort`, `int`, `uint`, `long`, `ulong`, `nint`, `nuint`, `Int128`, `UInt128` |
| شناور | `float` (۳۲)، `double` (۶۴)، `Half` (۱۶) |
| اعشاری | `decimal` — ۱۲۸ بیتی، ۲۸–۲۹ رقم معنادار، پایه ۱۰؛ **استاندارد محاسبات پولی** |
| دیگر | `bool`, `char` (UTF-16), `Rune` (code point) |

`decimal` تفاوت مهم C# با Java است: نوع اعشاری در سطح زبان با لیترال `19.99m`.

#### انواع مرکب

```csharp
// record — مرجعی و تغییرناپذیر با تساوی مقداری
public record Person(string Name, int Age);
var p2 = p1 with { Age = 31 };            // کپی غیرمخرب

// record struct — مقداری و کم‌هزینه
public readonly record struct Point(double X, double Y);

// tuple مقداری با نام فیلد (System.ValueTuple)
(string name, int age) t = ("Ada", 36);
var (name, age) = t;                       // تخریب
(int, int) Swap((int a, int b) x) => (x.b, x.a);

// struct و ref struct
public readonly struct Vec3 { public readonly float X, Y, Z; }
public ref struct SpanHolder { }           // فقط روی پشته

// Span و Memory — دسترسی بدون تخصیص
Span<byte> sp = stackalloc byte[64];
ReadOnlySpan<char> slice = "hello world".AsSpan(0, 5);

// nullable
string? maybe = null;                      // reference nullable (C# 8+)
int? n = null;                             // Nullable<int> مقداری
int len = maybe?.Length ?? 0;
```

- **Nullable Reference Types** (C# 8+) با `#nullable enable`: `string` غیرتهی، `string?` تهی‌پذیر؛ هشدار زمان کامپایل، بدون تغییر زمان اجرا.
- `Nullable<T>` (`T?` برای انواع مقداری) در زمان اجرا واقعی است — یک `struct` با `HasValue`/`Value`.
- `enum` بر پایه هر نوع صحیح؛ `[Flags]` برای بیت‌ماسک.
- `dynamic` برای صرف‌نظر از بررسی ایستا تا زمان اجرا؛ `object` ریشه همه انواع؛ boxing/unboxing برای انواع مقداری.

#### مجموعه‌ها

| فضای نام | انواع کلیدی |
|---|---|
| `System.Collections.Generic` | `List<T>`, `Dictionary<K,V>`, `HashSet<T>`, `SortedDictionary<K,V>`, `SortedSet<T>`, `Queue<T>`, `Stack<T>`, `LinkedList<T>`, `PriorityQueue<TE,TP>` |
| `System.Collections.Concurrent` | `ConcurrentDictionary`, `ConcurrentQueue`, `ConcurrentBag`, `BlockingCollection` |
| `System.Collections.Immutable` | `ImmutableArray<T>`, `ImmutableList<T>`, `ImmutableDictionary<K,V>`, `ImmutableHashSet<T>` — ساختارهای **پایدار** با اشتراک ساختار |
| `System.Collections.Frozen` | `FrozenDictionary`, `FrozenSet` — ساخت گران، خواندن بسیار سریع |
| فضایی/برداری | `Vector<T>`, `Vector128/256/512<T>` برای SIMD |

---

### ۳٫۵ C

C کوچک‌ترین سیستم نوع فهرست ماست و همه چیز حول نمایش حافظه می‌گردد.

#### انواع پایه

```c
// انواع صحیح — پهنا به پیاده‌سازی وابسته است، فقط حداقل تضمین می‌شود
char, signed char, unsigned char           // ≥ 8 بیت، CHAR_BIT
short, unsigned short                      // ≥ 16
int, unsigned int                          // ≥ 16 (عملاً 32)
long, unsigned long                        // ≥ 32 (لینوکس 64، ویندوز 32)
long long, unsigned long long              // ≥ 64

// انواع با پهنای دقیق — <stdint.h>، راه درست
int8_t, int16_t, int32_t, int64_t
uint8_t, uint16_t, uint32_t, uint64_t
intptr_t, uintptr_t, size_t, ptrdiff_t
int_least32_t, int_fast16_t, intmax_t

// شناور
float, double, long double
_Float16, _Float32, _Float64, _Float128    // C23, TS 18661
float _Complex, double _Complex            // <complex.h>

// منطقی و دیگر
bool (C23 کلیدواژه؛ پیش‌تر _Bool + <stdbool.h>)
void                                       // نوع ناقص
nullptr_t                                  // C23
```

**نکته حیاتی پرتابل‌پذیری:** `char` می‌تواند علامت‌دار یا بی‌علامت باشد (به پلتفرم بسته است)، `int` می‌تواند ۱۶ بیت باشد، و `sizeof(long)` بین لینوکس (LP64) و ویندوز (LLP64) متفاوت است. برای کد پرتابل همیشه از `<stdint.h>` استفاده کنید.

#### انواع مشتق

```c
struct Point { double x, y; };              // نوع محصولی؛ padding و alignment دارد
union Value { int i; float f; char *s; };   // همپوشانی حافظه — فقط یک عضو معتبر
enum Color { RED, GREEN = 5, BLUE };        // شمارشی؛ نوع پایه پیاده‌سازی‌وابسته (C23: قابل تعیین)
typedef struct Point Point;
int arr[10];                                // آرایه با طول ثابت
int (*fp)(int, int);                        // اشاره‌گر به تابع
int *p; void *vp;                           // اشاره‌گر
int vla[n];                                 // VLA — C99، اختیاری از C11
struct Flags { unsigned a : 1, b : 3; };    // بیت‌فیلد
_Atomic int counter;                        // C11 اتمیک
struct Tagged {                             // الگوی tagged union دستی
    enum { T_INT, T_STR } tag;
    union { int i; char *s; } data;
};
```

- **C نه `string` دارد، نه `Map`، نه `Set`، نه `Tuple`، نه جنریک واقعی.** رشته‌ها قراردادی هستند: `char*` با خاتمه `'\0'`. مجموعه‌ها را خودتان یا با کتابخانه‌ها (`glib`, `uthash`, `stb_ds`, `klib`) می‌سازید.
- جنریک تقریبی با ماکرو، `void*` + `size_t`، یا `_Generic` (C11) برای انتخاب بر اساس نوع.
- `const`, `volatile`, `restrict`, `_Atomic` واجدشرط‌های نوع (qualifier) هستند، نه نوع.
- `struct` با اعضای انعطاف‌پذیر (`char data[];` در پایان) الگوی رایج برای بافر با طول متغیر است.

---

### ۳٫۶ C++

C++ همه انواع C را به ارث می‌برد و یک کتابخانه استاندارد بسیار غنی روی آن می‌سازد، با «انتزاع بی‌هزینه» (zero-cost abstraction) به‌عنوان اصل راهنما.

#### انواع بنیادین افزوده بر C

```cpp
bool
char8_t (C++20), char16_t, char32_t, wchar_t
std::byte                     // بایت خام معنادار، بدون معنای عددی
std::nullptr_t
std::size_t, std::ptrdiff_t
std::int_fast64_t ...         // <cstdint>
std::float16_t, std::bfloat16_t, std::float128_t   // C++23 <stdfloat>
```

#### انواع کتابخانه استاندارد — نقشه کامل

| رده | انواع |
|---|---|
| رشته | `std::string`, `wstring`, `u8string`, `u16string`, `u32string`, `string_view` (نمای بدون مالکیت) |
| دنباله | `array<T,N>` (پشته، طول ثابت), `vector<T>`, `deque<T>`, `list<T>` (دوپیوندی), `forward_list<T>`, `inplace_vector` (C++26) |
| نگاشت مرتب | `map<K,V>`, `multimap<K,V>` — درخت سرخ-سیاه، O(log n) |
| نگاشت هش | `unordered_map<K,V>`, `unordered_multimap` — سطل + زنجیره |
| مجموعه | `set`, `multiset`, `unordered_set`, `unordered_multiset`, `flat_set` (C++23) |
| نگاشت مسطح | `flat_map` (C++23) — دو آرایه موازی، حافظه‌پیوسته و cache-friendly |
| آداپتور | `stack<T>`, `queue<T>`, `priority_queue<T>` |
| بیت | `bitset<N>`, `vector<bool>` (تخصص بحث‌برانگیز) |
| محصولی | `pair<A,B>`, `tuple<Ts...>` + `tie`, `apply`, `structured bindings` |
| جمعی | `variant<Ts...>` + `visit`, `any`, `optional<T>`, `expected<T,E>` (C++23) |
| نما و دامنه | `span<T>`, `mdspan` (C++23), `ranges::views::*` (C++20) |
| هوشمند | `unique_ptr<T>`, `shared_ptr<T>`, `weak_ptr<T>` |
| زمان | `chrono::duration`, `time_point`, `year_month_day`, `zoned_time` (C++20) |
| هم‌زمانی | `atomic<T>`, `atomic_ref`, `future<T>`, `jthread` |

```cpp
// tuple و structured binding
std::tuple<int, std::string, double> row{1, "Ada", 3.5};
auto [id, name, score] = row;                  // C++17

// variant = نوع جمعی نوع-ایمن
std::variant<int, std::string, double> v = "hi";
std::visit([](auto&& x){ std::cout << x; }, v);

// optional و expected
std::optional<int> parse(std::string_view s);
std::expected<Config, ParseError> load(std::string_view path);   // C++23

// concepts — محدودیت نوع جنریک (C++20)
template<typename T>
concept Numeric = std::integral<T> || std::floating_point<T>;
template<Numeric T> T square(T x) { return x * x; }

// designated initializers و aggregate
struct Cfg { int port = 8080; bool tls = false; };
Cfg c{.port = 443, .tls = true};               // C++20
```

- **`std::variant` + `std::visit`** معادل ADT است، اما ارگونومی آن به‌مراتب ضعیف‌تر از `enum` در Rust یا `sealed` در Java است (نبود تطبیق الگوی زبانی — پیشنهاد `inspect` هنوز استاندارد نشده).
- `string_view` و `span` انواع **بدون مالکیت** هستند؛ عمر (lifetime) را کامپایلر بررسی نمی‌کند — منبع رایج dangling reference.
- `constexpr`/`consteval` و `std::integral_constant` محاسبه با انواع در زمان کامپایل را ممکن می‌کنند؛ template metaprogramming عملاً یک زبان نوع تورینگ-کامل است.

---

### ۳٫۷ Go

**فلسفه:** سادگی رادیکال. مجموعه انواع کوچک، تنها سه ساختار داده داخلی (slice، map، channel)، و از Go 1.18 جنریک محدود.

#### انواع پایه

```go
bool
string                                        // تغییرناپذیر، بایت‌های UTF-8
int  int8  int16  int32  int64
uint uint8 uint16 uint32 uint64 uintptr
byte = uint8      rune = int32                // نام‌های مستعار معنادار
float32 float64
complex64 complex128
error                                         // اینترفیس داخلی
any = interface{}                             // Go 1.18
```

`int` و `uint` اندازه‌شان پلتفرم‌وابسته است (۶۴ بیت روی پلتفرم‌های مدرن). **تبدیل عددی همیشه باید صریح باشد** — حتی `int` به `int64`.

#### انواع مرکب

```go
// آرایه: طول بخشی از نوع است، معنای مقداری (کپی در انتساب)
var a [5]int
b := a                                        // کپی کامل

// slice: توصیفگر سه‌کلمه‌ای {ptr, len, cap} با معنای ارجاعی
s := make([]int, 0, 10)
s = append(s, 1)                              // ممکن است بازتخصیص کند
sub := s[1:3:4]                               // برش با cap مشخص

// map: جدول هش، ارجاعی، nil map قابل خواندن ولی نه نوشتن
m := map[string][]int{"a": {1, 2}}
v, ok := m["k"]                               // اصطلاح «comma ok»
delete(m, "a")
// ترتیب تکرار map عامدانه تصادفی است

// struct: نوع محصولی مقداری، با تگ برای سریال‌سازی
type User struct {
    ID    int64  `json:"id"`
    Name  string `json:"name"`
    _     struct{}                            // جلوگیری از ساخت بدون نام فیلد
}
type Admin struct {
    User                                      // جاسازی (embedding) — نه وراثت
    Level int
}

// اینترفیس: تطابق ساختاری، مجموعه متد
type Reader interface { Read(p []byte) (n int, err error) }

// channel: نوع هم‌زمانی درجه‌یک
ch := make(chan int, 8)
var recvOnly <-chan int = ch

// اشاره‌گر — بدون محاسبه اشاره‌گر (به‌جز unsafe)
p := &User{}
```

#### مجموعه غایب و اصطلاح‌های جبرانی

| نبود | راهکار اصطلاحی |
|---|---|
| `Set` | `map[T]struct{}` (صفر بایت مقدار) یا `map[T]bool` |
| `Tuple` | چند مقدار بازگشتی: `func f() (int, error)` |
| نوع جمعی/ADT | `interface` با پیاده‌سازی‌های محدود + type switch؛ بدون بررسی جامع |
| `Option<T>` | `*T` (nil = نبود) یا `(T, bool)` |
| ارث‌بری | جاسازی struct + اینترفیس |
| بارگذاری عملگر | ندارد (طراحی عامدانه) |

#### جنریک (Go 1.18+)

```go
type Number interface { ~int | ~int64 | ~float64 }         // مجموعه نوع
func Sum[T Number](xs []T) T { var s T; for _, x := range xs { s += x }; return s }
func Map[T, U any](xs []T, f func(T) U) []U { /* ... */ }

type Stack[T any] struct { items []T }

// comparable و cmp.Ordered
func Index[T comparable](xs []T, want T) int { /* ... */ }
```

`maps` و `slices` در کتابخانه استاندارد (Go 1.21+) توابع جنریک `slices.Sort`, `slices.Contains`, `maps.Keys` را می‌دهند؛ از Go 1.23 iterator با `range over func` اضافه شد.

#### مقدار صفر (Zero Value) — مفهوم مرکزی

هر نوع در Go مقدار صفر مفیدی دارد: `0`, `""`, `false`, `nil` (برای اشاره‌گر، slice، map، channel، func، interface). `var x T` همیشه معتبر است و این طراحی، ساخت‌گرها را در بسیاری موارد حذف می‌کند. تله رایج: `nil` map برای نوشتن panic می‌دهد، ولی `nil` slice با `append` کار می‌کند.

---

### ۳٫۸ Rust

Rust سیستم نوع غنی‌ترین فهرست ما را دارد: ADT کامل، جنریک با trait bound، و **مالکیت/عمر** به‌عنوان بخشی از نوع.

#### انواع اسکالر

```rust
i8 i16 i32 i64 i128 isize
u8 u16 u32 u64 u128 usize
f32 f64                       // f16, f128 در مسیر پایدارسازی
bool
char                          // 4 بایت، یک Unicode scalar value
()                            // نوع unit — تک‌مقداری
!                             // نوع never — عبارتی که برنمی‌گردد
```

#### انواع مرکب

```rust
// tuple — محصولی بی‌نام
let t: (i32, f64, char) = (1, 2.0, 'x');
let (a, b, c) = t;            // تخریب
let unit = ();

// struct در سه شکل
struct Point { x: f64, y: f64 }       // نام‌دار
struct Wrapper(String);               // tuple struct — برای newtype
struct Marker;                        // unit struct — صفر بایت

// enum — نوع جمعی واقعی با داده
enum Shape {
    Circle { r: f64 },
    Rect(f64, f64),
    Empty,
}

// Option و Result — هسته مدل خطای Rust
enum Option<T> { Some(T), None }
enum Result<T, E> { Ok(T), Err(E) }

fn area(s: &Shape) -> f64 {
    match s {                                  // بررسی جامع اجباری
        Shape::Circle { r } => std::f64::consts::PI * r * r,
        Shape::Rect(w, h)   => w * h,
        Shape::Empty        => 0.0,
    }
}
```

**بهینه‌سازی نمایش نیچ (niche optimization):** `Option<Box<T>>`, `Option<&T>`, `Option<NonZeroU32>` هم‌اندازه نوع درونی هستند — یعنی `Option` سربار حافظه ندارد. این ویژگی، استفاده از `Option` را عملاً رایگان می‌کند.

#### آرایه، برش، رشته

```rust
let arr: [i32; 5] = [1, 2, 3, 4, 5];    // طول بخشی از نوع، روی پشته
let slice: &[i32] = &arr[1..4];         // {ptr, len} — قرض‌گیری بدون مالکیت
let v: Vec<i32> = vec![1, 2, 3];        // آرایه پویا روی heap
let s: String = String::from("سلام");    // UTF-8 با مالکیت
let sr: &str = "سلام";                  // برش رشته‌ای — UTF-8، بدون مالکیت
let b: &[u8] = s.as_bytes();
```

#### مجموعه‌های استاندارد

| نوع | پشت صحنه |
|---|---|
| `Vec<T>` | آرایه پویا پیوسته |
| `VecDeque<T>` | بافر حلقوی — صف دوسر O(1) |
| `LinkedList<T>` | لیست دوپیوندی (کم‌کاربرد) |
| `HashMap<K,V>` / `HashSet<T>` | hashbrown (SwissTable)، هشر پیش‌فرض SipHash-1-3 مقاوم به HashDoS |
| `BTreeMap<K,V>` / `BTreeSet<T>` | B-tree، مرتب، پیمایش بازه‌ای |
| `BinaryHeap<T>` | هرم بیشینه |
| `Cow<'a, T>` | Clone-on-Write: قرض‌گرفته یا صاحب |

#### انواع اشاره‌گر و مالکیت

```rust
&T          // ارجاع تغییرناپذیر — هر تعداد
&mut T      // ارجاع تغییرپذیر — انحصاری
Box<T>      // مالکیت یگانه روی heap
Rc<T>       // شمارش ارجاع تک‌ریسمانی
Arc<T>      // شمارش ارجاع اتمی — بین ریسمان‌ها
RefCell<T>  // تغییرپذیری داخلی، بررسی قرض در زمان اجرا
Cell<T>     // تغییرپذیری داخلی با کپی
Mutex<T> / RwLock<T>   // دسترسی هم‌زمان هم‌گام‌شده
Pin<P>      // تضمین عدم جابه‌جایی در حافظه (برای async)
*const T / *mut T      // اشاره‌گر خام — نیازمند unsafe
```

قاعده طلایی: **یا چند خواننده یا یک نویسنده، هرگز هر دو** — این قاعده در سطح نوع اعمال می‌شود و «مسابقه داده» را در Safe Rust غیرممکن می‌کند.

#### trait، جنریک و انواع سطح-نوع

```rust
trait Area { fn area(&self) -> f64; }
impl Area for Shape { fn area(&self) -> f64 { /* ... */ } }

fn largest<T: PartialOrd + Copy>(xs: &[T]) -> T { /* ... */ }
fn render(s: &impl Area) {}             // جنریک ایستا — monomorphization
fn render_dyn(s: &dyn Area) {}          // چندریختی پویا — vtable

// نوع مرتبط و GAT
trait Container { type Item; fn get(&self, i: usize) -> Option<&Self::Item>; }

// جنریک ثابت (const generics)
struct Matrix<const R: usize, const C: usize> { data: [[f64; C]; R] }

// الگوی newtype برای نوع نامی و امنیت واحد
struct Meters(f64);
struct Seconds(f64);
```

`#[repr(C)]`, `#[repr(transparent)]`, `#[repr(packed)]`, `#[repr(u8)]` چیدمان حافظه را برای FFI و بهینه‌سازی کنترل می‌کنند.

---

### ۳٫۹ Kotlin

Kotlin روی JVM اجرا می‌شود اما سیستم نوع خودش را دارد: null-safety در سطح زبان و تفکیک تغییرپذیری در مجموعه‌ها.

#### انواع پایه (همه شیء در سطح زبان)

```kotlin
Byte Short Int Long                 // بدون نوع بی‌علامت پیش‌فرض
UByte UShort UInt ULong             // انواع بی‌علامت (پایدار از 1.5)
Float Double
Boolean
Char                                // واحد UTF-16
String
Unit                                // معادل void — تک‌مقداری
Nothing                             // نوع تهی، زیرنوع همه انواع
Any / Any?                          // ریشه سلسله‌مراتب
```

کامپایلر در صورت امکان اینها را به بدوی‌های JVM تبدیل می‌کند؛ `Int?` اما به `Integer` باکس می‌شود.

#### null-safety

```kotlin
var a: String = "x"          // a = null خطای کامپایل
var b: String? = null        // تهی‌پذیر
val len = b?.length ?: 0     // فراخوانی ایمن + عملگر elvis
val forced = b!!.length      // NPE در صورت null
b?.let { println(it) }
```

#### مجموعه‌ها: تفکیک خواندنی/تغییرپذیر

```kotlin
val ro: List<Int> = listOf(1, 2, 3)               // اینترفیس فقط-خواندنی
val mu: MutableList<Int> = mutableListOf(1, 2)    // تغییرپذیر
val m: Map<String, Int> = mapOf("a" to 1)
val mm: MutableMap<String, Int> = mutableMapOf()
val s: Set<Int> = setOf(1, 2)
val arr: IntArray = intArrayOf(1, 2, 3)           // آرایه بدوی، بدون باکسینگ
val gen: Array<String> = arrayOf("a")
val seq: Sequence<Int> = sequenceOf(1, 2).map { it * 2 }   // تنبل
```

مهم: `List` تغییرناپذیر **نیست** — فقط اینترفیس آن متد تغییر ندارد؛ نمونه زیرین می‌تواند تغییرپذیر باشد. برای تغییرناپذیری واقعی از `kotlinx.collections.immutable` (`PersistentList`) استفاده کنید.

#### انواع مرکب

```kotlin
data class User(val id: Long, val name: String)   // equals/hashCode/copy/toString/componentN
val u2 = u1.copy(name = "Ada")
val (id, name) = u2                               // تخریب

sealed class Result<out T> {                      // ADT
    data class Ok<T>(val value: T) : Result<T>()
    data class Err(val error: Throwable) : Result<Nothing>()
}
sealed interface Shape                            // sealed interface — 1.5+
@JvmInline value class UserId(val raw: Long)      // نوع مقداری بدون سربار
enum class Color(val hex: Int) { RED(0xFF0000), GREEN(0x00FF00) }
object Singleton                                  // تک‌نمونه
typealias Handler = (Event) -> Unit

val pair = Pair("a", 1); val triple = Triple(1, 2, 3)   // tuple محدود
```

- Kotlin نوع tuple عمومی ندارد؛ فقط `Pair` و `Triple`. توصیه اصطلاحی: `data class` با نام فیلد.
- `when` روی `sealed` بررسی جامع می‌دهد (وقتی به‌عنوان عبارت استفاده شود).
- واریانس صریح: `out T` (هم‌وند/covariant)، `in T` (پادوند/contravariant)، `*` (star projection).
- **انواع هوشمند (smart cast):** پس از `if (x is String)` نوع `x` در آن بلوک `String` است.
- `Result<T>` داخلی برای بسته‌بندی موفقیت/استثنا؛ `runCatching { }`.
- Kotlin Multiplatform: `expect`/`actual` برای نوع‌های پلتفرم‌وابسته.

---

### ۳٫۱۰ Swift

Swift مدل «انواع مقداری به‌عنوان پیش‌فرض» با کپی-در-نوشتن (CoW) را همراه با ADT کامل ارائه می‌کند.

#### انواع پایه

```swift
Int Int8 Int16 Int32 Int64 Int128            // Int128/UInt128 از Swift 6
UInt UInt8 ... UInt64 UInt128
Float16 Float Float80 Double
Bool
Character                                     // خوشه گرافیمی توسعه‌یافته
String / Substring
Void = ()
Never                                         // نوع تهی
Any / AnyObject / AnyHashable
```

#### مجموعه‌های داخلی — سه‌گانه اصلی

```swift
var a: [Int] = [1, 2, 3]                      // Array<Int> — مقداری با CoW
var d: [String: Int] = ["a": 1]               // Dictionary — نامرتب
var s: Set<Int> = [1, 2, 3]                   // Set — عضو باید Hashable
let slice: ArraySlice<Int> = a[1...]          // نمای بدون کپی
let cs = ContiguousArray<Int>()               // تضمین حافظه پیوسته
```

#### tuple، struct، enum

```swift
// tuple — با برچسب نام، نوع درجه‌یک (اما نه Hashable/Codable خودکار)
let point: (x: Double, y: Double) = (x: 1, y: 2)
let (a, b) = (1, 2)
func minMax(_ xs: [Int]) -> (min: Int, max: Int)? { /* ... */ }

// struct — مقداری، پیش‌فرض ترجیحی
struct Point: Hashable, Codable, Sendable {
    var x, y: Double
    mutating func scale(_ f: Double) { x *= f; y *= f }
}

// enum با payload — ADT کامل
enum Shape {
    case circle(radius: Double)
    case rect(w: Double, h: Double)
    indirect case group([Shape])              // بازگشتی نیازمند indirect
}

// Optional یک enum معمولی است
enum Optional<Wrapped> { case none, some(Wrapped) }
var name: String? = nil
if let n = name { }                           // اتصال اختیاری
guard let n = name else { return }
let len = name?.count ?? 0
let forced = name!                            // crash در صورت nil

// Result
enum Result<Success, Failure: Error> { case success(Success), failure(Failure) }
```

#### پروتکل‌ها و انواع مبتنی بر قابلیت

```swift
protocol Drawable { func draw() }
protocol Container { associatedtype Item; var count: Int { get } }

func render(_ d: some Drawable) {}             // جنریک مات (opaque) — Swift 5.7
func render(_ d: any Drawable) {}              // وجودی (existential) — جعبه پویا
func make() -> some Collection { [1, 2, 3] }   // نوع بازگشتی مات

// property wrapper، نوع‌های ساختاری‌شده
@propertyWrapper struct Clamped<T: Comparable> { /* ... */ }
```

- پروتکل‌های پرکاربرد: `Equatable`, `Hashable`, `Comparable`, `Codable` (= `Encodable & Decodable`), `Identifiable`, `Sendable`, `Sequence`, `Collection`, `RandomAccessCollection`.
- `Sendable` و `~Copyable`/`~Escapable` (انواع غیرقابل‌کپی، Swift 5.9+) مدل مالکیت را به Swift آورده‌اند — نزدیک شدن آشکار به Rust.
- `class` برای معنای ارجاعی؛ `actor` برای ایزوله‌سازی حالت هم‌زمان؛ `@MainActor` برای انحصار ریسمان اصلی.
- `Decimal`, `Measurement<UnitType>`, `Date`, `UUID`, `Data` از Foundation.

---

### ۳٫۱۱ Dart

Dart سیستم نوع sound (سالم) با null-safety کامل از نسخه ۲٫۱۲ دارد و از نسخه ۳ رکورد و الگوها را افزود.

```dart
// انواع پایه — همه شیء، همه زیرنوع Object
int          // ۶۴ بیتی روی VM؛ روی وب به double جاوااسکریپت نگاشت می‌شود
double       // IEEE-754 binary64
num          // ابرنوع int و double
bool String
Runes        // دنباله code point
Symbol
BigInt       // صحیح نامحدود
Object / Object? / dynamic / void / Never / Null

// مجموعه‌ها
List<int> l = [1, 2, 3];                  // آرایه رشدپذیر؛ List.filled ثابت
Set<int> s = {1, 2};
Map<String, int> m = {'a': 1};
final fixed = List<int>.filled(3, 0);
const frozen = [1, 2, 3];                 // ثابت زمان کامپایل، عمیقاً تغییرناپذیر
final imm = List.unmodifiable(l);
Iterable<int> lazy = l.map((x) => x * 2);  // تنبل
Int32List typed = Int32List(10);           // dart:typed_data
Uint8List bytes = Uint8List(1024);

// null safety
String? maybe;
int len = maybe?.length ?? 0;
late final String lazyInit;                // مقدار‌دهی به‌تأخیر با تضمین
String sure = maybe!;

// رکورد و tuple — Dart 3
(int, String) pair = (1, 'a');
({int x, int y}) named = (x: 1, y: 2);
var (a, b) = pair;                         // تخریب
(int, String) f() => (200, 'OK');          // چند بازگشتی واقعی

// کلاس‌های داده و ADT
sealed class Shape {}
final class Circle extends Shape { final double r; Circle(this.r); }
final class Rect extends Shape { final double w, h; Rect(this.w, this.h); }

double area(Shape s) => switch (s) {        // عبارت switch با بررسی جامع
  Circle(r: var r) => 3.14159 * r * r,
  Rect(w: var w, h: var h) => w * h,
};

enum Status { active, inactive; bool get isOn => this == Status.active; }
extension type UserId(int raw) {}           // نوع پوششی بدون سربار — Dart 3.3
typedef Json = Map<String, dynamic>;
```

- اصلاح‌کننده‌های کلاس Dart 3: `sealed`, `final`, `base`, `interface`, `mixin` — کنترل دقیق ارث‌بری و پیاده‌سازی.
- `Future<T>` و `Stream<T>` انواع async درجه‌یک.
- `dynamic` بررسی نوع را به زمان اجرا موکول می‌کند؛ `Object?` گزینه ایمن معادل است.

---

### ۳٫۱۲ Ruby

**فلسفه:** همه چیز شیء، حتی `nil` و اعداد. تایپ پویا و اردکی، با سیستم نوع اختیاری بیرونی (RBS + Steep/Sorbet).

```ruby
# انواع عددی
42                  # Integer — دقت نامحدود (Fixnum/Bignum از 2.4 یکی شدند)
3.14                # Float — binary64
Rational(1, 3)      # عدد گویا دقیق
Complex(1, 2)       # مختلط
BigDecimal("0.1")   # اعشاری دقیق (کتابخانه استاندارد)

# انواع دیگر
"text"              # String — تغییرپذیر! (مگر frozen_string_literal یا .freeze)
:symbol             # Symbol — شناسه تغییرناپذیر و درون‌گزین‌شده (interned)
true / false        # TrueClass / FalseClass
nil                 # NilClass — تک‌نمونه
(1..10)             # Range — شامل؛ (1...10) انحصاری؛ (1..) بی‌کران
/regex/             # Regexp
->(x) { x * 2 }     # Proc (lambda)
Data.define(:x, :y) # نوع محصولی تغییرناپذیر — Ruby 3.2
Struct.new(:x, :y)  # نوع محصولی تغییرپذیر، با keyword_init اختیاری
```

#### مجموعه‌ها

```ruby
arr = [1, "two", :three]           # Array — ناهمگن، پویا
h   = { name: "Ada", age: 36 }     # Hash — ترتیب درج حفظ می‌شود
h.default = 0                      # مقدار پیش‌فرض
Hash.new { |hash, k| hash[k] = [] }  # بلوک پیش‌فرض
require 'set'; s = Set[1, 2, 3]    # Set — بر پایه Hash
arr.frozen?                        # تغییرناپذیری با freeze
Comparable / Enumerable            # ماژول‌های میکس‌این که رفتار نوع را می‌سازند
ObjectSpace::WeakMap               # نگاشت ضعیف
```

#### انواع‌سازی و الگوها

```ruby
# Data — رکورد تغییرناپذیر (3.2+)
Point = Data.define(:x, :y)
p1 = Point.new(x: 1, y: 2)
p2 = p1.with(y: 5)

# تطبیق الگو (2.7+/3.0)
case config
in { db: { host: String => host, port: Integer => port } }
  connect(host, port)
in [Integer => a, Integer => b, *rest]
  # ...
end

# نوع‌دهی ایستا اختیاری
# sig { params(x: Integer).returns(String) }   # Sorbet
# def f(x); end
```

- `Symbol` در برابر `String`: نماد درون‌گزین و تغییرناپذیر است و برای کلید و شناسه استفاده می‌شود؛ رشته‌ها داده‌اند.
- `Struct` و `Data` تنها انواع محصولی سبک زبان‌اند؛ tuple اختصاصی وجود ندارد و از آرایه استفاده می‌شود.
- `method_missing`، `define_method` و باز بودن کلاس‌ها (monkey patching) یعنی «نوع» در Ruby یک مجموعه رفتار قابل تغییر در زمان اجراست، نه یک برچسب ثابت.

---

### ۳٫۱۳ PHP

```php
// انواع اسکالر
int          // پلتفرم‌وابسته (۶۴ بیت معمول)؛ سرریز → float
float        // binary64
string       // دنباله بایت، بدون کدگذاری داخلی — mbstring برای یونیکد
bool

// انواع مرکب
array        // ساختار دوگانه: لیست مرتب + نگاشت انجمنی در یک نوع
object / stdClass
callable
iterable     // Traversable|array
null
resource     // دسته منبع (در حال کنار گذاشته شدن)

// اعلان نوع مدرن
declare(strict_types=1);

function f(int|string $x): ?array {}        // نوع اجتماعی (۸٫۰) + تهی‌پذیر
function g(Countable&ArrayAccess $x): void {}  // نوع تقاطعی (۸٫۱)
function h(): never {}                      // ۸٫۱
function k(): static|self|parent {}
```

#### آرایه — نوع مرکزی و دوگانه PHP

```php
$list  = [1, 2, 3];                      // کلیدهای 0,1,2
$assoc = ['name' => 'Ada', 'age' => 36]; // نگاشت
$mixed = [0 => 'a', 'k' => 'b'];         // هر دو هم‌زمان
$list[] = 4;                             // افزودن
// کلید فقط int یا string؛ "1" به 1 تبدیل می‌شود (نرمال‌سازی کلید)
// معنای مقداری با کپی-در-نوشتن؛ &$arr برای ارجاع
```

PHP نوع `Map`, `Set`, `Tuple` داخلی ندارد. جایگزین‌ها:

| نیاز | راهکار |
|---|---|
| Map با کلید شیء | `SplObjectStorage`, `WeakMap` (۸٫۰) |
| مجموعه | `array_unique`، کلیدهای آرایه، یا `Ds\Set` (افزونه ds) |
| ساختار داده کارآمد | `SplFixedArray`, `SplDoublyLinkedList`, `SplStack`, `SplQueue`, `SplPriorityQueue`, `SplHeap`, یا افزونه `ds` (`Ds\Vector`, `Ds\Map`, `Ds\Deque`) |
| Tuple | `array` یا `list($a, $b) = f()` یا `[$a, $b] = f()` |
| عدد دقیق | `bcmath`, `gmp` |

#### انواع مدرن سطح زبان

```php
enum Status: string {                        // enum پشتیبانی‌شده — ۸٫۱
    case Active = 'active';
    case Banned = 'banned';
    public function label(): string { return ucfirst($this->value); }
}

final class Point {                          // ۸٫۱ readonly، ۸٫۲ readonly class
    public function __construct(
        public readonly float $x,            // ارتقای پارامتر سازنده — ۸٫۰
        public readonly float $y,
    ) {}
}

$r = $obj?->method()?->prop;                 // زنجیره ایمن null — ۸٫۰
$v = match(true) { $n < 0 => 'neg', default => 'pos' };   // match — ۸٫۰
// property hooks و asymmetric visibility — ۸٫۴
```

---

### ۳٫۱۴ Scala

Scala یکی از غنی‌ترین سیستم‌های نوع صنعتی را دارد: ترکیب شیءگرایی و تابعی، انواع بالاتر-مرتبه، و در Scala 3 انواع اجتماعی/تقاطعی و match types.

```scala
// انواع مقداری (نگاشت به بدوی‌های JVM)
Byte Short Int Long Float Double Char Boolean Unit
// سلسله‌مراتب
Any            // ریشه همه
  AnyVal       // انواع مقداری
  AnyRef       // = java.lang.Object
Nothing        // زیرنوع همه — نوع تهی
Null           // زیرنوع همه AnyRef
```

#### مجموعه‌ها — سلسله‌مراتب دوگانه immutable/mutable

```scala
import scala.collection.{immutable => im, mutable => mu}

// تغییرناپذیر (پیش‌فرض، در scope خودکار)
val l  = List(1, 2, 3)              // لیست پیوندی تک‌سویه — prepend O(1)
val v  = Vector(1, 2, 3)            // درخت ۳۲-شاخه — دسترسی/به‌روزرسانی ~O(1)
val m  = Map("a" -> 1)              // HashMap پایدار (CHAMP)
val s  = Set(1, 2)
val ls = LazyList(1, 2, 3)          // تنبل (جانشین Stream)
val ar = ArraySeq(1, 2, 3)
val q  = im.Queue(1, 2)
val ts = im.TreeMap(1 -> "a")       // مرتب

// تغییرپذیر
val ab = mu.ArrayBuffer(1, 2)
val hm = mu.HashMap("a" -> 1)
val ls2 = mu.ListBuffer[Int]()

// آرایه جاوا
val arr: Array[Int] = Array(1, 2, 3)   // آرایه واقعی JVM
```

#### انواع محصولی، جمعی و ویژگی‌های سطح-نوع

```scala
// tuple تا ۲۲ عضو؛ در Scala 3 نوع tuple نامتناهی و heterogeneous list
val t: (Int, String, Double) = (1, "a", 2.0)
val (a, b, c) = t
t._1

// case class — محصولی تغییرناپذیر با equals/hashCode/copy/unapply
case class Person(name: String, age: Int)
val p2 = p1.copy(age = 31)

// ADE با enum (Scala 3) یا sealed trait (Scala 2)
enum Shape:
  case Circle(r: Double)
  case Rect(w: Double, h: Double)

sealed trait Tree[+A]
case class Leaf[A](v: A) extends Tree[A]
case class Node[A](l: Tree[A], r: Tree[A]) extends Tree[A]

// انواع کاربردی
Option[A]        // Some / None
Either[L, R]     // Left / Right
Try[A]           // Success / Failure
Future[A]

// امکانات نوع Scala 3
type Id = Int                              // نام مستعار
opaque type UserId = Long                   // نوع مات — فقط در scope تعریف شفاف
type Num = Int | Double                     // نوع اجتماعی
type Both = Serializable & Cloneable        // نوع تقاطعی
type Elem[X] = X match                      // match type
  case List[t] => t
  case _       => X
case class Meters(v: Double) extends AnyVal // کلاس مقداری (unboxed)

// جنریک با واریانس و کرانه
class Box[+A]                                // هم‌وند
class Sink[-A]                               // پادوند
def max[A <: Ordered[A]](xs: List[A]): A     // کرانه بالا
def f[A: Numeric](x: A)                      // کرانه context — پارامتر ضمنی

// انواع بالاتر-مرتبه (higher-kinded)
trait Monad[F[_]] { def flatMap[A, B](fa: F[A])(f: A => F[B]): F[B] }
```

- `opaque type` (Scala 3) پرکاربردترین ابزار برای امنیت نوع بدون هزینه زمان اجراست.
- **انواع مبتنی بر مقدار (path-dependent types)** و `given`/`using` (جانشین `implicit`) امکان برنامه‌نویسی سطح-نوع پیشرفته می‌دهند.

---

### ۳٫۱۵ Erlang

Erlang تنها **هشت نوع داده اصلی** دارد، همه تغییرناپذیر، با طراحی حول پیام‌رسانی و تحمل خطا.

| نوع | نمونه | توضیح |
|---|---|---|
| `integer` | `42`, `16#FF`, `$a` | **دقت نامحدود**؛ small integer در یک word، bignum روی heap |
| `float` | `3.14` | IEEE-754 binary64 |
| `atom` | `ok`, `error`, `'با فاصله'` | ثابت نام‌دار، درون‌گزین در atom table؛ مقایسه O(1). جدول اتم محدود است — ساخت پویای اتم خطرناک |
| `binary` / `bitstring` | `<<1,2,3>>`, `<<1:3>>` | دنباله بایت/بیت؛ کارآمد، قابل اشتراک بین فرایندها |
| `reference` | `make_ref()` | شناسه یکتای سراسری |
| `fun` | `fun(X) -> X*2 end` | تابع بی‌نام درجه‌یک |
| `port` | `open_port(...)` | ارتباط با دنیای بیرون |
| `pid` | `self()` | شناسه فرایند |
| `tuple` | `{ok, Value}` | **محصولی با اندازه ثابت**، دسترسی O(1) با `element/2` |
| `list` | `[1,2,3]`, `[H\|T]` | لیست پیوندی تک‌سویه؛ improper list هم مجاز |
| `map` | `#{key => value}` | نگاشت (از R17)؛ flatmap کوچک و hashmap بزرگ |

```erlang
%% الگوی مرکزی: tuple با برچسب اتم به‌عنوان نوع جمعی
-spec fetch(key()) -> {ok, value()} | {error, not_found}.

case fetch(K) of
    {ok, V}          -> V;
    {error, Reason}  -> handle(Reason)
end.

%% record — قند نحوی روی tuple
-record(user, {id :: integer(), name = "" :: string()}).
U = #user{id = 1, name = "Ada"},
U2 = U#user{name = "Grace"},
Id = U#user.id.

%% تطبیق باینری — نقطه قوت بی‌نظیر Erlang
<<Version:4, IHL:4, TOS:8, Len:16, Rest/binary>> = Packet.

%% typespec — برای dialyzer، نه کامپایلر
-type shape() :: {circle, number()} | {rect, number(), number()}.
```

- ترتیب کلی مقایسه در Erlang: `number < atom < reference < fun < port < pid < tuple < map < nil < list < bitstring`. این ترتیب، مرتب‌سازی هر مجموعه ناهمگنی را ممکن می‌کند.
- ماژول‌های ساختار داده: `array`, `dict` (قدیمی)، `sets`, `ordsets`, `gb_sets`, `gb_trees`, `orddict`, `queue`, `digraph`, `ets` (جدول درون‌حافظه‌ای با دسترسی هم‌زمان)، `dets`, `mnesia`.
- **Dialyzer** یک تحلیلگر نوع «موفقیت‌گرا» (success typing) است: فقط چیزهایی را گزارش می‌کند که قطعاً خطا هستند — برخلاف کامپایلرهای نوع سنتی که هر چیز غیرقابل‌اثبات را رد می‌کنند.

---

### ۳٫۱۶ Elixir

Elixir روی BEAM اجرا می‌شود و همان انواع Erlang را دارد، به‌علاوه لایه‌ای از انواع ساخته‌شده روی آنها.

```elixir
# انواع پایه (همان BEAM)
42                # Integer — نامحدود
3.14              # Float
:ok               # Atom (true/false/nil هم اتم‌اند!)
"سلام"            # String = binary با کدگذاری UTF-8
'legacy'          # charlist = لیست code point (سازگاری با Erlang)
<<1, 2, 3>>       # Binary / Bitstring
{:ok, value}      # Tuple
[1, 2, 3]         # List (پیوندی)
%{a: 1}           # Map
fn x -> x * 2 end # Function
self()            # PID
make_ref()        # Reference

# انواع ساخته‌شده روی Map
%User{name: "Ada"}                       # Struct = map با کلید __struct__
defmodule User do
  defstruct name: "", age: 0
  @type t :: %__MODULE__{name: String.t(), age: non_neg_integer()}
end

# Keyword list — لیست از tuple دوعضوی با کلید اتم
opts = [timeout: 5000, retries: 3]       # = [{:timeout, 5000}, {:retries, 3}]

# مجموعه و صف
MapSet.new([1, 2, 3])
:queue.new()
Range: 1..10 و 1..10//2
Stream.map([1,2,3], &(&1 * 2))           # تنبل، ترکیب‌پذیر
Enum.map([1,2,3], &(&1 * 2))             # حریص

# Protocol — چندریختی مبتنی بر نوع داده
defprotocol Size do
  def size(data)
end
defimpl Size, for: BitString do
  def size(s), do: byte_size(s)
end

# نوع اختیاری/نتیجه — اصطلاحی، نه نوع زبانی
{:ok, result} | {:error, reason}
case File.read(path) do
  {:ok, content} -> content
  {:error, :enoent} -> ""
end
with {:ok, a} <- step1(), {:ok, b} <- step2(a), do: {:ok, a + b}

# typespec
@spec area(Shape.t()) :: float()
@type shape :: {:circle, number()} | {:rect, number(), number()}
```

- تفاوت مهم: `Map` برای داده با کلید پویا، `Struct` برای داده با شکل معلوم، `Keyword` برای گزینه‌های تابع (تکراری و مرتب مجاز).
- `Access` behaviour + `get_in`/`put_in`/`update_in` برای کار با ساختارهای تودرتو.
- **مسیر آینده:** تیم Elixir در حال افزودن یک سیستم نوع مجموعه‌ای تدریجی (set-theoretic gradual typing) به کامپایلر است که از نسخه ۱٫۱۷ به بعد به‌تدریج فعال می‌شود — نوع‌های اجتماعی/تقاطعی بومی برای map و struct.

---

### ۳٫۱۷ Zig

Zig سیستم نوعی دارد که در آن **انواع، مقادیر زمان کامپایل هستند** (`comptime`)؛ همین یک ایده، جنریک، reflection و metaprogramming را یک‌جا حل می‌کند.

#### انواع بدوی

بر اساس [مستندات رسمی Zig](https://ziglang.org/documentation/master/):

| دسته | انواع |
|---|---|
| صحیح ثابت | `i8`, `u8`, `i16`, `u16`, `i32`, `u32`, `i64`, `u64`, `i128`, `u128` |
| هم‌اندازه اشاره‌گر | `isize`, `usize` |
| **صحیح با پهنای دلخواه** | هر `iN`/`uN` تا **۶۵۵۳۵ بیت** — مثل `u3`, `i7`, `u1000` |
| سازگاری C | `c_char`, `c_short`, `c_ushort`, `c_int`, `c_uint`, `c_long`, `c_ulong`, `c_longlong`, `c_ulonglong`, `c_longdouble` |
| شناور | `f16`, `f32`, `f64`, `f80`, `f128` |
| منطقی | `bool` |
| ویژه | `anyopaque` (معادل `void` در C، برای اشاره‌گر نوع-پاک‌شده), `noreturn`, `type` (نوعِ نوع‌ها), `anyerror`, `comptime_int`, `comptime_float`, `void` |

`comptime_int` و `comptime_float` انواع لیترال‌ها هستند و **فقط در زمان کامپایل** وجود دارند — دقت نامحدود دارند و سپس به نوع مقصد تبدیل می‌شوند. مقادیر بدوی ویژه: `true`, `false`, `null`, `undefined`.

#### انواع مرکب

```zig
const std = @import("std");

// آرایه و برش
const arr: [5]i32 = .{ 1, 2, 3, 4, 5 };     // طول بخشی از نوع
const slice: []const i32 = arr[1..4];        // {ptr, len}
const sentinel: [:0]const u8 = "hello";      // برش با نگهبان — رشته‌ها

// انواع اشاره‌گر — بسیار دقیق‌تر از C
var x: i32 = 5;
const p: *i32 = &x;              // اشاره‌گر تک‌عضوی
const mp: [*]i32 = &arr;         // اشاره‌گر چندعضوی
const sp: [*:0]u8 = undefined;   // اشاره‌گر با نگهبان
const op: ?*i32 = null;          // اشاره‌گر اختیاری — nullable صریح

// struct — با کنترل چیدمان
const Point = struct {
    x: f64 = 0,                  // مقدار پیش‌فرض
    y: f64 = 0,
    pub fn len(self: Point) f64 { return @sqrt(self.x*self.x + self.y*self.y); }
};
const Packed = packed struct { a: u3, b: u5 };   // چیدمان بیتی دقیق
const Extern = extern struct { a: c_int };       // ABI سازگار با C

// enum و union — نوع جمعی نوع-ایمن
const Color = enum(u8) { red = 1, green, blue };
const Shape = union(enum) {                  // tagged union
    circle: f64,
    rect: struct { w: f64, h: f64 },
    empty: void,
};
fn area(s: Shape) f64 {
    return switch (s) {                      // بررسی جامع اجباری
        .circle => |r| std.math.pi * r * r,
        .rect => |d| d.w * d.h,
        .empty => 0,
    };
}

// نوع اختیاری و اتحاد خطا — دو ستون مدل خطای Zig
var maybe: ?i32 = null;
if (maybe) |v| { _ = v; }
const value = maybe orelse 0;

const FileError = error{ NotFound, PermissionDenied };
fn read(path: []const u8) FileError![]u8 { ... }   // error union
const data = try read("f.txt");                     // انتشار خطا
const data2 = read("f.txt") catch &[_]u8{};         // مقدار جایگزین

// جنریک با comptime — نوع به‌عنوان پارامتر
fn List(comptime T: type) type {
    return struct { items: []T, len: usize };
}
const IntList = List(i32);

// وکتور SIMD
const V = @Vector(4, f32);
```

#### مجموعه‌ها در کتابخانه استاندارد

Zig مجموعه داخلی زبانی ندارد؛ همه در `std` و همه **مدیریت حافظه صریح با allocator**:

`std.ArrayList(T)`, `std.ArrayListUnmanaged(T)`, `std.MultiArrayList(T)` (چیدمان SoA), `std.AutoHashMap(K,V)`, `std.StringHashMap(V)`, `std.ArrayHashMap` (ترتیب درج), `std.AutoArrayHashMap`, `std.BoundedArray(T,N)`, `std.SinglyLinkedList`, `std.DoublyLinkedList`, `std.PriorityQueue(T)`, `std.EnumArray`, `std.StaticBitSet`, `std.SegmentedList`.

برای مجموعه (`Set`) اصطلاح رایج `std.AutoHashMap(T, void)` است.

---

### ۳٫۱۸ Carbon

Carbon زبان تجربی گوگل به‌عنوان «جانشین C++» است و **هنوز در مرحله طراحی/آزمایشی است — برای تولید آماده نیست**. سیستم نوع آن بر اساس [سند طراحی رسمی](https://docs.carbon-lang.dev/docs/design/):

#### انواع بدوی

| رده | نام‌ها | مشخصات |
|---|---|---|
| منطقی | `bool` | دقیقاً دو مقدار `true`/`false`؛ هر سه کلیدواژه‌اند. شرط‌های `if`/`while` و عبارت `if-then-else` مقدار `bool` می‌گیرند |
| صحیح علامت‌دار | `iN` با N مضرب مثبت ۸ | سرریز **خطای برنامه‌نویسی** است: در build توسعه فوراً در زمان اجرا گرفته می‌شود؛ در build کارایی بهینه‌ساز می‌تواند فرض کند رخ نمی‌دهد (در غیر این صورت رفتار نامعین)؛ در build سخت‌شده برنامه abort می‌شود یا نتیجه ریاضی نادرست (مکمل دو یا صفر) تولید می‌شود |
| صحیح بی‌علامت | `uN` با N مضرب مثبت ۸ | در سرریز **می‌پیچد**. مستندات اکیداً توصیه می‌کند فقط جایی استفاده شود که معنای پیچش مطلوب است: دست‌کاری بیت، حساب پیمانه‌ای، هش، رمزنگاری، PRNG. برای مقادیری که منفی نمی‌شوند ولی پیچش بی‌معناست (مثل اندازه) از نوع علامت‌دار استفاده کنید |
| شناور IEEE-754 | `fN` با N مضرب ۸ | معنای IEEE-754، گردکردن به نزدیک‌ترین، بدون تنظیم وضعیت استثنای ممیز شناور. `f16`, `f32`, `f64` همیشه موجودند؛ `f80`, `f128`, `f256` بسته به پلتفرم |
| شناور ویژه | `BFloat16` | برش ۱۶ بیتی از قالب binary32 |
| رشته | `String`, `StringView` | UTF-8 |

**لیترال‌ها در Carbon نوع خاص خود را دارند:** لیترال صحیح نوعش از مقدارش مشتق می‌شود و به هر نوعی که آن مقدار را نمایش دهد به‌طور ضمنی تبدیل می‌شود — پسوند نوع وجود ندارد. لیترال‌ها حساس به حروف‌اند: `0x`, `0o`, `0b` باید کوچک و ارقام hex باید بزرگ باشند. `_` جداکننده رقم است. تقسیم ممکن است به‌دلیل محدودیت LLVM به حداکثر ۱۲۸ بیت محدود باشد.

#### انواع مرکب

```carbon
// tuple
var t: (i32, String) = (1, "a");
var x: i32 = t.0;

// struct type — نوع ساختاری با فیلد نام‌دار
var s: {.x: i32, .y: i32} = {.x = 1, .y = 2};

// class — نوع نامی
class Point {
  var x: f64;
  var y: f64;
  fn Length[self: Self]() -> f64;
}

// choice — نوع جمعی (معادل enum در Rust)
choice Shape {
  Circle(r: f64),
  Rect(w: f64, h: f64),
  Empty
}

// آرایه و برش
var a: array(i32, 5) = (1, 2, 3, 4, 5);

// اشاره‌گر و اختیاری
var p: i32* = &x;
var maybe: Optional(i32) = None;

// جنریک با interface و constraint
fn Sum[T:! Addable](xs: Slice(T)) -> T;
interface Addable { fn Op[self: Self](other: Self) -> Self; }
```

- Carbon تمایز `let` (ثابت) و `var` (متغیر) دارد و پارامترهای جنریک با `:!` مشخص می‌شوند (زمان کامپایل).
- انواع مجموعه‌ای در کتابخانه هستند، نه زبان؛ بخش بزرگی از کتابخانه استاندارد هنوز طراحی نشده است.
- هدف اصلی: **دوسویگی کامل با C++** — یعنی همه انواع C++ قابل استفاده مستقیم در Carbon و برعکس.

> **هشدار عملی:** Carbon هدف ۲۰۲۶–۲۰۲۷ را برای نسخه ۰٫۱ قابل استفاده اعلام کرده و صریحاً می‌گوید در حال حاضر برای پروژه واقعی مناسب نیست. جزئیات بالا ممکن است تغییر کنند.

---

### ۳٫۱۹ Gleam

Gleam یک زبان تابعی با تایپ ایستا و **استنباط نوع کامل** است که به Erlang (BEAM) و JavaScript کامپایل می‌شود. سیستم نوع آن sound است و `null` و استثنا ندارد.

#### انواع داخلی

| نوع | نمونه | نکته |
|---|---|---|
| `Int` | `42`, `0b1010`, `0xFF` | دقت نامحدود روی BEAM؛ روی JS به `BigInt`/`Number` نگاشت می‌شود |
| `Float` | `3.14` | binary64؛ **هیچ تبدیل ضمنی با Int وجود ندارد** — عملگرها جدا هستند: `+` برای Int و `+.` برای Float |
| `String` | `"سلام"` | UTF-8، تغییرناپذیر؛ الحاق با `<>` |
| `Bool` | `True`, `False` | در واقع یک نوع سفارشی با دو variant |
| `Nil` | `Nil` | مقدار «هیچ» — نه null؛ نوع بازگشتی توابع بدون نتیجه |
| `List(a)` | `[1, 2, 3]` | لیست پیوندی تک‌سویه، همگن، تغییرناپذیر؛ `[head, ..tail]` |
| `Tuple` | `#(1, "Hi!")` | نوع جنریک با پارامتر نوع برای اعضا |
| `BitArray` | `<<1, 2, 3>>` | دنباله بیت — از BEAM |
| `Result(a, e)` | `Ok(v)` / `Error(e)` | مدل خطای زبان؛ استثنا وجود ندارد |
| `Option(a)` | `Some(v)` / `None` | در `gleam/option` |
| `Dict(k, v)` | `dict.from_list([...])` | در `gleam/dict` |
| `Set(a)` | `set.from_list([...])` | در `gleam/set` |
| `fn(a) -> b` | `fn(x) { x * 2 }` | تابع درجه‌یک |

بر اساس [تور زبان Gleam](https://tour.gleam.run/data-types/tuples/)، Tuple برای ترکیب چند مقدار از انواع مختلف است، گزینه‌ای سریع و راحت، یک نوع جنریک با پارامتر نوع، و بیشتر برای بازگرداندن ۲ یا ۳ مقدار از یک تابع استفاده می‌شود — با این توصیه که در بسیاری موارد **نوع سفارشی روشن‌تر از tuple است**. دسترسی با `some_tuple.0` و `some_tuple.1` بدون نیاز به تطبیق الگو انجام می‌شود.

```gleam
// انواع سفارشی — محصولی و جمعی در یک ساختار
pub type Shape {
  Circle(radius: Float)
  Rect(width: Float, height: Float)
  Empty
}

pub fn area(shape: Shape) -> Float {
  case shape {                      // بررسی جامع الزامی
    Circle(radius: r) -> 3.14159 *. r *. r
    Rect(width: w, height: h) -> w *. h
    Empty -> 0.0
  }
}

// رکورد با فیلد نام‌دار و به‌روزرسانی
pub type User { User(name: String, age: Int) }
let u2 = User(..u1, age: 31)

// نوع مات (opaque) — سازنده بیرون ماژول مخفی است
pub opaque type Positive { Positive(Int) }
pub fn new(n: Int) -> Result(Positive, Nil) {
  case n > 0 { True -> Ok(Positive(n)) False -> Error(Nil) }
}

// جنریک با استنباط کامل — بدون annotation هم کار می‌کند
pub fn map_first(pair: #(a, b), f: fn(a) -> c) -> #(c, b) {
  #(f(pair.0), pair.1)
}

// زنجیره Result با use
pub fn load() -> Result(Config, Error) {
  use raw <- result.try(read_file("cfg"))
  use parsed <- result.try(parse(raw))
  Ok(parsed)
}
```

- Gleam **نوع اجتماعی، ارث‌بری، بارگذاری عملگر، تبدیل ضمنی و null ندارد** — عامدانه. تنها راه چندریختی، جنریک و تابع درجه‌یک است.
- کتابخانه استاندارد Gleam برای هر دو هدف Erlang و JavaScript کار می‌کند و با Erlang/OTP 26+ و نسخه‌های پشتیبانی‌شده Node/Deno/Bun و مرورگرهای اصلی سازگار است ([مستندات gleam_stdlib](https://hexdocs.pm/gleam_stdlib/)).
- برای تعامل با Erlang/Elixir از `external` و `Dynamic` + `decode` استفاده می‌شود — یعنی داده بی‌نوع در مرز سیستم اعتبارسنجی می‌شود.

---

### ۳٫۲۰ Haskell

Haskell قوی‌ترین سیستم نوع فهرست ماست: خالص، تنبل، با استنباط Hindley-Milner گسترش‌یافته و typeclassها.

#### انواع پایه

```haskell
-- صحیح
Int        -- حداقل ۶۴ بیت، ثابت، سریع
Integer    -- دقت نامحدود
Word       -- بی‌علامت هم‌اندازه Int
Int8, Int16, Int32, Int64          -- Data.Int
Word8, Word16, Word32, Word64      -- Data.Word

-- شناور و عددی
Float      -- binary32
Double     -- binary64
Rational   -- = Ratio Integer، گویای دقیق
Complex a  -- Data.Complex
Fixed      -- Data.Fixed، ممیز ثابت

-- دیگر
Bool       -- data Bool = False | True
Char       -- یک Unicode code point
()         -- unit
String = [Char]                    -- لیست پیوندی کاراکتر — کند
Data.Text.Text                     -- رشته بسته‌بندی‌شده کارآمد
Data.ByteString.ByteString         -- بایت خام
```

#### انواع جبری داده — قلب Haskell

```haskell
-- نوع جمعی (sum)
data Shape = Circle Double
           | Rect Double Double
           | Empty

-- نوع محصولی با فیلد نام‌دار (record syntax)
data Person = Person { name :: String, age :: Int } deriving (Show, Eq, Ord)
p2 = p1 { age = 31 }                  -- به‌روزرسانی رکورد

-- جنریک (پارامتری)
data Maybe a  = Nothing | Just a
data Either e a = Left e | Right a
data Tree a   = Leaf | Node (Tree a) a (Tree a)

-- tuple تا ۶۲ عضو (عملاً تا ۳ استفاده می‌شود)
pair :: (Int, String)
triple :: (Int, String, Double)
fst, snd :: (a, b) -> a

-- newtype — پوشش بدون سربار زمان اجرا
newtype Meters = Meters Double
newtype Age = Age { unAge :: Int }

-- type alias
type Name = String
```

#### Typeclass — چندریختی موردی

```haskell
class Eq a where (==) :: a -> a -> Bool
class Eq a => Ord a where compare :: a -> a -> Ordering
class Show a where show :: a -> String
class Functor f where fmap :: (a -> b) -> f a -> f b
class Functor f => Applicative f
class Applicative m => Monad m where (>>=) :: m a -> (a -> m b) -> m b
class Foldable t; class Traversable t
class Semigroup a where (<>) :: a -> a -> a
class Semigroup a => Monoid a where mempty :: a
class Num a; class Integral a; class Fractional a; class Floating a
```

#### مجموعه‌ها

| نوع | ماژول | مشخصات |
|---|---|---|
| `[a]` | داخلی | لیست پیوندی تنبل؛ cons O(1)، اندیس O(n) |
| `Data.Vector.Vector a` | vector | آرایه پیوسته؛ `Unboxed`, `Storable`, `Mutable` |
| `Data.Map.Map k v` | containers | درخت متوازن اندازه‌دار، مرتب، پایدار، O(log n) |
| `Data.IntMap.IntMap v` | containers | درخت Patricia برای کلید `Int` — سریع‌تر |
| `Data.Set.Set a` | containers | درخت متوازن |
| `Data.HashMap.Strict.HashMap` | unordered-containers | HAMT — سریع‌تر برای کلید هش‌پذیر |
| `Data.Sequence.Seq a` | containers | finger tree — افزودن/برداشتن از دو سر O(1) |
| `Data.Array.Array i e` | array | آرایه با اندیس دلخواه `Ix` |

#### امکانات پیشرفته سطح نوع (GHC extensions)

```haskell
{-# LANGUAGE GADTs, DataKinds, TypeFamilies, RankNTypes #-}

-- GADT — نوع دقیق برای هر سازنده
data Expr a where
  IntLit  :: Int  -> Expr Int
  BoolLit :: Bool -> Expr Bool
  Add     :: Expr Int -> Expr Int -> Expr Int
  If      :: Expr Bool -> Expr a -> Expr a -> Expr a

eval :: Expr a -> a          -- نوع-ایمن بدون بررسی زمان اجرا
eval (IntLit n)  = n
eval (Add a b)   = eval a + eval b
eval (If c t e)  = if eval c then eval t else eval e

-- DataKinds + type-level nat: بردار با طول در نوع
data Vec (n :: Nat) a where
  VNil  :: Vec 0 a
  VCons :: a -> Vec n a -> Vec (n + 1) a

-- خانواده نوع (type family) — تابع در سطح نوع
type family Elem c
type instance Elem [a] = a

-- Rank-N types
applyTwice :: (forall a. a -> a) -> (Int, String) -> (Int, String)
```

- **تنبلی (laziness)** یعنی هر نوع در Haskell به‌طور بالقوه شامل «thunk» است؛ انواع `!Int` (strict field) و `Data.Map.Strict` برای کنترل آن وجود دارند.
- `IO a`, `ST s a`, `State s a`, `Reader r a`, `Writer w a`, `STM a` — انواعی که اثر (effect) را در سیستم نوع کدگذاری می‌کنند. این کار Haskell را از همه زبان‌های دیگر این فهرست جدا می‌کند: **حتی «انجام کار» هم یک نوع است**.

---

## ۴. مباحث عرضی و عمیق

### ۴٫۱ Tuple: یک اسم، پنج معنای متفاوت

| سطح پشتیبانی | زبان‌ها | توضیح |
|---|---|---|
| نوع زبانی درجه‌یک با تطبیق الگو | Rust, Swift, Haskell, Scala, Elixir, Erlang, Gleam, Python, Carbon, Dart 3 | tuple نوع واقعی است، در امضای تابع و تطبیق الگو کار می‌کند |
| نوع کتابخانه‌ای | C++ (`std::tuple`), C# (`ValueTuple` با قند نحوی), Java (بدون — `record`), Kotlin (`Pair`/`Triple`) | با محدودیت‌های ارگونومیک |
| تقلید با آرایه | JavaScript, PHP, Ruby | `[a, b]` + تخریب |
| فقط چند مقدار بازگشتی | Go | `func f() (int, error)` — نه نوع، بلکه ویژگی امضای تابع |
| وجود ندارد | C | فقط `struct` |

**قاعده عملی:** tuple برای مقدار بازگشتی محلی و کوتاه‌عمر خوب است. برای هر داده‌ای که از مرز API عبور می‌کند یا بیش از سه عضو دارد، نوع محصولی نام‌دار (`struct`/`record`/`data class`) گزینه درست است — چون نام فیلد، مستندسازی و ایمنی در برابر جابه‌جایی ترتیب می‌دهد.

### ۴٫۲ Map: تفاوت‌های عملکردی و معنایی که مهم‌اند

```
جدول هش (میانگین O(1)):  dict (Py), HashMap (Java/Rust/Kotlin), Dictionary (C#),
                          map (Go), Map (JS), unordered_map (C++), Hash (Ruby)
درخت متوازن (O(log n)):   TreeMap (Java), BTreeMap (Rust), std::map (C++),
                          Data.Map (Haskell), SortedDictionary (C#)
HAMT/CHAMP پایدار:        Map (Scala im), HashMap (Clojure), ImmutableDictionary (C#),
                          HashMap (Haskell unordered-containers), Map (Elixir بزرگ)
آرایه مسطح:               flat_map (C++23), ArrayHashMap (Zig), IndexMap (Rust)
```

پرسش‌هایی که پیش از انتخاب باید پاسخ دهید:

1. **ترتیب:** آیا به ترتیب درج یا ترتیب کلید نیاز دارید؟ `dict` پایتون و `Map` جاوااسکریپت ترتیب درج را تضمین می‌کنند؛ `map` در Go عامدانه تکرار را تصادفی می‌کند تا وابستگی به ترتیب شکل نگیرد؛ `HashMap` جاوا هیچ ضمانتی ندارد.
2. **مقاومت به HashDoS:** Rust پیش‌فرض SipHash استفاده می‌کند (کندتر ولی امن)، Go برای هر map یک seed تصادفی می‌گیرد، Java هیچ محافظتی ندارد (و درخت‌سازی سطل تنها اثر را کاهش می‌دهد).
3. **تساوی کلید:** `NaN` به‌عنوان کلید، `-0` در برابر `0`، `Integer` باکس‌شده در برابر `int`، و نرمال‌سازی کلید عددی-رشته‌ای در PHP و JavaScript همه منبع باگ‌اند.
4. **کلید تغییرپذیر:** اگر کلیدی را پس از درج تغییر دهید (مثلاً `List` به‌عنوان کلید در Java)، نگاشت خراب می‌شود. پایتون این را با الزام `hashable` بودن جلوگیری می‌کند؛ Rust با نیاز به `Hash + Eq` و مالکیت.

### ۴٫۳ Set: چه زمانی واقعاً یک نوع درجه‌یک است؟

- **بومی زبان/کتابخانه استاندارد:** Python (`set`/`frozenset`), JS (`Set`), Java, C#, Rust, Swift, Kotlin, Scala, Dart, Haskell, Elixir (`MapSet`), Gleam, Ruby, C++.
- **تقلید با نگاشت:** Go (`map[T]struct{}`), Zig (`AutoHashMap(T, void)`), C (دستی).
- **چندگانه (multiset/bag):** فقط C++ (`multiset`) و Scala (`Bag` در کتابخانه) نوع مستقیم دارند؛ در بقیه با `Map<T, Int>` یا `Counter` (پایتون) مدل می‌شود.
- **مجموعه بیتی:** `bitset<N>` در C++, `EnumSet` در Java, `StaticBitSet` در Zig, `BitSet` در Java/Scala — برای دامنه کوچک و متراکم، ده‌ها برابر کارآمدتر از hash set.

### ۴٫۴ صحیح و شناور: تله‌های مشترک همه زبان‌ها

**ممیز شناور:**
- `0.1 + 0.2 != 0.3` در هر زبانی که binary64 دارد — یعنی تقریباً همه.
- `NaN != NaN`. این باعث می‌شود `Float` در Rust فقط `PartialOrd` باشد نه `Ord`، و در Haskell `Ord Double` قانون totality را نقض کند.
- برای پول **هرگز** از شناور دودویی استفاده نکنید: `decimal` (C#), `BigDecimal` (Java/Scala), `Decimal` (Python/Swift), `bcmath`/`gmp` (PHP), نوع صحیح بر حسب کوچک‌ترین واحد (سنت/ریال) گزینه‌های درست‌اند.

**صحیح:**
- تقسیم صحیح در C/C++/Java/C#/Go/Rust به‌سمت صفر کوتاه می‌شود؛ در Python/Ruby `//` و `/` به‌سمت منفی بی‌نهایت (floor). `-7 / 2` می‌شود `-3` در Java و `-4` در Python.
- باقی‌مانده: `%` در C-family علامت مقسوم را می‌گیرد؛ در Python علامت مقسوم‌علیه. `-7 % 3` می‌شود `-1` در Java و `2` در Python.
- ارتقای عددی ضمنی در C/C++ (integer promotion) باعث می‌شود `uint8_t + uint8_t` نوع `int` بدهد؛ منبع باگ‌های ظریف.
- Go و Rust **هیچ تبدیل ضمنی عددی ندارند** — این پرحرفی به‌جای باگ است.

### ۴٫۵ چیدمان حافظه: چرا ترتیب فیلدها مهم است

```
struct Bad  { u8 a; u64 b; u8 c; }   // C/C++: 24 بایت با padding
struct Good { u64 b; u8 a; u8 c; }   // C/C++: 16 بایت
```

- **C, C++, Zig (`extern`/`packed`), Rust (`#[repr(C)]`)**: ترتیب فیلدها را حفظ می‌کنند؛ بهینه‌سازی دست شماست.
- **Rust (پیش‌فرض `#[repr(Rust)]`), Zig (پیش‌فرض), Swift**: کامپایلر آزاد است فیلدها را بازآرایی کند تا padding کم شود.
- **Java, C#, Python, Ruby, JS**: چیدمان شیء را نمی‌بینید؛ هر شیء header دارد (۸–۱۶ بایت) و فیلدهای ارجاعی اشاره‌گر هستند — باعث پراکندگی حافظه و کاهش محلیت cache.
- **الگوی SoA (Struct of Arrays):** `std.MultiArrayList` در Zig، `Vec<T>` جداگانه در Rust، `Vector` در Haskell/Julia — برای پیمایش‌های سنگین، چند برابر سریع‌تر از AoS.

### ۴٫۶ جنریک: چهار استراتژی پیاده‌سازی

| استراتژی | زبان‌ها | نتیجه |
|---|---|---|
| **Monomorphization** (تخصص‌سازی در زمان کامپایل) | Rust, C++, Swift (برای `some`), Zig (comptime), C# (انواع مقداری) | بدون سربار زمان اجرا، اندازه باینری بیشتر |
| **Type erasure** (پاک‌کردن نوع) | Java, Kotlin, Scala (JVM), TypeScript | یک کد برای همه، نیاز به boxing، `List<String>` در زمان اجرا `List` است |
| **Reified generics** (نوع در زمان اجرا موجود) | C#, Dart, Swift (برای `any`) | `typeof(T)` کار می‌کند، `List<int>` بدون boxing |
| **Dictionary passing** (عبور جدول نمونه) | Haskell (typeclass), Swift (protocol witness), Go (gcshape) | یک کد + جدول متد |

پیامد عملی: در Java نمی‌توانید `new T[]` بنویسید یا `instanceof List<String>` بسنجید؛ در C# می‌توانید. در Rust جنریک صفر-هزینه است ولی `dyn Trait` برای چندریختی پویا لازم است.

### ۴٫۷ انواع جبری داده و بررسی جامع (Exhaustiveness)

بررسی جامع — اینکه کامپایلر مطمئن شود همه حالت‌ها پوشش داده شده‌اند — احتمالاً تأثیرگذارترین ویژگی سیستم نوع بر کیفیت کد است.

| زبان | ADT | بررسی جامع |
|---|---|---|
| Rust | `enum` | ✅ اجباری |
| Haskell | `data` | ✅ با `-Wincomplete-patterns` |
| Swift | `enum` با payload | ✅ اجباری در `switch` |
| Scala 3 | `enum` / `sealed` | ✅ هشدار |
| Kotlin | `sealed class/interface` | ✅ برای `when` به‌عنوان عبارت |
| Java 21+ | `sealed` + `record` | ✅ در `switch` الگومحور |
| TypeScript | union تفکیک‌شده | ✅ با `never` exhaustive check |
| Zig | `union(enum)` | ✅ اجباری در `switch` |
| Dart 3 | `sealed class` | ✅ در `switch` عبارتی |
| Gleam | `type` با variant | ✅ اجباری |
| C++ | `std::variant` | ⚠️ جزئی (با `std::visit` و overload کامل) |
| Elixir/Erlang | tuple برچسب‌دار | ❌ فقط هشدار زمان اجرا / dialyzer |
| C# | (سلسله‌مراتب کلاس) | ⚠️ با `switch` الگومحور و `_` |
| Go | `interface` + type switch | ❌ هیچ |
| Python | `Union` + `match` | ⚠️ فقط با mypy/pyright |
| C | `union` + tag دستی | ❌ هیچ |

### ۴٫۸ انواع زمان و تاریخ — دسته‌ای که اغلب از قلم می‌افتد

| زبان | انواع کلیدی |
|---|---|
| Java | `Instant`, `LocalDate`, `LocalDateTime`, `ZonedDateTime`, `OffsetDateTime`, `Duration`, `Period`, `ZoneId` |
| C# | `DateTime`, `DateTimeOffset`, `DateOnly`, `TimeOnly`, `TimeSpan`, `TimeZoneInfo` |
| Python | `datetime`, `date`, `time`, `timedelta`, `timezone`, `zoneinfo.ZoneInfo` |
| Go | `time.Time`, `time.Duration`, `time.Location`, `time.Month` |
| Rust | `std::time::{Instant, SystemTime, Duration}` + `chrono`/`time` crate |
| Swift | `Date`, `DateComponents`, `TimeInterval`, `Calendar`, `Duration` |
| JS | `Date` (معیوب) → `Temporal` (`Temporal.Instant`, `PlainDate`, `ZonedDateTime`) |
| C++ | `chrono::system_clock`, `steady_clock`, `year_month_day`, `zoned_time` (C++20) |
| Elixir | `DateTime`, `NaiveDateTime`, `Date`, `Time`, `Duration` |
| Haskell | `Data.Time.{UTCTime, Day, TimeOfDay, NominalDiffTime}` |

قاعده مهم: **همیشه بین «لحظه مطلق» (`Instant`/`UTCTime`) و «تاریخ-ساعت محلی بدون منطقه» (`LocalDateTime`/`NaiveDateTime`) تمایز بگذارید.** ذخیره تاریخ تولد به‌عنوان `Instant` و ذخیره زمان یک رویداد به‌عنوان `LocalDate` هر دو باگ‌های کلاسیک‌اند.

### ۴٫۹ نوع در مرز سیستم: سریال‌سازی

هر سیستم نوعی در مرز I/O شکسته می‌شود. راهکارهای هر زبان:

| زبان | مکانیزم |
|---|---|
| Rust | `serde` با `#[derive(Serialize, Deserialize)]` — بررسی در زمان کامپایل |
| Swift | `Codable` — تولید خودکار کامپایلر |
| Go | تگ struct `json:"..."` + reflection |
| Java | Jackson/Gson با annotation؛ `record` سازگارتر |
| C# | `System.Text.Json` با source generator |
| Python | `pydantic` (اعتبارسنجی زمان اجرا از type hints), `dataclasses.asdict`, `attrs` |
| TypeScript | `zod`/`valibot` — طرح زمان اجرا که نوع ایستا از آن استنباط می‌شود (`z.infer`) |
| Haskell | `aeson` با `Generic` |
| Elixir | `Jason` + struct؛ اعتبارسنجی با `Ecto.Changeset` |
| Gleam | `gleam/dynamic` + decoder ترکیب‌پذیر — صریح‌ترین مدل |

الگوی طلایی: **اعتبارسنجی در مرز، سپس کار با نوع دقیق در درون.** یعنی `Map<String, Any>` ورودی را فوراً به `struct` تبدیل کنید، نه اینکه در سراسر برنامه dict خام پاس بدهید.

### ۴٫۱۰ تساوی، هش و ترتیب: قراردادهایی که باید نگه دارید

| زبان | تساوی مقداری | تساوی ارجاعی | قرارداد هش |
|---|---|---|---|
| Java | `equals()` | `==` | `equals` برابر ⟹ `hashCode` برابر |
| C# | `Equals()` / `==` قابل بارگذاری | `ReferenceEquals` | همان |
| Python | `__eq__` | `is` | `__hash__` سازگار با `__eq__`؛ تغییرپذیر ⟹ `__hash__ = None` |
| Rust | `PartialEq`/`Eq` | `ptr::eq` | `Hash` باید با `Eq` سازگار باشد |
| Go | `==` (ساختاری برای نوع قابل‌مقایسه) | مقایسه اشاره‌گر | map کلید را با `==` می‌سنجد |
| Swift | `Equatable` | `===` برای class | `Hashable` |
| JS | `===` (ارجاعی برای شیء) | همان | `Map` از SameValueZero استفاده می‌کند |
| Elixir/Erlang | `==` (با تبدیل عددی) و `===` (دقیق) | — | ساختاری |

نکته‌ای که اغلب فراموش می‌شود: در Go فقط انواع «قابل‌مقایسه» (comparable) می‌توانند کلید map باشند — slice، map و function نمی‌توانند. در Java قرار دادن شیء تغییرپذیر در `HashSet` و سپس تغییر آن، عضو را «گم» می‌کند.

### ۴٫۱۱ انواع و هم‌زمانی: چه چیزی را می‌توان به اشتراک گذاشت؟

| مکانیزم | زبان | توضیح |
|---|---|---|
| `Send` / `Sync` trait | Rust | کامپایلر مسابقه داده را در زمان کامپایل رد می‌کند |
| `Sendable` protocol | Swift | بررسی در حالت Strict Concurrency |
| تغییرناپذیری کامل | Erlang, Elixir, Haskell, Gleam | اشتراک همیشه ایمن است |
| `volatile`/`Atomic*` | Java, C#, C++, C | همگام‌سازی دستی |
| GIL | Python (تا ۳٫۱۲؛ `--disable-gil` اختیاری از ۳٫۱۳) | موازی‌سازی واقعی ریسمان محدود |
| channel + «اشتراک نکن، پیام بده» | Go | قرارداد فرهنگی، نه تضمین کامپایلر (race detector زمان اجرا) |
| Actor | Swift (`actor`), Elixir/Erlang (فرایند), Scala (Akka) | ایزوله‌سازی حالت |

Rust تنها زبان صنعتی این فهرست است که **ایمنی ریسمان را در سیستم نوع کدگذاری می‌کند**؛ `Rc<T>` عامدانه `Send` نیست و `Arc<T>` هست.

---

## ۵. الگوهای انتخاب نوع داده در عمل

### ۵٫۱ درخت تصمیم برای انتخاب مجموعه

```
به ترتیب نیاز دارید؟
├── نه، فقط عضویت و یکتایی      → Set (یا BitSet اگر دامنه کوچک و متراکم)
├── نه، نگاشت کلید→مقدار         → HashMap
└── بله
    ├── ترتیب درج + دسترسی با اندیس  → Array/Vector/List (آرایه پویا)
    ├── ترتیب کلید (مرتب)             → TreeMap/BTreeMap/SortedSet
    ├── ترتیب اولویت                  → PriorityQueue/BinaryHeap
    ├── افزودن/برداشتن از دو سر        → Deque/VecDeque
    └── درج/حذف زیاد در وسط           → LinkedList (به‌ندرت برنده واقعی است)

تغییرناپذیری لازم است؟
├── با اشتراک زیاد بین ریسمان‌ها  → ساختار پایدار (ImmutableList, PersistentMap, im crate)
└── فقط تضمین API                → اینترفیس فقط-خواندنی (List در Kotlin، ReadonlyArray در TS)
```

### ۵٫۲ نگاشت مفهوم دامنه به نوع درست

| مفهوم دامنه | انتخاب ضعیف (رایج) | انتخاب بهتر | دلیل |
|---|---|---|---|
| مبلغ پول | `float` / `double` | `Decimal` (Python)، `BigDecimal` (Java/Scala)، `decimal` (C#)، عدد صحیح از واحد خُرد (سِنت/ریال) | خطای دودویی شناور در جمع‌های مالی انباشته می‌شود |
| شناسه (ID) | `int` | نوع پوشش‌دار (`newtype`, `value class`, `struct`, `opaque type`) | جلوگیری از جابه‌جا شدن `UserId` و `OrderId` |
| شماره تلفن / کد پستی | `int` | `String` + اعتبارسنجی | صفر پیشوند و کاراکتر `+` معنادار است |
| تاریخ تولد | `Date`/`DateTime` | `LocalDate` / نوع بدون منطقه‌زمانی | تولد یک تاریخ تقویمی است، نه یک لحظه |
| زمان رویداد | `LocalDateTime` | `Instant` / `UTC timestamp` | لحظه مطلق باید بدون ابهام منطقه‌زمانی باشد |
| مقدار «شاید نبود» | `null` / مقدار جادویی (`-1`, `""`) | `Option`/`Maybe`/`?` | نبودِ مقدار باید در نوع دیده شود |
| نتیجه عملیات خطاپذیر | استثنا برای جریان معمول | `Result`/`Either`/`(value, error)` | خطای انتظارپذیر بخشی از امضای تابع است |
| مجموعه محدود حالت‌ها | رشته یا `int` ثابت | `enum` / نوع جمعی | بررسی جامع در زمان کامپایل |
| داده دودویی | `String` | `bytes`/`[]byte`/`Vec<u8>`/`BitArray` | رشته معنای کدگذاری دارد، بایت ندارد |
| واحد فیزیکی (متر، ثانیه) | `double` خام | نوع پوشش‌دار یا واحدهای نوع‌دار | جلوگیری از جمع متر با ثانیه |

### ۵٫۳ هفت اشتباه پرتکرار در کار با انواع داده

۱. **استفاده از شناور برای پول.** `0.1 + 0.2 != 0.3` در هر زبانی با IEEE‑754 دودویی. راه‌حل: نوع دسیمال یا عدد صحیح واحد خُرد.

۲. **فرض «یک کاراکتر = یک بایت = یک نویسه بصری».** در Python `len()` روی code point، در Java/C#/JS روی UTF‑16 code unit، در Rust/Go روی بایت می‌شمارد. برای «طول دیداری» باید grapheme cluster شمرد.

۳. **استفاده از نوع تغییرپذیر به‌عنوان کلید map یا مقدار پیش‌فرض پارامتر.** کلاسیک‌ترین نمونه `def f(x=[])` در Python و `HashMap` با کلیدی که `hashCode` آن تغییر می‌کند در Java.

۴. **نادیده گرفتن رفتار سرریز.** C/C++ (علامت‌دار) و Zig/Carbon رفتار نامعین یا خطا دارند؛ Java/C#/Go/Rust(release) بی‌صدا می‌پیچند؛ Python/Erlang/Elixir/Haskell(`Integer`) بزرگ می‌شوند. کد قابل حمل نمی‌تواند به یک رفتار تکیه کند.

۵. **کپی سطحی به‌جای عمیق.** `list.copy()`، `slice()`، `clone()` سطحی‌اند؛ اشیای درونی مشترک می‌مانند. اسلایس‌های Go و `ArraySlice` سوئیفت حتی بافر پشتی را مشترک نگه می‌دارند.

۶. **تکیه بر ترتیب map جایی که تضمین نشده.** Python `dict` و PHP `array` ترتیب درج را تضمین می‌کنند؛ Go `map` عامدانه ترتیب را تصادفی می‌کند؛ Java `HashMap` و Rust `HashMap` هیچ تضمینی نمی‌دهند.

۷. **نشتی نوع‌های مرزی به هسته دامنه.** `JSON`, `Map<String, dynamic>`, `any` و `interface{}` باید در لایه ورودی به انواع دامنه تبدیل (parse) شوند، نه در سراسر کد پخش.

### ۵٫۴ سه اصل راهنما

- **Parse، نه Validate.** ورودی بی‌ساختار را یک‌بار در مرز سیستم به نوع دقیق تبدیل کنید؛ پس از آن کامپایلر (یا تست‌ها) نامعتبر بودن را غیرممکن می‌کند.
- **حالت‌های غیرممکن را غیرقابل‌نمایش کنید.** اگر «کاربر تأییدشده همیشه ایمیل دارد»، دو حالت جداگانه در نوع جمعی بسازید، نه یک رکورد با فیلد اختیاری.
- **پیش‌فرض را تغییرناپذیر بگیرید.** تغییرپذیری را جایی اضافه کنید که سنجش عملکرد آن را ایجاب کند، نه به‌طور پیش‌فرض.

---

## ۶. جمع‌بندی

جدول زیر خلاصه‌ای از موضع هر زبان در سه محور تعیین‌کننده است: غنای سیستم نوع، مدل کنترل حافظه، و نحوه مدیریت نبودِ مقدار.

| زبان | سیستم نوع | کنترل حافظه | نبودِ مقدار |
|---|---|---|---|
| C | ضعیف، ایستا | کامل دستی | اشاره‌گر `NULL` |
| C++ | قوی‌تر، ایستا، قالب‌محور | دستی + RAII/smart pointer | `nullptr`, `std::optional` |
| Zig | ایستا، comptime به‌جای جنریک | دستی + allocator صریح | `?T` اجباری |
| Carbon | ایستا، جنریک بررسی‌شده | دستی، سازگار با C++ | `Optional(T)` کتابخانه‌ای |
| Rust | بسیار قوی، ADT + مالکیت | بدون GC، زمان کامپایل | `Option<T>`, `Result<T,E>` |
| Go | ساده و عمدی‌مینیمال | GC | مقدار صفر + `error` جداگانه |
| Java | قوی، nominal، erasure | GC | `null` + `Optional<T>` |
| C# | قوی، جنریک واقعی | GC | `T?` با تحلیل nullability |
| Kotlin | قوی، nullability در نوع | GC (JVM/Native) | `T?` اجباری |
| Scala | بسیار قوی، ADT + implicit | GC | `Option[A]` |
| Swift | قوی، ADT + value semantics | ARC (شمارش ارجاع) | `Optional<T>` اجباری |
| Dart | قوی، sound null safety | GC | `T?` |
| TypeScript | قوی اما ساختاری و erased | GC (زمان اجرای JS) | `undefined`/`null` + union |
| JavaScript | پویا، تبدیل ضمنی گسترده | GC | `undefined` و `null` |
| Python | پویا + انوتیشن اختیاری | GC (شمارش ارجاع + چرخه) | `None`, `Optional[T]` |
| Ruby | پویا، همه‌چیز شیء | GC | `nil` |
| PHP | پویا + نوع‌دهی تدریجی | GC | `null`, `?T` |
| Erlang | پویا، تغییرناپذیر | GC هر فرایند جدا | اتم `undefined`, tuple نتیجه |
| Elixir | پویا + typespec | GC هر فرایند جدا | `nil`, `{:ok, v}`/`{:error, r}` |
| Gleam | قوی، ADT، بدون null | GC (BEAM یا JS) | `Option`, `Result` |
| Haskell | بسیار قوی، تنبل، ADT | GC | `Maybe a`, `Either e a` |

روند کلی سه دهه گذشته روشن است: حرکت از «نوع به‌عنوان توصیف چیدمان حافظه» (C) به «نوع به‌عنوان اثبات درستی» (Rust, Haskell, Gleam). زبان‌های میانی (Kotlin, Swift, C#, Dart) همین ایده‌ها را — nullability در نوع، انواع جبری، تطبیق الگوی جامع، رکوردهای تغییرناپذیر — به اکوسیستم‌های صنعتی آورده‌اند. آشنایی با این تقسیم‌بندی‌ها نه صرفاً دانش نحوی است، بلکه ابزاری برای انتقال سریع بین زبان‌ها و انتخاب مدل‌سازی درست در هر کدام.

---

## ۷. منابع

مستندات رسمی مرجع، برای پیگیری دقیق‌ترین و به‌روزترین جزئیات هر زبان:

- انواع داخلی Python — [Python Standard Library: Built-in Types](https://docs.python.org/3/library/stdtypes.html)
- انواع Zig — [Zig Language Reference: Primitive Types](https://ziglang.org/documentation/master/#Primitive-Types)
- طراحی انواع Carbon — [Carbon Language Design Overview](https://docs.carbon-lang.dev/docs/design/)
- تور زبان Gleam — [Gleam Language Tour](https://tour.gleam.run/) و [Gleam Documentation](https://gleam.run/documentation/)
- کتابخانه استاندارد Gleam — [gleam_stdlib on HexDocs](https://hexdocs.pm/gleam_stdlib/)
- JavaScript/TypeScript — [MDN: JavaScript data types and structures](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Data_structures)، [TypeScript Handbook](https://www.typescriptlang.org/docs/handbook/intro.html)
- Java — [Java Language Specification, Chapter 4: Types, Values, and Variables](https://docs.oracle.com/javase/specs/jls/se21/html/jls-4.html)
- C# — [.NET: Types and members](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/built-in-types)
- C++ — [cppreference: Fundamental types](https://en.cppreference.com/w/cpp/language/types) و [Containers library](https://en.cppreference.com/w/cpp/container)
- Go — [The Go Programming Language Specification: Types](https://go.dev/ref/spec#Types)
- Rust — [The Rust Reference: Types](https://doc.rust-lang.org/reference/types.html) و [std::collections](https://doc.rust-lang.org/std/collections/index.html)
- Kotlin — [Kotlin Docs: Basic types](https://kotlinlang.org/docs/basic-types.html)
- Swift — [The Swift Programming Language: The Basics](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/thebasics)
- Dart — [Dart language: Built-in types](https://dart.dev/language/built-in-types)
- Ruby — [Ruby Core API Documentation](https://docs.ruby-lang.org/en/master/)
- PHP — [PHP Manual: Types](https://www.php.net/manual/en/language.types.php)
- Scala — [Scala 3 Book: Data Types](https://docs.scala-lang.org/scala3/book/first-look-at-types.html)
- Erlang — [Erlang Reference Manual: Data Types](https://www.erlang.org/doc/system/data_types.html)
- Elixir — [Elixir: Basic types](https://hexdocs.pm/elixir/basic-types.html)
- Haskell — [Haskell 2010 Language Report](https://www.haskell.org/onlinereport/haskell2010/) و [Hackage: base](https://hackage.haskell.org/package/base)

> نکته: نسخه‌های زبان‌ها سریع تغییر می‌کنند (به‌ویژه Carbon که در مرحله آزمایشی است و Zig که پیش از نسخه ۱٫۰ است). برای هر جزئیات حساسِ پروژه، مستندات نسخه‌ی مورد استفاده خود را مرجع بگیرید.
