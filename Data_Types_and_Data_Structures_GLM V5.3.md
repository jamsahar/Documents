# راهنمای جامع انواع داده در ۲۰ زبان برنامه‌نویسی

فایل Markdown کامل و قابل دانلود را آماده کردم:

# راهنمای جامع انواع داده (Data Types) در ۲۰ زبان برنامه‌نویسی

> سند مرجع کامل: انواع اولیه، آرایه‌ها، تاپل‌ها، مجموعه‌ها (Set)، نگاشت‌ها (Map)، رکوردها و انواع ویژه (Optional، Result، ADT) در Python, JavaScript, TypeScript, Java, C#, C++, C, Go, Rust, Kotlin, Swift, Dart, Ruby, PHP, Scala, Erlang, Elixir, Zig, Carbon, Gleam و Haskell — به‌همراه جداول مقایسه‌ای.

---

## فهرست مطالب

1. مفاهیم پایه
2. ماتریس مقایسهٔ سریع
3. Python
4. JavaScript
5. TypeScript
6. Java
7. C#
8. C++
9. C
10. Go
11. Rust
12. Kotlin
13. Swift
14. Dart
15. Ruby
16. PHP
17. Scala
18. Erlang
19. Elixir
20. Zig
21. Carbon
22. Gleam
23. Haskell
24. جداول مقایسهٔ تفصیلی
25. جمع‌بندی و راهنمای انتخاب
26. واژه‌نامه

---

## ۱. مفاهیم پایه

### ۱.۱. سه لایهٔ انواع داده

| لایه | توضیح | مثال |
|---|---|---|
| اولیه (Primitive) | مستقیماً توسط کامپایلر/مفسر پشتیبانی می‌شود؛ یک مقدار ساده | `int`, `float`, `bool`, `char` |
| ترکیبی (Composite) | از انواع دیگر ساخته می‌شود | آرایه، تاپل، لیست، نگاشت، ساختار |
| جبری (ADT) | ترکیب انواع «مجموع» (Sum) و «ضرب» (Product) به‌همراه pattern matching | `enum` در Rust/Swift، `data` در Haskell |

- **Product Type** (نوع ضرب): مانند struct/tuple — همهٔ فیلدها هم‌زمان وجود دارند.
- **Sum Type** (نوع مجموع): مانند enum/tagged union — فقط یکی از حالت‌ها فعال است.

### ۱.۲. ویژگی‌های کلیدی کالکشن‌ها

| ویژگی | معنا |
|---|---|
| تغییرپذیری (Mutable/Immutable) | امکان تغییر محتوا پس از ساخت |
| ترتیب (Ordered/Unordered/Sorted) | حفظ ترتیب درج یا مرتب‌سازی خودکار |
| یکتایی (Unique) | اجازه یا عدم اجازهٔ عنصر تکراری |
| همگنی (Homogeneous) | الزام هم‌نوع بودن عناصر |
| معناشناسی مقداری/ارجاعی | کپی‌شدن مقدار در انتساب یا اشتراک ارجاع |
| اندازهٔ ثابت/پویا | Fixed یا Dynamic |

### ۱.۳. پیچیدگی عملیات کالکشن‌های رایج

| ساختار | دسترسی تصادفی | درج/حذف انتها | جستجو |
|---|---|---|---|
| آرایهٔ ثابت | O(1) | — | O(n) |
| آرایهٔ پویا | O(1) | O(1)\* | O(n) |
| لیست پیوندی | O(n) | O(1) در ابتدا/انتها | O(n) |
| جدول درهم (Hash) | — | O(1)\* | O(1)\* |
| درخت متوازن | — | O(log n) | O(log n) |

(\*) میانگین / Amortized

---

## ۲. ماتریس مقایسهٔ سریع

راهنما: ✅ داخلی و رسمی | 🟡 نیمه‌رسمی / ایدیوم / کتابخانه‌ای | ❌ ندارد

| زبان | تایپ‌دهی | Tuple | Set | Map | Optional | ADT/Enum | آرایهٔ پویا |
|---|---|---|---|---|---|---|---|
| Python | پویا + قوی | ✅ tuple | ✅ set | ✅ dict | ❌ (None) | 🟡 enum ماژول | ✅ list |
| JavaScript | پویا + ضعیف | ❌ | ✅ Set | ✅ Map/Object | ❌ (null/undefined) | ❌ | ✅ Array |
| TypeScript | ایستا (اختیاری) | ✅ تایپی | ✅ Set | ✅ Map | 🟡 union با null | ✅ enum/union | ✅ Array |
| Java | ایستا + قوی | ❌ | ✅ Set | ✅ Map | ✅ Optional | ✅ enum/sealed | ✅ ArrayList |
| C# | ایستا + قوی | ✅ ValueTuple | ✅ HashSet | ✅ Dictionary | ✅ T? | ✅ enum | ✅ List<T> |
| C++ | ایستا + قوی | ✅ std::tuple | ✅ set/unordered_set | ✅ map/unordered_map | ✅ optional | 🟡 enum class/variant | ✅ vector |
| C | ایستا + ضعیف | ❌ | ❌ | ❌ | ❌ (NULL) | 🟡 enum دستی | ❌ |
| Go | ایستا + قوی | ❌ | 🟡 map[T]struct{} | ✅ map | ❌ (nil) | 🟡 iota | ✅ slice |
| Rust | ایستا + قوی | ✅ | ✅ HashSet | ✅ HashMap | ✅ Option | ✅ enum | ✅ Vec |
| Kotlin | ایستا + قوی | 🟡 Pair/Triple | ✅ Set | ✅ Map | ✅ T? | ✅ sealed/enum | ✅ MutableList |
| Swift | ایستا + قوی | ✅ | ✅ Set | ✅ Dictionary | ✅ T? | ✅ enum | ✅ Array |
| Dart | ایستا + قوی | ✅ record | ✅ Set | ✅ Map | ✅ T? | ✅ sealed/enum | ✅ List |
| Ruby | پویا + قوی | ❌ | ✅ Set | ✅ Hash | ❌ (nil) | ❌ (کلاس) | ✅ Array |
| PHP | پویا (+انوتیشن) | ❌ | 🟡 ایدیوم array | ✅ array | 🟡 null / ?T | ✅ enum (8.1) | ✅ array |
| Scala | ایستا + قوی | ✅ | ✅ Set | ✅ Map | ✅ Option | ✅ enum/ADT | ✅ ArrayBuffer |
| Erlang | پویا + قوی | ✅ | 🟡 ماژول sets | ✅ map | 🟡 اتم undefined | ✅ (اتم/تاپل) | ✅ list پیوندی |
| Elixir | پویا + قوی | ✅ | ✅ MapSet | ✅ map | 🟡 nil | ✅ custom type | ✅ list پیوندی |
| Zig | ایستا + قوی | ✅ | 🟡 std.HashMap | 🟡 std.HashMap | ✅ ?T | ✅ union(enum) | 🟡 std.ArrayList |
| Carbon | ایستا + قوی | ✅ | ❌ | 🟡 | 🟡 در طراحی | ✅ choice | 🟡 |
| Gleam | ایستا + قوی | ✅ | ✅ Set | ✅ Dict | ✅ Option | ✅ | ✅ List پیوندی |
| Haskell | ایستا + قوی | ✅ | ✅ Data.Set | ✅ Data.Map | ✅ Maybe | ✅ data | ✅ لیست |

---

## ۳. Python

> **پروفایل:** تایپ‌دهی پویا + قوی (با type hint اختیاری) | GC | پیش‌فرض تغییرپذیر | عدد صحیح با دقت نامحدود

### ۳.۱. انواع اولیه

| نوع | توضیح | مثال |
|---|---|---|
| `int` | عدد صحیح با دقت دلخواه (بدون سرریز) | `42`, `10**100` |
| `float` | ممیز شناور ۶۴ بیتی IEEE 754 | `3.14`, `1e-9` |
| `complex` | عدد مختلط | `3+4j` |
| `bool` | `True`/`False` (زیرنوع `int`) | `True` |
| `str` | رشتهٔ یونیکد، تغییرناپذیر | `"سلام"` |
| `bytes` / `bytearray` | دنبالهٔ بایت (تغییرناپذیر / تغییرپذیر) | `b"\x00"` |
| `NoneType` | تک‌مقدار `None` | `None` |

### ۳.۲. کالکشن‌های داخلی

