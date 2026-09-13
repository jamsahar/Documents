# درس یک — انواع داده (Data Types)

## فهرست مطالب
1. مقدمه
2. انواع عددی
3. Boolean
4. Character و String
5. Array / List / Vector
6. Tuple
7. Set
8. Map / Dictionary
9. Object / Class / Struct / Record
10. Enum
11. Binary Data
12. Optional / Nullable
13. Union / Variant / Result
14. Function / Lambda
15. Iterator / Generator
16. Stack / Queue / Deque
17. ساختارهای داده پیشرفته
18. Pointer / Reference
19. Date/Time و UUID
20. AI/LLM Data Types
21. مقایسه جامع زبان‌ها
22. جمع‌بندی

---

## 1. مقدمه

Data Type مشخص می‌کند یک مقدار چه معنایی دارد، چه عملیاتی روی آن مجاز است و چگونه معمولاً نمایش داده می‌شود. انواع مهم شامل Integer، Float، Decimal، Boolean، Character، String، Array، List، Vector، Tuple، Set، Map، Object، Struct، Record، Enum، Binary، Optional، Union، Result، Function، Iterator، Pointer، Date/Time و UUID هستند.

**Data Type** را از **Data Structure** جدا کنید؛ مثلاً `int` نوع داده است، اما `HashMap` و `Tree` ساختار داده‌اند.

---

## 2. انواع عددی

| نوع | کاربرد |
|---|---|
| Integer | اعداد صحیح |
| Float / Double | اعداد اعشاری |
| Decimal | محاسبات اعشاری دقیق، به‌ویژه مالی |
| Big Integer | اعداد صحیح بسیار بزرگ |
| Complex | اعداد مختلط |

| زبان | Integer | Floating Point | Decimal / Big Number |
|---|---|---|---|
| Python | `int` | `float` | `decimal.Decimal` |
| JavaScript/TypeScript | `number`, `bigint` | `number` = IEEE-754 double | `BigInt`؛ Decimal معمولاً کتابخانه |
| Java | `byte/short/int/long` | `float/double` | `BigInteger`, `BigDecimal` |
| C# | `sbyte/short/int/long` | `float/double` | `decimal`, `BigInteger` |
| C++ | signed/unsigned integers | `float/double/long double` | کتابخانه‌ها |
| Go | `int8...int64`, `uint...` | `float32/float64` | کتابخانه‌ها |
| Rust | `i8...i128`, `u8...u128` | `f32/f64` | کتابخانه‌ها |
| Zig | signed/unsigned integers متعدد | `f16/f32/f64/f80/f128` بسته به target | معمولاً کتابخانه |
| Carbon | در حال تکامل | در حال تکامل | در حال تکامل |
| Scala | `Byte/Short/Int/Long` | `Float/Double` | `BigInt`, `BigDecimal` |
| Erlang | `integer()` | `float()` | integer با دقت دلخواه |
| Elixir | `integer()` | `float()` | معمولاً کتابخانه |

---

## 3. Boolean

| زبان | Boolean |
|---|---|
| Python | `bool` |
| JavaScript/TypeScript | `boolean` |
| Java | `boolean` |
| C# | `bool` |
| C++ | `bool` |
| Go | `bool` |
| Rust | `bool` |
| Zig | `bool` |
| Carbon | در حال تکامل |
| Scala | `Boolean` |
| Erlang | atoms: `true`, `false` |
| Elixir | atoms: `true`, `false` |

---

## 4. Character و String

| زبان | Character | String |
|---|---|---|
| Python | رشته تک‌کاراکتری | `str` |
| JavaScript/TypeScript | `char` مستقل ندارد | `string` |
| Java | `char` = UTF-16 code unit | `String` |
| C# | `char` = UTF-16 code unit | `string` |
| C++ | `char` و انواع مرتبط | `std::string` و... |
| Go | `rune` و `byte` | `string` |
| Rust | `char` = Unicode scalar value | `String`, `&str` |
| Zig | بایت/Unicode با مدل صریح | معمولاً `[]const u8` |
| Carbon | در حال تکامل | در حال تکامل |
| Scala | `Char` | `String` |
| Erlang | charlist یا code point؛ binary نیز رایج | charlist یا binary |
| Elixir | integer/code point | UTF-8 binary؛ charlist نیز وجود دارد |