| نوع | تغییرپذیر | ترتیب | تکرار | ساختار زیربنایی |
|---|---|---|---|---|
| `list` | بله | ترتیب درج | مجاز | آرایهٔ پویا از اشاره‌گر به اشیا |
| `tuple` | خیر | ترتیب درج | مجاز | دنبالهٔ ثابت |
| `set` | بله | بدون ترتیب | یکتا | جدول درهم |
| `frozenset` | خیر | بدون ترتیب | یکتا | جدول درهم |
| `dict` | بله | ترتیب درج (از ۳.۷) | کلید یکتا | جدول درهم |

### ۳.۳. کتابخانهٔ استاندارد و typing

- `collections`: `deque`، `Counter`، `defaultdict`، `OrderedDict`، `ChainMap`، `namedtuple`
- `array`: آرایهٔ فشردهٔ عددی | `heapq`: صف اولویت | `enum`، `dataclasses`
- typing: `list[int]`، `tuple[int, str]`، `dict[str, int]`، `set[int]`، `Optional[T]`، `Union`، `Literal`، `TypedDict`، `Protocol`

### ۳.۴. مثال

```python
from dataclasses import dataclass
from typing import NamedTuple, Optional

n, f, s, flag = 42, 3.14, "سلام", True

lst = [1, 2, 3]                    # list — تغییرپذیر
tup = (1, "a", [2])                # tuple — تغییرناپذیر
st, fz = {1, 2, 3}, frozenset({1}) # set / frozenset
d = {"name": "Ali", "age": 30}     # dict — ترتیب درج حفظ می‌شود

class Point(NamedTuple):
    x: int
    y: int

@dataclass
class User:
    name: str
    age: int = 0

def find(id: int) -> Optional[User]: ...
```

### ۳.۵. نکات کلیدی

- کلیدهای `dict` و عناصر `set` باید hashable باشند؛ به همین دلیل `tuple` کلید می‌شود اما `list` نه.
- `list` ناهمگن است (آرایه‌ای از اشاره‌گرها)، برخلاف آرایه‌های C-مانند.
- طول ثابت داخلی وجود ندارد (جز `bytes` و ماژول `array`).

---

## ۴. JavaScript

> **پروفایل:** تایپ‌دهی پویا + ضعیف | GC | فقط یک نوع عددی: float64

### ۴.۱. انواع اولیه (همگی تغییرناپذیر)

| نوع | توضیح |
|---|---|
| `number` | فقط double ۶۴ بیتی (شامل `NaN` و `Infinity`) — بدون int جدا |
| `bigint` | عدد صحیح با دقت دلخواه (`123n`) |
| `string` | UTF-16، تغییرناپذیر |
| `boolean` | `true` / `false` |
| `undefined` | مقداردهی‌نشده |
| `null` | خالی عمدی (دام: `typeof null === "object"`) |
| `symbol` | شناسهٔ یکتا برای کلید شیء |

### ۴.۲. اشیاء و کالکشن‌ها

| نوع | توضیح |
|---|---|
| `Object` | نقش دیکشنری (کلید رشته/symbol) |
| `Array` | پویا، ناهمگن، sparse، شیءگونه |
| `Map` / `Set` | هر کلید / مجموعهٔ یکتا — با حفظ ترتیب درج |
| `WeakMap` / `WeakSet` / `WeakRef` | ارجاع ضعیف (GC) |
| `Date`, `RegExp`, `Error`, `Function` | انواع شیءای دیگر |

### ۴.۳. Typed Arrays (دادهٔ باینری)

`ArrayBuffer`، `SharedArrayBuffer`، `DataView` و `Int8Array`، `Uint8Array`، `Uint8ClampedArray`، `Int16Array`، `Uint16Array`، `Int32Array`، `Uint32Array`، `Float32Array`، `Float64Array`، `BigInt64Array`، `BigUint64Array` (و `Float16Array` از ES2024).

### ۴.۴. مثال

```javascript
const n = 42, big = 123n, s = "hello", flag = true;
const id = Symbol("id");

const arr = [1, "a", true];          // Array
const map = new Map([["k", 1]]);     // Map — ترتیب درج
const set = new Set([1, 2, 3]);      // Set
const buf = new ArrayBuffer(16);     // باینری
const i32 = new Int32Array(buf);

const [x, y] = [1, 2];               // destructuring (جایگزین tuple)
```

### ۴.۵. نکات کلیدی

- Tuple ندارد؛ آرایه + destructuring جایگزین است.
- `Object` کلید را به رشته تبدیل می‌کند؛ برای کلید دلخواه از `Map` استفاده کنید.
- `===` برای مقایسهٔ دقیق؛ `NaN !== NaN`.

---

## ۵. TypeScript

> **پروفایل:** لایهٔ تایپ ایستا روی JavaScript | تایپ‌ها فقط در زمان کامپایل (Type Erasure)

### ۵.۱. انواع ویژهٔ زبان

`any`، `unknown` (ایمن‌تر از any)، `never` (نوع تهی)، `void`، literal type (`"up"`)، union `A | B`، intersection `A & B`، generic، `keyof`، `typeof`، mapped type، template literal type، `as const`.

### ۵.۲. Tuple (فقط سطح تایپ؛ در اجرا آرایه است)

```typescript
let pair: [string, number] = ["a", 1];
let named: [x: number, y: number] = [1, 2];   // عناصر نام‌دار
let opt: [string, number?] = ["a"];           // عنصر اختیاری
let rest: readonly [number, ...number[]] = [1, 2, 3];
```

### ۵.۳. سایر امکانات

- `enum` و `const enum` (عددی/رشته‌ای)
- Utility type ها: `Partial`، `Required`، `Readonly`، `Record<K,V>`، `Pick`، `Omit`، `Exclude`، `Extract`، `NonNullable`، `ReturnType`، `Parameters`، `Awaited`
- کالکشن‌های اجرایی همان JS اما تایپ‌دار: `T[]`، `readonly T[]`، `Map<K,V>`، `Set<T>`

```typescript
type ID = number | string;
type Dir = "up" | "down";
enum Color { Red, Green }

const list: number[] = [1, 2];
const map = new Map<string, number>();
const set = new Set<number>();
type UsersByCity = Record<string, User[]>;
```

---

## ۶. Java

> **پروفایل:** ایستا + قوی | JVM + GC | ارجاعی برای اشیاء، مقداری برای primitives | بدون tuple داخلی

### ۶.۱. انواع اولیه (۸ عدد)

| نوع | عرض | مثال |
|---|---|---|
| `byte` | ۸ | `42` |
| `short` | ۱۶ | — |
| `int` | ۳۲ | `42` |
| `long` | ۶۴ | `42L` |
| `float` | ۳۲ | `3.14f` |
| `double` | ۶۴ | `3.14` |
| `char` | ۱۶ (UTF-16) | `'A'` |
| `boolean` | — | `true` |

- Wrapper ها (`Integer`, `Double`, …) + autoboxing (دام: کش `Integer` از ۱۲۸- تا ۱۲۷).
- `String` تغییرناپذیر UTF-16؛ `StringBuilder` تغییرپذیر؛ Text Block.

### ۶.۲. آرایه و Collections Framework

| اینترفیس | پیاده‌سازی‌ها | نکته |
|---|---|---|
| `List` | `ArrayList`, `LinkedList`, `Vector`, `CopyOnWriteArrayList` | آرایهٔ پویا / پیوندی / legacy همگام / همگام نویسی |
| `Set` | `HashSet`, `LinkedHashSet`, `TreeSet`, `EnumSet` | hash / ترتیب درج / مرتب (درخت قرمز-سیاه) |
| `Map` | `HashMap`, `LinkedHashMap`, `TreeMap`, `ConcurrentHashMap`, `EnumMap`, `WeakHashMap`, `Hashtable` | |
| `Queue`/`Deque` | `ArrayDeque`, `PriorityQueue` | صف دوطرفه / صف اولویت (heap) |

### ۶.۳. انواع ویژه

- `record` (۱۶+): `record Point(int x, int y) {}`
- `enum`: شیء با فیلد و متد
- `Optional<T>` (۸+): برای خروجی متدها
- tuple ندارد → از `record` یا کتابخانه (Vavr، Commons) استفاده کنید.

```java
int i = 42; Integer boxed = i;
String s = "immutable";
int[] nums = {1, 2, 3};                       // طول ثابت

List<String> list = new ArrayList<>();
Set<Integer> set = new HashSet<>();           // یا LinkedHashSet / TreeSet
Map<String, Integer> map = new HashMap<>();   // یا TreeMap
Queue<Integer> q = new ArrayDeque<>();

record Point(int x, int y) {}
Optional<String> found = Optional.of("x");
enum Status { ACTIVE, INACTIVE }
```

---

## ۷. C#

> **پروفایل:** ایستا + قوی | .NET + GC | value/reference types | ValueTuple داخلی

### ۷.۱. انواع مقداری

| گروه | انواع |
|---|---|
| صحیح | `byte`, `sbyte`, `short`, `ushort`, `int`, `uint`, `long`, `ulong`, `nint`/`nuint` |
| اعشاری | `float` (۳۲)، `double` (۶۴)، `decimal` (۱۲۸؛ مناسب مالی) |
| دیگر | `bool`, `char`, `struct`, `enum` |

- `string`: تغییرناپذیر UTF-16؛ `Span<T>`/`ReadOnlySpan<T>` برای کار بدون کپی.
- Nullable: `int?` = `Nullable<int>`؛ از C# 8 انوتیشن `string?` برای ارجاع‌ها.

### ۷.۲. Tuple و کالکشن‌ها

- Tuple: `(int, string)`، نام‌دار `(int Id, string Name)`، deconstruction — بر پایهٔ `ValueTuple` (struct).
- آرایه: یک‌بعدی، چندبعدی `[,]`، دندانه‌دار `[][]`، `stackalloc`.

| کالکشن | کاربرد |
|---|---|
| `List<T>` | آرایهٔ پویا |
| `Dictionary<K,V>` | نگاشت درهم |
| `HashSet<T>` / `SortedSet<T>` | مجموعه / مجموعهٔ مرتب |
| `SortedDictionary<K,V>` / `SortedList<K,V>` | نگاشت مرتب |
| `Queue<T>`, `Stack<T>`, `LinkedList<T>` | صف/پشته |
| `ConcurrentDictionary` و خانوادهٔ Concurrent | همگام |
| `ImmutableList/Array/Dictionary` | تغییرناپذیر |
| `FrozenDictionary/Set` (.NET 8) | فقط-خواندنی بهینه پس از ساخت |

```csharp
int i = 42; decimal money = 19.99m; int? maybe = null;

(int Id, string Name) named = (1, "Ali");
var (id, name) = named;                     // deconstruction

var list = new List<int>();
var dict = new Dictionary<string, int>();
var set = new HashSet<int>();

int[] arr = { 1, 2, 3 };
int[,] grid = new int[3, 4];
int[][] jagged = new int[3][];

record Point(int X, int Y);
Span<byte> sp = stackalloc byte[8];
```

---

## ۸. C++

> **پروفایل:** ایستا + قوی | بدون GC | پیش‌فرض مقداری | کنترل کامل حافظه | STL

### ۸.۱. انواع پایه

- `bool`, `char`, `wchar_t`, `char8_t/16/32`، `short`, `int`, `long`, `long long`, `float`, `double`, `long double` + `signed/unsigned`
- عرض ثابت (`<cstdint>`): `int8_t`…`int64_t`، `uint8_t`…
- `std::string` (تغییرپذیر، بهینه‌سازی SSO)، `std::string_view` (۱۷+)

### ۸.۲. STL

| دسته | انواع |
|---|---|
| ترتیبی | `array`, `vector`, `deque`, `list`, `forward_list` |
| انجمنی مرتب (درخت) | `set`, `map`, `multiset`, `multimap` |
| درهم‌سازی (۱۱+) | `unordered_set`, `unordered_map`, `unordered_multiset`, `unordered_multimap` |
| آداپتور | `stack`, `queue`, `priority_queue` |
| تخت (C++23) | `flat_map`, `flat_set` |

### ۸.۳. انواع ویژه

- `std::pair`, `std::tuple` + structured binding: `auto [x, y] = p;`
- `std::optional<T>` (۱۷)، `std::variant<Ts...>` (۱۷؛ sum type ایمن)، `std::any` (۱۷)، `std::expected<T,E>` (۲۳)
- `std::span<T>` (۲۰)، `std::mdspan` (۲۳)
- اشاره‌گر هوشمند: `unique_ptr`, `shared_ptr`, `weak_ptr`
- `enum class`، `union`، `bitset`, `valarray`

```cpp
#include <vector>
#include <map>
#include <unordered_map>
#include <tuple>
#include <optional>
#include <memory>

int i = 42; std::int32_t fixed32 = 42;
std::string s = "mutable";

std::vector<int> vec{1, 2, 3};
std::map<std::string, int> m;             // درخت (مرتب)
std::unordered_map<std::string, int> um;  // درهم
std::set<int> st; std::multiset<int> ms;

auto t = std::make_tuple(1, "a", 3.14);
auto [x, y, z] = t;

std::optional<int> maybe;
std::variant<int, std::string> v;

auto sp = std::make_shared<int>(42);
auto up = std::make_unique<int>(42);
```

---

## ۹. C

> **پروفایل:** ایستا + ضعیف | بدون GC | مدیریت دستی حافظه | هیچ کالکشن آماده‌ای در کتابخانهٔ استاندارد ندارد

### ۹.۱. انواع پایه

`char`, `short`, `int`, `long`, `long long`, `float`, `double`, `long double`, `_Bool`/`bool` (stdbool.h)، `void` + `signed/unsigned`
عرض ثابت (`stdint.h`): `int8_t`…، `uint8_t`…، `intptr_t`، `size_t`

### ۹.۲. انواع ترکیبی

| نوع | توضیح |
|---|---|
| آرایهٔ `[N]T` | ثابت، همگن؛ به اشاره‌گر decay می‌شود |
| رشته | `char[]`/`char*` با پایان `\0` |
| `struct` | فیلدهای نام‌دار؛ Flexible Array Member (C99) |
| `union` | همپوشانی حافظه |
| `enum` | ثابت‌های صحیح |
| اشاره‌گر | `T*`، `void*`، اشاره‌گر تابع |

- VLA (آرایهٔ طول-متغیر): C99، اختیاری در C11.
- کالکشن: کتابخانهٔ شخص ثالث (GLib: `GHashTable`, `GPtrArray`؛ uthash؛ klib) یا پیاده‌سازی دستی.
- ADT دستی: struct تگ‌دار + union.

```c
#include <stdint.h>
#include <stdbool.h>

int nums[3] = {1, 2, 3};
char name[] = "Ali";

typedef struct { int id; char name[32]; } User;

typedef struct {                 /* tagged union = ADT دستی */
    enum { CIRCLE, RECT } kind;
    union {
        double r;
        struct { double w, h; } rect;
    };
} Shape;

int *p = &nums[0];
typedef struct { size_t len; int data[]; } Vec;   /* flexible array member */
```

---

## ۱۰. Go

> **پروفایل:** ایستا + قوی | GC | value semantics برای آرایه/struct | slice و map ارجاعی | بدون tuple و set داخلی

### ۱۰.۱. انواع پایه

| گروه | انواع |
|---|---|
| صحیح | `int`, `int8`…`int64`, `uint`…, `uintptr`, `byte`(=uint8), `rune`(=int32) |
| اعشاری | `float32`, `float64`, `complex64`, `complex128` |
| دیگر | `bool`, `string` (تغییرناپذیر UTF-8), `error` |

### ۱۰.۲. انواع ترکیبی

| نوع | نحو | نکته |
|---|---|---|
| آرایه | `[3]int{1,2,3}` | طول ثابت؛ مقداری (کپی می‌شود) |
| Slice | `[]int` | هدر (ptr,len,cap) + `append` — عملاً «آرایهٔ پویا» |
| Map | `map[string]int` | درهم‌سازی؛ بدون ترتیب؛ مقدار صفر `nil` |
| Struct | `type User struct{…}` | فیلدهای نام‌دار، تودرتو |
| بدون tuple | — | بازگشت چندگانه: `func f() (int, error)` |
| بدون set | — | ایدیوم: `map[T]struct{}` یا ساخت با generics (1.18+) |

- دیگر: اشاره‌گر `*T` (بدون حساب اشاره‌گر)، `chan T`، interface، generic `[T any]`.
- Zero value برای همهٔ انواع؛ تکرار رشته با `for range` بر حسب rune.

```go
i, f, s, flag := 42, 3.14, "immutable UTF-8", true
r := 'A'                       // rune = int32

arr := [3]int{1, 2, 3}         // آرایهٔ ثابت (مقداری)
nums := []int{1, 2}            // slice
nums = append(nums, 3)

ages := map[string]int{"Ali": 30}
set := map[string]struct{}{"a": {}}   // idiom برای Set

type User struct { Name string; Age int }

func divmod(a, b int) (int, int, error) {   // جایگزین tuple
    if b == 0 { return 0, 0, errors.New("divide by zero") }
    return a / b, a % b, nil
}
```

---

## ۱۱. Rust