### Unicode

بین Byte، Code Unit، Code Point و Grapheme Cluster تفاوت وجود دارد؛ چیزی که کاربر یک «کاراکتر» می‌بیند ممکن است از چند code point تشکیل شده باشد.

---

## 5. Array / List / Vector

| زبان | Array | List / Dynamic Sequence | Vector |
|---|---|---|---|
| Python | `list` و `array` کتابخانه‌ای | `list` | کتابخانه |
| JS/TS | `Array` | `Array` | کتابخانه |
| Java | `T[]` | `ArrayList`, `LinkedList` | collection/library |
| C# | `T[]` | `List<T>` | collectionهای دیگر |
| C++ | array/`std::array` | `std::vector`, `std::list` | `std::vector` |
| Go | `[N]T` | `[]T` slice | معمولاً slice |
| Rust | `[T; N]` | `Vec<T>` | `Vec<T>` |
| Zig | `[N]T`, slices | dynamic arrays مانند `ArrayList` در std | کتابخانه |
| Carbon | در حال تکامل | در حال تکامل | در حال تکامل |
| Scala | `Array[T]` | `List`, `Seq` | `Vector` |
| Erlang | list/tuple/binary | list | ساختار مستقل رایج نیست |
| Elixir | list/tuple/binary | list | ساختار مستقل رایج نیست |

---

## 6. Tuple

Tuple مجموعه‌ای مرتب از چند مقدار است و می‌تواند انواع متفاوت داشته باشد.

| زبان | Tuple |
|---|---|
| Python | بومی |
| JavaScript/TypeScript | TypeScript tuple type |
| Java | record/class یا کتابخانه |
| C# | `ValueTuple` |
| C++ | `std::tuple` |
| Go | tuple عمومی بومی ندارد |
| Rust | بومی |
| Zig | tuple |
| Carbon | در حال تکامل |
| Scala | بومی |
| Erlang | بومی |
| Elixir | بومی |

---

## 7. Set

| زبان | Set |
|---|---|
| Python | `set` |
| JavaScript/TypeScript | `Set` |
| Java | `Set`, `HashSet`, `TreeSet` |
| C# | `HashSet<T>` |
| C++ | `std::set`, `std::unordered_set` |
| Go | معمولاً `map[T]struct{}` یا کتابخانه |
| Rust | `HashSet`, `BTreeSet` |
| Zig | collections/hash-set patterns در std |
| Carbon | در حال تکامل |
| Scala | `Set`, `HashSet`, `TreeSet` |
| Erlang | `sets` |
| Elixir | `MapSet` |

---

## 8. Map / Dictionary

| زبان | Map / Dictionary |
|---|---|
| Python | `dict` |
| JavaScript/TypeScript | `Map`, object |
| Java | `Map`, `HashMap`, `TreeMap` |
| C# | `Dictionary<TKey,TValue>` |
| C++ | `std::map`, `std::unordered_map` |
| Go | `map[K]V` |
| Rust | `HashMap`, `BTreeMap` |
| Zig | hash maps در library |
| Carbon | در حال تکامل |
| Scala | `Map`, `HashMap`, `TreeMap` |
| Erlang | `map()` |
| Elixir | `Map` |

---

## 9. Object / Class / Struct / Record

| زبان | Object/Class | Struct/Record |
|---|---|---|
| Python | `class` | class/dataclass |
| JS/TS | `class`, object | `interface`, `type`, class |
| Java | `class` | `record` |
| C# | `class` | `struct`, `record` |
| C++ | `class`, `struct` | `struct` |
| Go | class سنتی ندارد | `struct` |
| Rust | struct/enum + impl | `struct` |
| Zig | `struct` | `struct` |
| Carbon | در حال تکامل | در حال تکامل |
| Scala | `class`, `object`, `case class` | `case class` |
| Erlang | object/class سنتی ندارد | `record`, tuple, map |
| Elixir | object/class سنتی ندارد | `struct`, map, tuple |