> **پروفایل:** ایستا + قوی | بدون GC (Ownership/Borrowing) | بدون null | ADT کامل | ایمنی حافظه

### ۱۱.۱. انواع اسکالر

`i8`…`i128`، `u8`…`u128`، `isize`/`usize`، `f32`، `f64`، `bool`، `char` (۴ بایت؛ Unicode Scalar)، `str` (نوع بدون‌اندازه؛ همیشه به‌صورت `&str` قرضی)، `String` (مالک، UTF-8).

### ۱۱.۲. ترکیبی و کالکشن‌ها

| نوع | توضیح |
|---|---|
| `(T1, T2)` | تاپل + destructuring |
| `[T; N]` | آرایهٔ ثابت |
| `&[T]` / `&mut [T]` | slice (نمای قرضی) |
| `Vec<T>` | آرایهٔ پویای مالک — انتخاب پیش‌فرض |
| `VecDeque`, `LinkedList`, `BinaryHeap` | دوطرفه / پیوندی / صف اولویت |
| `HashMap<K,V>`, `BTreeMap<K,V>` | درهم / درخت |
| `HashSet<T>`, `BTreeSet<T>` | مجموعه |
| `struct` | named-field / tuple-struct / unit |
| `enum` | ADT واقعی (sum type) + pattern matching |

### ۱۱.۳. انواع ویژه

- `Option<T>` (`Some`/`None`) — جایگزین null
- `Result<T,E>` (`Ok`/`Err`) — مدیریت خطا
- اشاره‌گرهای هوشمند: `Box<T>`، `Rc<T>`، `Arc<T>`، `Cell`/`RefCell`، `Cow`
- نوع `!` (never)، newtype idiom، alias با `type`

```rust
let i: i32 = 42;
let ch: char = 'A';                       // ۴ بایت
let s: &str = "borrowed";                 // قرضی
let owned = String::from("owned");        // مالک

let tuple: (i32, f64, char) = (42, 3.14, 'A');
let (x, y, z) = tuple;
let arr: [u8; 3] = [1, 2, 3];             // ثابت
let slice: &[u8] = &arr[..];

use std::collections::{HashMap, HashSet, BTreeMap, BinaryHeap};

let mut vec: Vec<i32> = Vec::new();
vec.push(42);

let mut map: HashMap<&str, i32> = HashMap::new();
map.insert("key", 1);

let maybe: Option<i32> = Some(42);        // بدون null
let res: Result<i32, String> = Ok(42);

enum Shape {                             // ADT
    Circle(f64),
    Rect { w: f64, h: f64 },
}

struct User { name: String, age: u8 }
```

---

## ۱۲. Kotlin

> **پروفایل:** ایستا + قوی روی JVM | null-safety در سطح تایپ | تفکیک کالکشن فقط-خواندنی/تغییرپذیر | data class

- انواع پایه (روی JVM به primitive کامپایل می‌شوند مگر nullable): `Byte`, `Short`, `Int`, `Long`, `Float`, `Double`, `Char`, `Boolean` + بدونعلامت: `UInt`, `ULong`, …
- `String` (UTF-16، تغییرناپذیر) + رشتهٔ خام `"""…"""` + قالب `$x`
- `Any` (نوع بالا)، `Unit` (void)، `Nothing` (نوع تهی)
- Nullable: `T?` با `?.`، `?:`، `!!`
- آرایه: `Array<T>` (boxing)، `IntArray`/`ByteArray`/… (بدون boxing)

| فقط-خواندنی | تغییرپذیر | سازنده |
|---|---|---|
| `List<E>` | `MutableList<E>` | `listOf` / `mutableListOf` / `buildList` |
| `Set<E>` | `MutableSet<E>` | `setOf` / … |
| `Map<K,V>` | `MutableMap<K,V>` | `mapOf` / … |

- `Pair`/`Triple` + destructuring؛ میان‌بر `to` برای Pair
- `data class`، `enum class`، `sealed` (ADT)، `object`، `value class`
- `Sequence<T>`: ارزیابی تنبل (مشابه Stream جاوا)

```kotlin
val i: Int = 42
val maybe: Int? = null            // null-safety
val list: List<Int> = listOf(1, 2)
val mlist: MutableList<Int> = mutableListOf(1)
val map: Map<String, Int> = mapOf("a" to 1)
val ints: IntArray = intArrayOf(1, 2, 3)

val pair = "key" to 42
val (k, v) = pair                 // destructuring

data class User(val name: String, val age: Int)

sealed class Result
object Loading : Result()
data class Ok(val data: Int) : Result()

val lazySeq = sequence { yield(1); yield(2) }
```

---

## ۱۳. Swift

> **پروفایل:** ایستا + قوی | ARC | value semantics + Copy-on-Write | ADT کامل | بدون null

- عددی: `Int`, `Int8/16/32/64`, `UInt…`, `Float`, `Double`, `CGFloat`؛ `Bool`؛ `Character` (extended grapheme cluster!)؛ `String` (مقداری، پشتیبانی کامل یونیکد)؛ `Substring`
- Optional: `T?` = `Optional<T>` با `if let`/`guard let`/`??`
- `Result<Success, Failure>`

| نوع | توضیح |
|---|---|
| `Array<T>` / `[T]` | مقداری + COW |
| `Set<T>` (نیازمند `Hashable`) | درهم |
| `Dictionary<K,V>` | درهم |
| `(T, U)` | تاپل (نام‌دار هم می‌شود)؛ Hashable نیست → کلید dict نمی‌شود |
| `ContiguousArray`, `ArraySlice` | بهینه |

- `struct` (مقداری) / `class` (ارجاعی) / `actor` (همگام) / `protocol`
- `enum` با associated values = ADT کامل؛ `indirect` برای بازگشتی؛ `OptionSet` برای بیت‌ماسک
- بازه‌ها: `0..<10` (`Range`)، `0...10` (`ClosedRange`)

```swift
let i: Int = 42
let ch: Character = "A"           // grapheme cluster
var s = "value type, یونیکد"

var maybe: Int? = nil
if let x = maybe { print(x) }

let list: [Int] = [1, 2, 3]       // مقداری + COW
var dict: [String: Int] = ["a": 1]
let set: Set<String> = ["a", "b"]

let pair: (Int, String) = (1, "a")
let labeled = (x: 1, y: 2)

enum Shape {                      // ADT
    case circle(radius: Double)
    case rect(w: Double, h: Double)
}

struct User { let name: String; let age: Int }
let range = 0..<10
let result = Result<Int, Error>.success(42)
```

---

## ۱۴. Dart

> **پروفایل:** ایستا + قوی | null-safety (از ۲.۱۲) | رکورد از Dart 3 | اجرا روی VM و کامپایل به JS

- `num` ← `int` (۶۴بیتی native؛ در کامپایل به JS رفتار متفاوت) و `double` (IEEE 64)؛ `bool`؛ `String` (تغییرناپذیر، واحد کد UTF-16؛ `runes` برای یونیکد کامل)؛ `dynamic`, `Object`, `Never`؛ Nullable `T?`

| نوع | نکته |
|---|---|
| `List<E>` | پیش‌فرض growable؛ `List.filled(n)` ثابت؛ `const []` کامپایل‌تایم |
| `Set<E>` | LinkedHashSet → ترتیب درج |
| `Map<K,V>` | LinkedHashMap → ترتیب درج |
| `Queue` (dart:collection) | صف دوطرفه |
| `SplayTreeMap/Set` | مرتب |

- رکورد (Dart 3): `(int, String)` و نام‌دار `({int id, String name})` + pattern matching و destructuring؛ exhaustiveness با `sealed`
- `enum` پیشرفته (فیلد/متد)، `sealed`/`final`/`base`/`interface`
- `Future<T>`, `Stream<T>`؛ typed data: `Int32List`… (dart:typed_data)

```dart
int i = 42; double f = 3.14; num any = 42;
String s = 'UTF-16, تغییرناپذیر';
int? maybe = null;

List<int> list = [1, 2, 3];
Set<String> set = {'a', 'b'};
Map<String, int> map = {'a': 1};

(int, String) pair = (42, 'a');               // رکورد (Dart 3)
({int id, String name}) named = (id: 1, name: 'Ali');
final (id, name) = pair;                      // pattern

sealed class Result {}
class Ok extends Result {}

enum Color { red, green }

Future<int> later = Future.value(42);
```

---

## ۱۵. Ruby

> **پروفایل:** پویا + قوی | همه‌چیز شیء است | GC | عدد صحیح با دقت نامحدود | هیچ نوع «اولیه»یی ندارد

| کلاس | توضیح |
|---|---|
| `Integer` | دقت نامحدود (Fixnum/Bignum یکپارچه از ۲.۴) |
| `Float` | ۶۴ بیتی |
| `Rational`, `Complex` | کسر و عدد مختلط دقیق |
| `String` | دنبالهٔ بایت تغییرپذیر با encoding؛ `freeze`؛ `frozen_string_literal` |
| `Symbol` | نام interned تغییرناپذیر (`:name`) |
| `nil`, `true`, `false` | اشیاء تک‌مقدار |
| `Array` | پویا، ناهمگن، اندیس منفی؛ نقش stack/queue نیز می‌دهد |
| `Hash` | هر کلیدی؛ حفظ ترتیب درج؛ مقدار پیش‌فرض |
| `Set` | مجموعه (از stdlib؛ در ۳.۲+ بدون `require`) |
| `Struct` / `Data` | ساختار تغییرپذیر / شیء مقداری تغییرناپذیر (۳.۲+) |
| `Range` | `1..10` (شامل) / `1...10` (غیرشامل) |
| `Enumerator::Lazy` | ارزیابی تنبل |

```ruby
n = 42                # Integer — دقت نامحدود
r = Rational(1, 3)    # کسر دقیق
c = 1 + 2i            # Complex
s = "mutable"         # String
sym = :name           # Symbol
nothing = nil

arr = [1, "a", nil]              # ناهمگن
h = { name: "Ali", 1 => :x }     # Hash — ترتیب‌دار
set = Set.new([1, 2])            # require "set"

Point = Struct.new(:x, :y)
p = Point.new(1, 2)

range = (1..10)
enum = (1..Float::INFINITY).lazy
```

---

## ۱۶. PHP

> **پروفایل:** پویا (با تایپ‌های امضایی فزاینده) | GC / Copy-on-Write | `array` = نقشهٔ مرتب همه‌کاره

- انواع: `bool`, `int` (۶۴بیتی روی پلتفرم ۶۴بیتی), `float`, `string` (رشتهٔ بایتی), `null`
- تایپ‌های ویژه: `callable`, `iterable`, `object`, `mixed`, `void`, `never` (۸.۱)، `false/true/null` مستقل (۸.۲)، union `A|B` (۸.۰)، intersection `A&B` (۸.۱)، DNF (۸.۲)، nullable `?T`
- `array`: جدول درهم مرتب — هم لیست `[1,2]`، هم دیکشنری `['k'=>v]`، هم صف/پشته (با توابع)، هم شبه-set (کلید = مقدار)؛ destructuring با `[$a,$b] = $pair`
- اشیاء: `stdClass`، کلاس‌ها، anonymous class، `WeakMap`/`WeakReference`، `DateTimeImmutable`
- SPL: `SplFixedArray`, `SplDoublyLinkedList`, `SplStack`, `SplQueue`, `SplPriorityQueue`, `SplObjectStorage`
- افزونهٔ DS: `Ds\Vector`, `Ds\Deque`, `Ds\Map`, `Ds\Set`, `Ds\Stack`, `Ds\Queue`
- `enum` (۸.۱): pure / backed؛ `readonly` (۸.۱)؛ typed properties (۷.۴)

```php
<?php
$list = [1, 2, 3];
$map = ['name' => 'Ali', 1 => 'x'];
$pair = ['a', 1];                // جایگزین tuple
[$a, $b] = $pair;                // destructuring

$obj = new stdClass();
$wm = new WeakMap();
$fixed = new SplFixedArray(100);
$dsSet = new Ds\Set([1, 2]);

enum Status: string {            // enum (8.1)
    case Active = 'active';
    case Inactive = 'inactive';
}

function find(int $id): ?User {}
function cast(mixed $v): int|string {}
```

---

## ۱۷. Scala

> **پروفایل:** ایستا + قوی روی JVM | inference قوی | کالکشن تغییرناپذیر به‌صورت پیش‌فرض | ADT با case class | Scala 3: enum/union/opaque

سلسله‌مراتب تایپ: `Any` ← `AnyVal` (انواع مقداری) / `AnyRef` (اشیاء)؛ `Nothing` (تهی)؛ `Null`؛ `Unit`

- مقداری: `Byte`, `Short`, `Int`, `Long`, `Float`, `Double`, `Char`, `Boolean`, `Unit`
- `String` = `java.lang.String`
- Tuple: `(1, "a")` — تا ۲۲ عضو (در Scala 3 دلخواه)
- `Option[T]`، `Try[T]`، `Either[A,B]`

| تغییرناپذیر (پیش‌فرض) | تغییرپذیر |
|---|---|
| `List` (پیوندی)، `Vector` (شبه‌آرایهٔ پویا)، `LazyList`, `Range`, `Queue` | `ArrayBuffer`, `ListBuffer`, `Queue`, `HashMap/Set`, `SortedMap/Set` (درخت) |

- `Array[T]` = آرایهٔ خام JVM
- `case class`/`case object` → ADT + pattern matching؛ Scala 3: `enum`
- Scala 3: union `A | B`، intersection `A & B`، `opaque type`

```scala
val i: Int = 42
val s: String = "java.lang.String"

val pair = (1, "a")
val (x, y) = pair

val list = List(1, 2, 3)          // تغییرناپذیر
val vec  = Vector(1, 2, 3)
val map  = Map("a" -> 1)
val set  = Set(1, 2)

import scala.collection.mutable
val buf = mutable.ArrayBuffer[Int]()
buf += 42

val maybe: Option[Int] = Some(42)
case class User(name: String, age: Int)

enum Color:                       // Scala 3
  case Red, Green

type ID = Int | String            // union
opaque type Meters = Double
```

---

## ۱۸. Erlang

> **پروفایل:** پویا + قوی | همه‌چیز تغییرناپذیر + تک-انتسابی (Single Assignment) | GC به ازای هر process | همزمانی محور

| نوع | توضیح |
|---|---|
| عدد | `integer` دقت نامحدود؛ `float` ۶۴بیتی |
| atom | ثابت نامی؛ `true`/`false` خود atom هستند |
| binary / bitstring | `<<"متن"/utf8>>`؛ bit syntax در سطح بیت |
| string | به‌طور سنتی لیست اعداد؛ امروز binary ترجیح دارد |
| tuple | `{ok, 42}` — هستهٔ الگوی «تاپل تگ‌دار» |
| map | `#{k => v}` (از OTP 17) |
| list | پیوندی `[H|T]`، ناهمگن |
| record | شکر نحسی روی tuple در زمان کامپایل |
| fun | تابع بی‌نام |
| pid / reference / port | شناسه‌های همزمانی |
| ets / dets | جداول KV همگام در حافظه/دیسک |

```erlang
N = 42,                          %% integer — دقت نامحدود
F = 3.14,
Ok = ok,                         %% atom

Bin = <<"سلام"/utf8>>,           %% binary
Pair = {ok, 42},                 %% tuple تگ‌دار
L = [1, 2 | [3]],                %% list پیوندی
M = #{name => <<"Ali">>, age => 30},

-record(user, {name, age = 0}).  %% record (تاپل کامپایل‌تایم)
User = #user{name = <<"Ali">>, age = 30},

Double = fun(X) -> X * 2 end,    %% fun
Double(21).

{ok, Value} = {ok, 42}.          %% pattern matching همه‌جا
```

---

## ۱۹. Elixir

> **پروفایل:** پویا + قوی روی BEAM | تغییرناپذیری کامل (متغیرها rebound می‌شوند) | ماکرو و pipe operator | زیربنای Erlang

| نوع | نحو | توضیح |
|---|---|---|
| integer | `42`, `0x1F` | دقت نامحدود |
| float | `3.14` | ۶۴بیتی |
| atom | `:ok`, `true`, `nil` | — |
| string | `"سلام"` | binary یونیکد UTF-8 |
| charlist | `'abc'` | لیست اعداد |
| list | `[1, 2, 3]` | پیوندی، ناهمگن |
| tuple | `{:ok, 42}` | اندازهٔ ثابت، تگ‌دار |
| keyword list | `[a: 1]` | لیستی از `{atom, value}` |
| map | `%{k => v}` | درهم؛ pattern matching |
| struct | `%User{}` | map با ماژول و فیلدهای ثابت (`defstruct`) |
| MapSet | `MapSet.new([1,2])` | مجموعهٔ درهم |
| Range | `1..10` | شمارش‌پذیر |
| BitArray | `<<1,2>>` | سطح بیت |