---

## 10. Enum

| زبان | Enum |
|---|---|
| Python | `enum.Enum` |
| JavaScript/TypeScript | `enum` در TypeScript |
| Java | `enum` |
| C# | `enum` |
| C++ | `enum`, `enum class` |
| Go | constants + type |
| Rust | `enum` بسیار قدرتمند و داده‌دار |
| Zig | `enum` |
| Carbon | در حال تکامل |
| Scala | `enum` و ADT |
| Erlang | atoms/tagged tuples معمولاً جایگزین |
| Elixir | atoms/tagged tuples معمولاً جایگزین |

---

## 11. Binary Data

| زبان | Binary / Bytes |
|---|---|
| Python | `bytes`, `bytearray` |
| JavaScript/TypeScript | `Uint8Array`, `ArrayBuffer`, Node `Buffer` |
| Java | `byte[]`, `ByteBuffer` |
| C# | `byte[]`, `Span<byte>` |
| C++ | `std::byte` و byte containers |
| Go | `[]byte` |
| Rust | `Vec<u8>`, `&[u8]` |
| Zig | `[]u8`, `[]const u8` |
| Carbon | در حال تکامل |
| Scala | `Array[Byte]` |
| Erlang | `binary()`, `bitstring()` |
| Elixir | binaries / bitstrings |

---

## 12. Optional / Nullable

| زبان | Optional / Nullable |
|---|---|
| Python | `None` + type hints |
| JS/TS | `null`, `undefined`, union |
| Java | `Optional<T>` |
| C# | nullable reference/value types |
| C++ | `std::optional<T>` |
| Go | pointer یا `(value, ok)` |
| Rust | `Option<T>` |
| Zig | `?T` |
| Carbon | در حال تکامل |
| Scala | `Option[T]` |
| Erlang | tagged values مانند `none` |
| Elixir | `nil` و tagged values |

---

## 13. Union / Variant / Result

| زبان | Union / Variant | Result / Error |
|---|---|---|
| Python | `Union` / `|` در typing | exceptions/typed patterns |
| JS/TS | union types | exceptions/union |
| Java | sealed types + records | exceptions/libraries |
| C# | type/record patterns | exceptions/libraries |
| C++ | `std::variant` | `std::expected` |
| Go | interfaces/structs | `(value, error)` |
| Rust | `enum` | `Result<T,E>` |
| Zig | tagged unions | error union `!T` |
| Carbon | در حال تکامل | در حال تکامل |
| Scala | ADT | `Either`, `Try` |
| Erlang | tagged tuples | `{ok,V}`, `{error,R}` |
| Elixir | tagged tuples | `{:ok,V}`, `{:error,R}` |

---

## 14. Function / Lambda

| زبان | Function / Lambda |
|---|---|
| Python | function, `lambda` |
| JS/TS | function, arrow function |
| Java | lambda |
| C# | lambda, delegate |
| C++ | lambda |
| Go | function values, closures |
| Rust | closures, function pointers |
| Zig | functions, function pointers |
| Carbon | در حال تکامل |
| Scala | first-class functions |
| Erlang | `fun` |
| Elixir | `fn` |

---

## 15. Iterator / Generator

| زبان | Iterator | Generator/Lazy |
|---|---|---|
| Python | iterator protocol | `yield` |
| JS/TS | iterator protocol | `function*` |
| Java | `Iterator`, Stream | Stream/lazy patterns |
| C# | `IEnumerable` | `yield` |
| C++ | iterators/ranges | coroutines |
| Go | iteration patterns | channels/functions |
| Rust | `Iterator` | iterator adapters |
| Zig | iterator patterns | الگوهای دستی/کتابخانه‌ای |
| Carbon | در حال تکامل | در حال تکامل |
| Scala | `Iterator` | lazy collections |
| Erlang | recursion/list processing | stream patterns |
| Elixir | `Enum`, `Stream` | `Stream` |

---

## 16. Stack / Queue / Deque

| ساختار | رفتار |
|---|---|
| Stack | LIFO |
| Queue | FIFO |
| Deque | ورود/خروج از هر دو طرف |