```elixir
n = 42
ok = :ok
nothing = nil
s = "UTF-8 binary"

list = [1, 2, 3]                 # پیوندی
kw = [name: "Ali", age: 30]      # keyword list
pair = {:ok, 42}
{a, b} = {1, 2}                  # pattern matching

m = %{"str" => 1, atom: 2}       # map

defmodule User do
  defstruct name: "Ali", age: 0  # struct
end
u = %User{age: 30}

set = MapSet.new([1, 2])
range = 1..10
bin = <<1, 2, 3>>

def handle({:ok, data}), do: data
def handle({:error, reason}), do: {:error, reason}
```

---

## ۲۰. Zig

> **پروفایل:** ایستا + قوی | بدون GC و بدون runtime پنهان | allocator صریح | comptime | عدد صحیح با عرض دلخواه

| نوع | توضیح |
|---|---|
| عدد صحیح | `i8…i128`، `u8…u128`، `usize`/`isize` و **عرض دلخواه** مثل `i7`، `u42`؛ `comptime_int` |
| عدد اعشاری | `f16`, `f32`, `f64`, `f128`، `comptime_float` |
| ویژه | `bool`, `void`, `noreturn`, `type`, `anytype`, `undefined` |
| آرایه | `[N]T` — طول کامپایل‌تایمی |
| slice | `[]T` / `[]const T` / sentinel مانند `[:0]u8` |
| اشاره‌گر | `*T` (تک) و `[*]T` (چند)؛ اختیاری `?*T` |
| struct | نام‌دار، بی‌نام، tuple (فیلدهای شماره‌ای)، `packed` |
| enum / union | `enum` و `union(enum)` = ADT |
| optional | `?T` |
| error union | `T!E` + `try` / `catch` |
| vector | `@Vector(4, f32)` — SIMD |
| رشته | قرارداد `[]const u8`؛ لیترال `*const [N:0]u8` |

- std: `ArrayList`، `AutoHashMap`/`StringHashMap`/`HashMap`، `MultiArrayList` (چیدمان SoA) — توجه: API کالکشن‌های std در نسخه‌های جدید Zig در حال تغییر به سبک unmanaged است.
- `defer`/`errdefer`؛ generics با comptime.

```zig
const std = @import("std");

const a: i32 = 42;
const tiny: i7 = 60;            // عدد صحیح ۷ بیتی!
const f: f32 = 3.14;
const maybe: ?i32 = null;       // optional

const arr: [3]u8 = .{ 1, 2, 3 };
const slice: []const u8 = &arr;
const s = "hello";              // []const u8

const pair = .{ 42, "a" };      // tuple (struct بی‌نام)

const User = struct { name: []const u8, age: u8 };
const ali = User{ .name = "Ali", .age = 30 };

const Tag = enum { circle, rect };
const Shape = union(Tag) {      // ADT
    circle: f64,
    rect: struct { w: f64, h: f64 },
};

const val: error{NotFound}!u32 = 42;   // error union
const unwrapped = val catch 0;

var list = std.ArrayList(u32).init(std.heap.page_allocator);
defer list.deinit();
try list.append(42);

var map = std.AutoHashMap(u32, []const u8)
    .init(std.heap.page_allocator);
defer map.deinit();
```

---

## ۲۱. Carbon (آزمایشی)

> **پروفایل:** ایستا + قوی | هدف: جانشین بالقوهٔ C++ | ⚠️ **نسخهٔ پایدار وجود ندارد؛ سینتکس و دیزاین پیوسته در حال تغییر است**

بر اساس مستندات طراحی و دموهای عمومی فعلی:

| مفهوم | نحو فعلی |
|---|---|
| عدد صحیح/اعشاری | `i8`/`i16`/`i32`/`i64`/`i128`، انواع `u…`، `f16`/`f32`/`f64`/`f128` |
| تغییرپذیری | `var` (قابل تغییر) / `let` (تغییرناپذیر) |
| تاپل | `var (a, b): (i32, i32) = (0, 1);` |
| اشاره‌گر | `T*`، `&x` (بدون حساب اشاره‌گر در سطح ایمن) |
| آرایه | `array(T, N)` |
| struct | `struct Point { var x: i32; … }` + literal `{.x = 1}` |
| کلاس | `class` + وراثت و متد virtual |
| sum type | `choice` (در حال بازطراحی به `variant`) |
| استنتاج تایپ | `auto` |
| کتابخانهٔ Core | `Optional`، `Result`، `String` — در حال طراحی |

```carbon
// ⚠️ سینتکس در حال تحول — صرفاً جهت آشنایی

var x: i32 = 42;
let constant: i32 = 10;

var (a, b): (i32, i32) = (0, 1);   // تاپل + destructuring

var p: i32* = &x;                   // اشاره‌گر
var arr: array(i32, 3) = (1, 2, 3); // آرایه

struct Point {
  var x: i32;
  var y: i32;
}
var pt: Point = {.x = 1, .y = 2};

choice OptionalInt {                // sum type
  None;
  Some(i32);
}

var inferred: auto = 42;
```

⚠️ این بخش بر پایهٔ مستندات طراحی در دسترس نگارنده است و به‌قطع با نسخه‌های بعدی Carbon تغییر خواهد کرد.

---

## ۲۲. Gleam

> **پروفایل:** ایستا + قوی با inference | **بدون null و بدون استثنا** | تغییرناپذیری کامل | کامپایل به Erlang و JavaScript

| نوع | توضیح |
|---|---|
| `Int` | ۶۴بیتی علامت‌دار |
| `Float` | ۶۴بیتی |
| `Bool` | `True` / `False` |
| `String` | binary یونیکد UTF-8، تغییرناپذیر |
| `BitArray` | دنبالهٔ بیت |
| `List(a)` | پیوندی تغییرناپذیر؛ دسترسی تصادفی ندارد |
| `#(a, b)` | تاپل با هر تعداد عضو |
| `Dict(k, v)` | نگاشت درهم تغییرناپذیر (gleam/dict) |
| `Set(a)` | مجموعه (gleam/set) |
| `Result(a, e)` | `Ok`/`Error` — مدیریت خطای استاندارد (داخلی) |
| `Option(a)` | `Some`/`None` (gleam/option) |
| custom type | ADT کامل + pattern matching جامع |

```gleam
import gleam/dict
import gleam/set
import gleam/option.{type Option, Some, None}

let n: Int = 42
let s: String = "UTF-8, تغییرناپذیر"
let bits: BitArray = <<1, 2, 3>>

let list: List(Int) = [1, 2, 3]          // پیوندی

let pair: #(Int, String) = #(42, "a")
let #(a, b) = pair                        // pattern

let d = dict.from_list([#("a", 1)])
let s2 = set.from_list([1, 2])

let r: Result(Int, String) = Ok(42)       // بدون استثنا
let maybe: Option(Int) = Some(1)          // بدون null

type Shape {
  Circle(Float)
  Rect(Float, Float)
}

type User {
  User(name: String, age: Int)            // رکورد با فیلد نام‌دار
}

case shape {
  Circle(r) -> r *. 3.14 *. 2.0
  Rect(w, h) -> w *. h
}
```

---

## ۲۳. Haskell

> **پروفایل:** ایستا + قوی + خالص + تنبل | استنتاج تایپ کامل | بدون null | ADT و type class

| نوع | توضیح |
|---|---|
| `Int` | صحیح محدود (معمولاً ۶۴بیتی) |
| `Integer` | دقت نامحدود |
| `Float` / `Double` | — |
| `Word`, `Word8…64` | بدون علامت |
| `Rational` | کسر دقیق |
| `Bool`, `Char` | — |
| `String` = `[Char]` | لیست کاراکتر (کند)؛ عملی: `Data.Text`, `Data.ByteString` |
| `[a]` | لیست پیوندی همگن **تنبل**؛ لیست بی‌نهایت مجاز |
| `(a, b)` | تاپل ناهمگن (تا ۶۲ عضو در GHC)؛ `()` = واحد |
| `Maybe a` | `Just` / `Nothing` |
| `Either e a` | `Left` / `Right` |
| `data` / `newtype` / `type` | ADT / بدون سربار اجرا / مترادف |
| record syntax | `{ field :: T }` با تابع گیرنده |
| `Void` | نوع بی‌سکنه (تهی) |

کتابخانه‌ها: `Data.Map`/`Data.Set` (درخت)، `Data.HashMap`/`Data.HashSet` (unordered-containers)، `Data.IntMap`/`IntSet`، `Data.Sequence` (finger tree)، `Data.Vector` (آرایه)، `Data.Array`.

```haskell
n :: Int; n = 42
big :: Integer; big = 2^200         -- دقت نامحدود

nums = [1..10]
infinite = [1..]                     -- لیست بی‌نهایت (تنبل)
comprehension = [x*x | x <- [1..10], even x]

pair :: (Int, String); pair = (42, "a")
unit = ()

maybeVal :: Maybe Int; maybeVal = Just 42
eitherVal :: Either String Int; eitherVal = Right 42

data User = User { name :: String, age :: Int }
data Shape = Circle Double | Rect Double Double
  deriving (Show, Eq)

area :: Shape -> Double
area (Circle r) = pi * r * r
area (Rect w h) = w * h

newtype Meters = Meters Double       -- بدون سربار

import qualified Data.Map as M
import qualified Data.Set as S
m = M.fromList [("a", 1)]
s = S.fromList [1, 2]
```

---

## ۲۴. جداول مقایسهٔ تفصیلی

### ۲۴.۱. آرایهٔ پویا / لیست

| زبان | نام | تغییرپذیر | ناهمگن | زیربنای رایج |
|---|---|---|---|---|
| Python | `list` | بله | بله | آرایهٔ پویا از اشاره‌گر |
| JavaScript | `Array` | بله | بله | شیءگونه (بهینه‌شده) |
| TypeScript | `Array<T>` | بله | خیر (تایپ) | همان JS |
| Java | `ArrayList<T>` | بله | خیر | آرایهٔ پویا |
| C# | `List<T>` | بله | خیر | آرایهٔ پویا |
| C++ | `std::vector<T>` | بله | خیر | حافظهٔ پیوسته |
| C | — | — | — | دستی |
| Go | `slice` | بله | خیر | ptr+len+cap |
| Rust | `Vec<T>` | بله | خیر | پیوسته، مالک |
| Kotlin | `MutableList<T>` | بله | خیر | ArrayList جاوا |
| Swift | `Array` | COW | خیر | مقداری، پیوسته |
| Dart | `List` | بله | خیر | growable |
| Ruby | `Array` | بله | بله | آرایهٔ پویا |
| PHP | `array` (لیستی) / `Ds\Vector` | بله | بله | hashtable |
| Scala | `ArrayBuffer` / `Vector` | بله / خیر | خیر | آرایهٔ پویا / trie |
| Erlang / Elixir | `list` | خیر | بله | پیوندی |
| Zig | `std.ArrayList` | بله | خیر | پیوسته |
| Carbon | `array(T,N)` | — | خیر | ثابت |
| Gleam | `List(a)` | خیر | بله | پیوندی |
| Haskell | `[a]` | خیر | خیر | پیوندی، تنبل |

### ۲۴.۲. Tuple

| زبان | وضعیت | نحو | نکته |
|---|---|---|---|
| Python | ✅ | `(1, "a")` | تغییرناپذیر، hashable |
| JavaScript | ❌ | — | آرایه + destructuring |
| TypeScript | ✅ (تایپی) | `[number, string]` | در اجرا آرایه |
| Java | ❌ | — | `record` یا کتابخانه |
| C# | ✅ | `(1, "a")` | ValueTuple (struct) |
| C++ | ✅ | `std::tuple`, `std::pair` | + structured binding |
| C | ❌ | — | struct |
| Go | ❌ | — | بازگشت چندگانه |
| Rust | ✅ | `(1, "a")` | + destructuring |
| Kotlin | 🟡 | `Pair`, `Triple` | data class |
| Swift | ✅ | `(1, "a")` | نام‌دار هم می‌شود |
| Dart | ✅ | `(1, "a")` | رکورد (از ۳.۰) |
| Ruby / PHP | ❌ | — | آرایه |
| Scala | ✅ | `(1, "a")` | تا ۲۲ (دلخواه در Scala 3) |
| Erlang / Elixir | ✅ | `{1, 2}` / `{:ok, 42}` | الگوی تگ‌دار |
| Zig | ✅ | `.{ 1, "a" }` | tuple struct بی‌نام |
| Carbon | ✅ | `(1, 2)` | — |
| Gleam | ✅ | `#(1, "a")` | — |
| Haskell | ✅ | `(1, "a")` | تا ۶۲ عضو |

### ۲۴.۳. Set

| زبان | داخلی | مرتب/ترتیب‌دار |
|---|---|---|
| Python | `set` / `frozenset` | بدون ترتیب |
| JavaScript / TS | `Set` | ترتیب درج |
| Java | `HashSet` / `LinkedHashSet` / `TreeSet` | hash / درج / مرتب |
| C# | `HashSet<T>` / `SortedSet<T>` | hash / مرتب |
| C++ | `set` / `unordered_set` (+ multi) | درخت / hash |
| C | ❌ | دستی |
| Go | ❌ → `map[T]struct{}` | — |
| Rust | `HashSet` / `BTreeSet` | hash / درخت |
| Kotlin | `Set` / `MutableSet` | hash (LinkedHashSet) |
| Swift | `Set` | بدون ترتیب |
| Dart | `Set` | ترتیب درج (Linked) |
| Ruby | `Set` | hash |
| PHP | 🟡 ایدیوم array / `Ds\Set` / `SplObjectStorage` | ترتیب درج |
| Scala | `Set` (+ `SortedSet`) | hash / مرتب |
| Erlang | 🟡 ماژول `sets`/`ordsets`/`gb_sets` | — |
| Elixir | `MapSet` | hash |
| Zig | 🟡 `std.HashMap` به‌عنوان set | — |
| Carbon | ❌ (هنوز) | — |
| Gleam | `Set` | hash |
| Haskell | `Data.Set` / `Data.HashSet` | درخت / hash |

### ۲۴.۴. Map / Dictionary

| زبان | اصلی | مرتب | نکته |
|---|---|---|---|
| Python | `dict` | ترتیب درج (۳.۷+) | کلید باید hashable باشد |
| JavaScript | `Object` / `Map` | Map: درج | کلید Map هر نوعی |
| TypeScript | `Map<K,V>` / `Record` | درج | — |
| Java | `HashMap` | `LinkedHashMap`/`TreeMap` | — |
| C# | `Dictionary<K,V>` | `SortedDictionary` | — |
| C++ | `unordered_map` | `map` | — |
| C | ❌ | — | GLib و… |
| Go | `map[K]V` | ❌ | بدون ترتیب |
| Rust | `HashMap` | `BTreeMap` | — |
| Kotlin | `Map`/`MutableMap` | `LinkedHashMap` | — |
| Swift | `Dictionary` | ❌ | کلید: `Hashable` |
| Dart | `Map` | ترتیب درج | — |
| Ruby | `Hash` | ترتیب درج | هر کلیدی |
| PHP | `array` | ترتیب درج | همه‌کاره |
| Scala | `Map` | `SortedMap` | تغییرناپذیر پیش‌فرض |
| Erlang / Elixir | `map` / `%{}` | ❌ | pattern matching |
| Zig | `std.AutoHashMap` و… | ❌ | allocator صریح |
| Carbon | 🟡 در طراحی | — | — |
| Gleam | `Dict` | ❌ | تغییرناپذیر |
| Haskell | `Data.Map` | خودش مرتب | درخت متوازن |

### ۲۴.۵. Optional / Nullable

| زبان | رویکرد |
|---|---|
| Python | `None` + `Optional[T]` (تایپی) |
| JavaScript | `null` / `undefined` + `?.` و `??` |
| TypeScript | `T \| null \| undefined` |
| Java | `null` + `Optional<T>` |
| C# | `null` + `Nullable<T>`/`T?` + انوتیشن ارجاع |
| C++ | اشاره‌گر null + `std::optional` |
| C | `NULL` |
| Go | `nil` (برای pointer/map/slice/interface)؛ بدون Optional رسمی |
| Rust | `Option<T>` — **null وجود ندارد** |
| Kotlin | `T?` — null-safety در سطح تایپ |
| Swift | `Optional<T>` — **null وجود ندارد** |
| Dart | `T?` |
| Ruby | `nil` |
| PHP | `null` + `?T` |
| Scala | `null` (interop) + `Option[T]` |
| Erlang | اتم `undefined` (قراردادی) |
| Elixir | `nil` |
| Zig | `?T` (optional) |
| Carbon | 🟡 در طراحی |
| Gleam | **null ندارد** → `Option` کتابخانه‌ای |
| Haskell | **null ندارد** → `Maybe` |

### ۲۴.۶. رشته