| زبان | امکانات رایج |
|---|---|
| Python | `list`, `collections.deque` |
| JS/TS | `Array` یا کتابخانه |
| Java | `Queue`, `Deque`, `ArrayDeque` |
| C# | `Queue<T>`, `Stack<T>` |
| C++ | `queue`, `stack`, `deque` |
| Go | slice یا library |
| Rust | `Vec`, `VecDeque` |
| Zig | collections/structures در std |
| Carbon | در حال تکامل |
| Scala | collections |
| Erlang | list/queue |
| Elixir | list/queue |

---

## 17. ساختارهای داده پیشرفته

| ساختار | کاربرد |
|---|---|
| Linked List | node-based sequence |
| Tree | داده سلسله‌مراتبی |
| AVL / Red-Black Tree | balanced search |
| B-Tree / B+Tree | database/filesystem indexes |
| Heap | priority queue |
| Graph | شبکه روابط |
| Trie | prefix search |
| Hash Table | lookup بر اساس hash |
| Skip List | ordered probabilistic structure |
| Union-Find | connectivity |
| Segment Tree | range queries |
| Fenwick Tree | prefix/range aggregation |
| Persistent Data Structure | versioned immutable data |

---

## 18. Pointer / Reference

| زبان | Pointer / Reference |
|---|---|
| Python | reference semantics؛ pointer خام ندارد |
| JS/TS | reference semantics |
| Java | reference؛ pointer خام ندارد |
| C# | reference؛ `unsafe` برای pointer |
| C++ | pointer و reference واقعی |
| Go | pointer |
| Rust | references و raw pointers |
| Zig | pointerهای صریح |
| Carbon | در حال تکامل |
| Scala | reference semantics روی JVM |
| Erlang | مدیریت‌شده توسط BEAM |
| Elixir | مدیریت‌شده توسط BEAM |

---

## 19. Date/Time و UUID

مفاهیم مهم:

- Date
- Time
- DateTime
- Instant
- Duration
- UTC
- Time Zone
- Offset
- Timestamp
- UUID

| زبان | Date/Time |
|---|---|
| Python | `datetime`, `date`, `time` |
| JS/TS | `Date` و APIها/کتابخانه‌ها |
| Java | `java.time` |
| C# | `DateTime`, `DateTimeOffset` |
| C++ | `<chrono>` |
| Go | `time` |
| Rust | crates مانند `chrono`/`time` |
| Zig | کتابخانه/ساختارهای زمان |
| Carbon | در حال تکامل |
| Scala | `java.time` و libraries |
| Erlang | date/time APIs |
| Elixir | `Date`, `Time`, `DateTime`, `NaiveDateTime` |

UUIDهای مهم: v1، v4 و v7.

---

## 20. AI/LLM Data Types

| نوع | مفهوم |
|---|---|
| Token | واحد متن پس از tokenization |
| Token ID | شناسه عددی token |
| Tensor | آرایه چندبعدی |
| Embedding | بردار عددی معنایی |
| Logits | امتیاز خام مدل |
| Probability | احتمال خروجی |
| Attention Mask | کنترل بخش‌های قابل توجه |
| Message | پیام system/user/assistant/tool |
| Tool Call | درخواست اجرای ابزار |
| Tool Result | نتیجه ابزار |
| Document | سند |
| Chunk | قطعه سند |
| Metadata | اطلاعات توصیفی |
| Agent State | وضعیت عامل |
| Memory Item | واحد حافظه |
| Vector Record | بردار + metadata |
| Similarity Score | امتیاز شباهت |

---

# 21. مقایسه جامع زبان‌های برنامه‌نویسی

زبان‌های این درس:

**Python, JavaScript/TypeScript, Java, C#, C++, Go, Rust, Zig, Carbon, Scala, Erlang, Elixir**

> **Carbon:** پروژه‌ای در حال تکامل است؛ syntax، library و tooling آن را نباید مانند زبان‌های بالغ ثابت فرض کرد.

## 21.1 جدول اصلی