| زبان | نوع | کدگذاری | تغییرپذیری | نکته |
|---|---|---|---|---|
| Python | `str` | یونیکد | خیر | — |
| JavaScript | `string` | UTF-16 | خیر | — |
| Java | `String` | UTF-16 | خیر | `StringBuilder` |
| C# | `string` | UTF-16 | خیر | — |
| C++ | `std::string` | بایت | بله | — |
| C | `char*` | بایت | بله | پایان `\0` |
| Go | `string` | UTF-8 | خیر | `[]byte` / `[]rune` |
| Rust | `String`/`&str` | UTF-8 | String بله | مالک/قرضی |
| Kotlin | `String` | UTF-16 | خیر | — |
| Swift | `String` | یونیکد (grapheme) | مقداری | `Character` = گرافم |
| Dart | `String` | UTF-16 | خیر | `runes` |
| Ruby | `String` | بایت + encoding | بله | `freeze` |
| PHP | `string` | بایت | COW | — |
| Scala | `String` | UTF-16 | خیر | Java |
| Erlang / Elixir | binary | UTF-8 | خیر | — |
| Zig | `[]const u8` | بایت (قرارداد UTF-8) | بله | — |
| Carbon | 🟡 در طراحی | — | — | — |
| Gleam | `String` | UTF-8 | خیر | — |
| Haskell | `String`/`Text` | یونیکد | خیر | `[Char]` کند |

### ۲۴.۷. Enum / ADT (Sum Type)

| زبان | سطح پشتیبانی |
|---|---|
| Rust, Swift, Haskell, Gleam | ✅ کامل (associated values + pattern matching) |
| Scala | ✅ `case class`/`enum` (Scala 3) |
| TypeScript | ✅ union type + discriminant |
| Kotlin | ✅ `sealed class` + `enum` |
| Dart | ✅ `sealed` + enum پیشرفته |
| C++ | 🟡 `std::variant` + `enum class` |
| Java | 🟡 `enum` (غنی) + `sealed` (۱۷+) |
| C# | 🟡 `enum` ساده + کتابخانه/`OneOf` |
| Go | 🟡 `iota` + interface (ضعیف) |
| Erlang/Elixir | ✅ با atom/tuple/custom type |
| Zig | ✅ `union(enum)` |
| Python | 🟡 `enum` ماژول |
| C | 🟡 struct تگ‌دار دستی |
| Ruby, PHP, JavaScript | 🟡/❌ (enum کتابخانه‌ای / PHP 8.1 رسمی) |

### ۲۴.۸. Struct / Record

| زبان | نام |
|---|---|
| Python | `dataclass`, `NamedTuple` |
| TS | interface / `type` / `Record` |
| Java | `record` |
| C# | `record` / `struct` |
| C++ / C / Zig | `struct` |
| Go | `struct` |
| Rust | `struct` |
| Kotlin | `data class` |
| Swift | `struct` |
| Dart | class + رکورد |
| Ruby | `Struct` / `Data` |
| Scala | `case class` |
| Elixir | `defstruct` |
| Gleam | custom type با فیلد نام‌دار |
| Haskell | record syntax |
| Erlang | `record` (کامپایل‌تایم) |

### ۲۴.۹. صف / پشته / صف اولویت (گزیده)

| زبان | صف | پشته | صف اولویت |
|---|---|---|---|
| Python | `deque` | `list` | `heapq` |
| Java | `ArrayDeque` | `ArrayDeque` | `PriorityQueue` |
| C# | `Queue<T>` | `Stack<T>` | — (لیست مرتب/کتابخانه) |
| C++ | `queue` | `stack` | `priority_queue` |
| Rust | `VecDeque` | `Vec` | `BinaryHeap` |
| Go | — (slice) | — (slice) | container/heap |
| Scala | `Queue` | `Stack` | `PriorityQueue` |
| PHP | `SplQueue` | `SplStack` | `SplPriorityQueue` |
| Dart | `Queue` | `List` | — |

---

## ۲۵. جمع‌بندی و راهنمای انتخاب

سه خانوادهٔ فلسفی:

1. **پویا و چابک** (Python, JS, Ruby, PHP, Erlang, Elixir): انواع در زمان اجرا؛ کالکشن‌های همه‌کاره (مثل `list` پایتون یا `array` پی‌اچ‌پی که چند نقش را هم‌زمان ایفا می‌کند).
2. **ایستای شیءگرا** (Java, C#, Kotlin, Swift, Dart, Scala): انواع غنی از طریق کتابخانه؛ تفکیک ریز میان پیاده‌سازی‌ها (hash/درخت/مرتب/همگام).
3. **ایستای سیستم‌محور/تابعی با ADT** (Rust, Zig, C++, Haskell, Gleam): کنترل حافظه یا خالص‌گرایی؛ ADT + pattern matching به‌عنوان ابزار اصلی مدل‌سازی داده.

روندهای مشترک نسل جدید:

- **حذف null** و جایگزینی با `Optional`/`Option`/`Maybe`
- **خطا به‌عنوان مقدار**: `Result` (Rust, Swift, Gleam), `Either` (Haskell, Scala), تاپل‌های `{:ok, _}/{:error, _}` (Elixir)
- **تغییرناپذیری پیش‌فرض**: کالکشن‌های تغییرناپذیر در Scala/Elixir/Gleam/Haskell؛ رابط‌های فقط-خواندنی در Kotlin
- **ADT + pattern matching**: از Haskell/Rust به Swift، Kotlin (sealed)، TS (union)، Dart (sealed) و حتی Java (sealed) و C++ (`variant`) رسیده است
- **معناشناسی مقداری + COW**: Swift و Rust

راهنمای سریع انتخاب:

- ایمنی + ADT + بدون GC → **Rust**
- موبایل iOS/Android → **Swift / Kotlin**
- چندسکویی UI → **Dart**
- سیستم‌های همزمان توزیع‌شده → **Erlang / Elixir**
- سیستمی با کنترل دقیق حافظه → **C / C++ / Zig** (و Carbon در آینده)
- سازمانی/بزرگ‌مقیاس → **Java / C#**
- تحلیل داده و سریع‌ترین مسیر توسعه → **Python**
- وب فرانت‌اند → **JavaScript / TypeScript**
- کاربردی روی JVM با مدل تابعی → **Scala**
- صحت ریاضی و کد بسیار قابل‌اتکا → **Haskell**
- امن، کوچک و سریع روی BEAM/JS با تایپ ایستا → **Gleam**

---

## ۲۶. واژه‌نامه

| اصطلاح | توضیح |
|---|---|
| ADT (Algebraic Data Type) | نوع جبری — ترکیب sum و product type |
| Amortized | هزینهٔ میانگین‌گیری‌شده در طول زمان |
| COW (Copy-on-Write) | کپی فقط هنگام نوشتن — بهینه‌سازی value semantics |
| Hash table | جدول درهم‌سازی — دسترسی میانگین O(1) |
| Homogeneous / Heterogeneous | همگن (هم‌نوع) / ناهمگن |
| Immutable / Mutable | تغییرناپذیر / تغییرپذیر |
| Sum / Product type | نوع مجموع (یکی از حالت‌ها) / نوع ضرب (همهٔ فیلدها) |
| Type inference | استنتاج خودکار تایپ بدون انوتیشن صریح |
| Value / Reference semantics | کپی مقدار در انتساب / اشتراک ارجاع |
| Zero value | مقدار پیش‌فرض آمادهٔ نوع (مفهوم Go) |
| Sentinel | مقدار ویژهٔ پایان‌دهنده (مثل `\0` یا `[:0]u8` در Zig) |

---

*این سند برای مطالعه، کپی و توسعهٔ آزاد است. بخش Carbon بر پایهٔ مستندات طراحی آزمایشی است و در نسخه‌های بعدی زبان تغییر خواهد کرد.*

---

نکات مهم این سند:

- **۲۶ بخش**: مفاهیم پایه، ۲۱ بخش زبان‌به‌زبان (JavaScript و TypeScript جداگانه)، ماتریس مقایسهٔ سریع، ۹ جدول مقایسهٔ تفصیلی (آرایه، تاپل، Set، Map، Optional، رشته، ADT، Record، صف/پشته) و واژه‌نامه
- **هر زبان شامل**: پروفایل تایپ‌سیستم، جدول انواع اولیه، جدول کالکشن‌ها، انواع ویژه (Optional/Result/ADT)، مثال کد و نکات کلیدی
- ⚠️ **توجه**: بخش Carbon چون زبان هنوز نسخهٔ پایدار ندارد، صرفاً بر اساس مستندات طراحی آزمایشی نوشته شده و ممکن است outdated باشد.

اگر مایل باشید می‌توانم بخش خاصی را عمیق‌تر کنم (مثلاً مقایسهٔ عملکردی حافظه، یا افزودن زبان‌هایی مثل Julia، R، Lua، Nim یا F#).