| ویژگی | Python | JS/TS | Java | C# | C++ | Go | Rust | Zig | Carbon | Scala | Erlang | Elixir |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Type System | Dynamic/Gradual | Dynamic + TS static | Static | Static | Static | Static | Static | Static | evolving | Static | Dynamic | Dynamic |
| GC | بله | بله | بله | بله | خیر | بله | خیر | خیر | evolving | بله | بله | بله |
| Ownership | ندارد | ندارد | GC | GC | RAII/manual | GC | بله | allocator صریح | evolving | GC | VM-managed | VM-managed |
| Pointer | محدود/reference | reference | reference | reference | بله | بله | raw/reference | بله | evolving | reference | معمولاً پنهان | معمولاً پنهان |
| Generics | typing | generics | generics | generics | templates | generics | generics | comptime | evolving | generics/type system | patterns/modules | protocols/macros |
| Array | list/array | Array | array | array | array/vector | array/slice | array/Vec | array/slice | evolving | Array | tuple/list/binary | tuple/list/binary |
| Map | dict | Map/object | HashMap | Dictionary | map/unordered_map | map | HashMap | hash maps | evolving | Map | map | Map |
| Set | set | Set | HashSet | HashSet | set/unordered_set | map pattern | HashSet | library | evolving | Set | sets | MapSet |
| Tuple | native | TS tuple | record/class | ValueTuple | tuple | — | native | tuple | evolving | native | native | native |
| Functional Style | متوسط | زیاد | زیاد | زیاد | زیاد | متوسط | زیاد | متوسط | evolving | بسیار زیاد | بسیار زیاد | بسیار زیاد |
| Concurrency | threads/async | event loop/async | threads/futures | Task/async | threads/coroutines | goroutines/channels | async/threads | threads/async patterns | evolving | Futures/actors | processes/message passing | processes/message passing |
| Low-level Control | محدود | محدود | متوسط | متوسط | بسیار زیاد | زیاد | بسیار زیاد | بسیار زیاد | evolving/target | متوسط | کمتر | کمتر |
| Systems Programming | متوسط | محدود | متوسط | متوسط | عالی | عالی | عالی | عالی | هدف پروژه | متوسط | محدود | محدود |
| Ecosystem | بسیار بزرگ | بسیار بزرگ | بسیار بزرگ | بسیار بزرگ | بسیار بزرگ | بزرگ | بزرگ | رو به رشد | نوپا | بزرگ | تخصصی/پایدار | رو به رشد |
| Status | بالغ | بالغ | بالغ | بالغ | بالغ | بالغ | بالغ | بالغ/رو به رشد | در حال تکامل | بالغ | بالغ | بالغ |

## 21.2 Collection Comparison

| زبان | Sequence | Tuple | Set | Map |
|---|---|---|---|---|
| Python | list | tuple | set | dict |
| JS/TS | Array | TS tuple | Set | Map/object |
| Java | List | record/class | Set | Map |
| C# | List | ValueTuple | HashSet | Dictionary |
| C++ | vector/list/deque | tuple | set | map/unordered_map |
| Go | slice/array | — | map pattern | map |
| Rust | Vec/array | tuple | HashSet/BTreeSet | HashMap/BTreeMap |
| Zig | array/slice/dynamic array | tuple | hash-set patterns | hash maps |
| Carbon | evolving | evolving | evolving | evolving |
| Scala | List/Vector/Seq | Tuple | Set | Map |
| Erlang | list | tuple | sets | map |
| Elixir | list | tuple | MapSet | Map |

## 21.3 Optional / Result / Error

| زبان | Optional | Result/Error |
|---|---|---|
| Python | `None` | exceptions / typed patterns |
| JS/TS | `null`/`undefined` | exceptions / union |
| Java | `Optional` | exceptions/libraries |
| C# | nullable | exceptions/libraries |
| C++ | `optional` | `expected` / exceptions |
| Go | pointer / `(value, ok)` | `(value, error)` |
| Rust | `Option<T>` | `Result<T,E>` |
| Zig | `?T` | `!T` error union |
| Carbon | evolving | evolving |
| Scala | `Option` | `Either`, `Try` |
| Erlang | tagged values | `{ok,V}` / `{error,R}` |
| Elixir | `nil` / tagged values | `{:ok,V}` / `{:error,R}` |

## 21.4 Memory Management

| زبان | مدل |
|---|---|
| Python | مدیریت خودکار + GC implementation details |
| JS/TS | GC |
| Java | GC |
| C# | GC |
| C++ | RAII/manual/smart pointers |
| Go | GC |
| Rust | ownership + borrowing |
| Zig | explicit allocator؛ بدون GC عمومی |
| Carbon | در حال تکامل |
| Scala | JVM GC |
| Erlang | BEAM-managed + per-process GC |
| Elixir | BEAM-managed + per-process GC |

## 21.5 Concurrency

| زبان | مدل‌های مهم |
|---|---|
| Python | threads, async, multiprocessing |
| JS/TS | event loop, async/await, workers |
| Java | threads, executors, futures, virtual threads |
| C# | Task, async/await, threads |
| C++ | threads, atomics, coroutines |
| Go | goroutines, channels |
| Rust | async runtimes, threads, channels |
| Zig | threads و الگوهای async بسته به نسخه/هدف |
| Carbon | evolving |
| Scala | Futures, actors/library ecosystem |
| Erlang | lightweight processes + message passing |
| Elixir | processes + message passing + supervision |

## 21.6 Functional Programming

| زبان | سطح تقریبی |
|---|---|
| Python | متوسط |
| JavaScript/TypeScript | زیاد |
| Java | زیاد |
| C# | زیاد |
| C++ | زیاد |
| Go | متوسط |
| Rust | زیاد |
| Zig | متوسط |
| Carbon | evolving |
| Scala | بسیار زیاد |
| Erlang | بسیار زیاد |
| Elixir | بسیار زیاد |

## 21.7 نکات کلیدی زبان‌های اضافه‌شده

### Zig
- systems-oriented
- `comptime`
- allocator صریح
- بدون GC عمومی
- pointer و sliceهای صریح
- کنترل زیاد بر memory layout و منابع

### Carbon
- پروژه‌ای در حال تکامل
- با هدف مسیر مدرن‌تر برای توسعه‌دهندگان C++
- syntax، API و tooling می‌تواند تغییر کند
- برای production باید وضعیت جاری پروژه و ecosystem بررسی شود

### Scala
- روی JVM
- ترکیب Object-Oriented و Functional Programming
- `case class`
- pattern matching
- immutable collections
- `Option`, `Either`, `Try`
- generics و ADTها

### Erlang
- functional و concurrent
- immutable data
- tuple/list/map/record
- pattern matching
- lightweight processes
- message passing
- supervision و fault tolerance
- BEAM VM

### Elixir
- functional روی BEAM
- immutable data
- tuple/list/map/struct/binary
- pattern matching
- anonymous functions
- `Enum` و `Stream`
- processes، message passing و supervision

---

# 22. جمع‌بندی

مسیر مفهومی یادگیری:

```text
Primitive Types
      ↓
Collections
      ↓
Tuple / Set / Map
      ↓
Object / Struct / Record / Enum
      ↓
Optional / Union / Result
      ↓
Function / Iterator / Generator
      ↓
Binary / Text / DateTime
      ↓
Pointer / Reference
      ↓
Memory Model
      ↓
Data Structures
      ↓
Algorithms
      ↓
AI/LLM Data Models
      ↓
RAG Data Models
      ↓
Agent State / Memory
```

برای مقایسه زبان‌ها فقط syntax را مقایسه نکنید؛ Type System، Memory Management، Ownership، Mutability، Generics، Collections، Error Handling، Concurrency، Functional Programming، Low-level Control، Ecosystem، Performance، Safety و Runtime را نیز بررسی کنید.

در نهایت، یک برنامه‌نویس حرفه‌ای باید یک داده را در چند سطح ببیند:

```text
Value
  ↓
Data Type
  ↓
Memory Representation
  ↓
Data Structure
  ↓
Algorithm
  ↓
Serialization
  ↓
Database Representation
  ↓
Distributed Representation
  ↓
AI/LLM Representation
  ↓
Agent / RAG State
```
