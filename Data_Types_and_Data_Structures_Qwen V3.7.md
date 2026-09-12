# 📘 راهنمای جامع انواع داده (Data Types) در زبان‌های برنامه‌نویسی

> **نسخه:** 1.0  
> **تاریخ:** ۱۲ سپتامبر ۲۰۲۶  
> **زبان‌های پوشش‌داده‌شده:** Python, JavaScript/TypeScript, Java, C#, C++, C, Go, Rust, Kotlin, Swift, Dart, Ruby, PHP, Scala, Erlang, Elixir, Zig, Carbon, Gleam, Haskell

---

## فهرست مطالب

1. [مقدمه و دسته‌بندی انواع داده](#1-مقدمه-و-دسته-بندی-انواع-داده)
2. [انواع داده اولیه (Primitive Types)](#2-انواع-داده-اولیه)
3. [انواع داده مرکب (Composite Types)](#3-انواع-داده-مرکب)
4. [مجموعه‌ها (Collections)](#4-مجموعه‌ها)
5. [بررسی زبان‌به‌زبان](#5-بررسی-زبانبه-زبان)
6. [جدول مقایسه‌ای جامع](#6-جدول-مقایسه‌ای-جامع)
7. [جمع‌بندی و توصیه‌ها](#7-جمع‌بندی-و-توصیه‌ها)

---

## 1. مقدمه و دسته‌بندی انواع داده

**نوع داده (Data Type)** مشخص می‌کند که یک متغیر چه نوع مقداری را می‌تواند نگهداری کند، چه عملیاتی روی آن مجاز است و چقدر حافظه اشغال می‌کند.

### دسته‌بندی کلی

```
┌─────────────────────────────────────────────────────────┐
│                   انواع داده (Data Types)               │
├────────────────────┬────────────────────┬───────────────┤
│   Primitive        │   Composite        │  Collections  │
│   (اولیه)          │   (مرکب)           │  (مجموعه‌ها)   │
├────────────────────┼────────────────────┼───────────────┤
│ - Integer          │ - Tuple            │ - Array/List  │
│ - Float/Double     │ - Record/Struct    │ - Map/Dict    │
│ - Boolean          │ - Class/Object     │ - Set         │
│ - Character        │ - Union/Variant    │ - Queue/Stack │
│ - String           │ - Enum             │ - Tree/Graph  │
│ - Void/Unit        │ - Nullable         │               │
└────────────────────┴────────────────────┴───────────────┘
```

---

## 2. انواع داده اولیه

### 2.1 اعداد صحیح (Integer)

| زبان | نوع | اندازه | محدوده |
|------|------|--------|--------|
| **C** | `int`, `short`, `long`, `long long` | 16–64 بیت | بسته به پلتفرم |
| **C++** | `int`, `int8_t`, `int16_t`, `int32_t`, `int64_t` | دقیق | `-2^(n-1)` تا `2^(n-1)-1` |
| **Java** | `byte`, `short`, `int`, `long` | 8/16/32/64 بیت | ثابت |
| **C#** | `sbyte`, `short`, `int`, `long` | 8/16/32/64 بیت | ثابت |
| **Go** | `int`, `int8`, `int16`, `int32`, `int64` | متغیر/ثابت | - |
| **Rust** | `i8`, `i16`, `i32`, `i64`, `i128`, `isize` | 8–128 بیت | ثابت |
| **Kotlin** | `Byte`, `Short`, `Int`, `Long` | 8/16/32/64 بیت | ثابت |
| **Swift** | `Int8`, `Int16`, `Int32`, `Int64`, `Int` | متغیر/ثابت | - |
| **Python** | `int` | دلخواه (arbitrary precision) | نامحدود |
| **JavaScript** | `Number` (IEEE 754) / `BigInt` | 53/دلخواه بیت | - |
| **TypeScript** | `number`, `bigint` | - | - |
| **Ruby** | `Integer` | دلخواه | نامحدود |
| **PHP** | `int` | 64 بیت (معمولاً) | - |
| **Dart** | `int` | 64 بیت | - |
| **Scala** | `Byte`, `Short`, `Int`, `Long`, `BigInt` | - | - |
| **Haskell** | `Int`, `Integer` | ماشین/دلخواه | - |
| **Erlang/Elixir** | عدد صحیح | دلخواه | نامحدود |
| **Zig** | `i8`, `i16`, `i32`, `i64`, `i128` | دقیق | ثابت |
| **Carbon** | `i8`, `i16`, `i32`, `i64` | دقیق | ثابت |
| **Gleam** | `Int` | دلخواه | نامحدود |

### 2.2 اعداد اعشاری (Floating Point)

| زبان | نوع | دقت | استاندارد |
|------|------|------|-----------|
| **C/C++** | `float`, `double`, `long double` | 32/64/80+ بیت | IEEE 754 |
| **Java** | `float`, `double` | 32/64 بیت | IEEE 754 |
| **C#** | `float`, `double`, `decimal` | 32/64/128 بیت | `decimal` برای پول |
| **Go** | `float32`, `float64` | 32/64 بیت | IEEE 754 |
| **Rust** | `f32`, `f64` | 32/64 بیت | IEEE 754 |
| **Swift** | `Float`, `Double`, `Float80` | 32/64/80 بیت | - |
| **Kotlin** | `Float`, `Double` | 32/64 بیت | IEEE 754 |
| **Python** | `float` | 64 بیت | IEEE 754 |
| **JavaScript** | `Number` | 64 بیت | IEEE 754 |
| **Ruby** | `Float` | 64 بیت | IEEE 754 |
| **PHP** | `float` | پلتفرم‌وابسته | - |
| **Dart** | `double` | 64 بیت | IEEE 754 |
| **Scala** | `Float`, `Double`, `BigDecimal` | - | - |
| **Haskell** | `Float`, `Double`, `Rational` | - | دقیق |
| **Elixir** | `Float` | 64 بیت | IEEE 754 |
| **Zig** | `f16`, `f32`, `f64`, `f80`, `f128` | دقیق | - |
| **Carbon** | `f16`, `f32`, `f64`, `f128`, `f256` | دقیق | - |
| **Gleam** | `Float` | 64 بیت | IEEE 754 |

### 2.3 بولین (Boolean)

- **C**: `bool` (از C99، در `<stdbool.h>`) - در واقع `int` با مقادیر 0/1
- **C++**: `bool` - نوع مستقل
- **Java/C#/Kotlin**: `boolean` / `bool`
- **Go**: `bool`
- **Rust**: `bool`
- **Swift**: `Bool`
- **Python**: `bool` (زیرکلاس `int`)
- **JavaScript**: `boolean`
- **Ruby**: `TrueClass` / `FalseClass`
- **PHP**: `bool`
- **Dart**: `bool`
- **Scala**: `Boolean`
- **Haskell**: `Bool` (`True` / `False`)
- **Erlang/Elixir**: `true` / `false` (اتم‌های خاص)
- **Zig/Carbon/Gleam**: `bool`

### 2.4 کاراکتر و رشته (Character & String)

| زبان | کاراکتر | رشته | ویژگی |
|------|----------|------|--------|
| **C** | `char` (1 بایت) | `char*` / آرایه | بدون نوع اختصاصی رشته |
| **C++** | `char`, `wchar_t`, `char16_t`, `char32_t` | `std::string`, `std::string_view`, `std::wstring` | UTF-8/16/32 |
| **Java** | `char` (UTF-16, 2 بایت) | `String` (غیرقابل تغییر) | - |
| **C#** | `char` (UTF-16) | `string` | غیرقابل تغییر |
| **Go** | `rune` (alias `int32`) | `string` (UTF-8) | غیرقابل تغییر |
| **Rust** | `char` (4 بایت, Unicode Scalar) | `String`, `&str` | UTF-8 |
| **Swift** | `Character` | `String` | Unicode grapheme cluster |
| **Kotlin** | `Char` (UTF-16) | `String` | - |
| **Python** | - (کاراکتر مستقل ندارد) | `str` | Unicode، غیرقابل تغییر |
| **JavaScript** | - | `string` (UTF-16) | غیرقابل تغییر |
| **Ruby** | - | `String` | قابل تغییر، Encoding-aware |
| **PHP** | `string[0]` | `string` | بایت-محور |
| **Dart** | - | `String` (UTF-16) | غیرقابل تغییر |
| **Scala** | `Char` | `String` | - |
| **Haskell** | `Char` | `String` = `[Char]` | لیستی از کاراکتر |
| **Elixir** | - | `String` (UTF-8 binaries) | - |
| **Erlang** | - | list of integers / binaries | - |
| **Zig** | `u8` | `[]const u8`, `[]u8` | UTF-8 |
| **Carbon** | - | `String` | UTF-8 |
| **Gleam** | - | `String` | UTF-8 |

---

## 3. انواع داده مرکب

### 3.1 تاپل (Tuple)

تاپل مجموعه‌ای **مرتّب و غیرقابل تغییر** از عناصر با انواع مختلف است.

```python
# Python
point = (3, 4)
person: tuple[str, int, bool] = ("Ali", 30, True)
named = collections.namedtuple("Point", ["x", "y"])
```

```javascript
// JavaScript - تاپل اختصاصی ندارد، از آرایه استفاده می‌شود
const point = [3, 4];

// TypeScript
const point: [number, number] = [3, 4];
const person: [string, number, boolean] = ["Ali", 30, true];
```

```java
// Java - قبل از JDK 21: کلاس Record یا کتابخانه
record Point(int x, int y) {}
// JDK 21+: Pair/Tuple از طریق الگوها
```

```csharp
// C#
var point = (3, 4);
var person = (Name: "Ali", Age: 30, Active: true);
// System.ValueTuple<T1, T2, ...>
```

```cpp
// C++
#include <tuple>
auto t = std::make_tuple(3, 4.5, "hello");
std::tuple<int, double, std::string> t2{3, 4.5, "hello"};
```

```rust
// Rust
let point: (i32, i32) = (3, 4);
let mixed: (i32, f64, &str) = (3, 4.5, "hello");
```

```go
// Go - تاپل ندارد، چندمقدار بازگشتی دارد
func divide(a, b int) (int, int) { return a / b, a % b }
```

```swift
// Swift
let point: (Int, Int) = (3, 4)
let labeled: (x: Int, y: Int) = (3, 4)
```

```kotlin
// Kotlin
val pair = Pair(1, "one")
val triple = Triple(1, "one", true)
// برای بیش از 3 عنصر: data class
```

```dart
// Dart - تاپل ندارد، از Record (Dart 3+) استفاده می‌شود
var point = (3, 4);
var person = (name: "Ali", age: 30);
```

```ruby
# Ruby
point = [3, 4]
# یا با OpenStruct
```

```php
// PHP - تاپل ندارد
$point = [3, 4];
// PHP 8.1+: readonly class
```

```scala
// Scala
val point = (3, 4)
val tuple5 = (1, 2, 3, 4, 5) // تا 22 عنصر
```

```haskell
-- Haskell
point = (3, 4)
mixed = (3, 4.5, "hello")
```

```erlang
% Erlang
Point = {3, 4}.
Person = {person, "Ali", 30}. % تاپل برچسب‌دار
```

```elixir
# Elixir
point = {3, 4}
person = {"Ali", 30, true}
```

```zig
// Zig - تاپل دارد (از نسخه‌های اخیر)
const point = .{ @as(i32, 3), @as(i32, 4) };
```

```carbon
// Carbon
var point: (i32, i32) = (3, 4);
```

```gleam
// Gleam
let point = #(3, 4)
let person = #("Ali", 30, True)
```

### 3.2 ساختار / رکورد (Struct / Record)

```c
// C
struct Point {
    int x;
    int y;
};
```

```cpp
// C++
struct Point {
    int x, y;
};
// یا class
```

```rust
// Rust
struct Point {
    x: i32,
    y: i32,
}
// Tuple struct
struct Pair(i32, i32);
// Unit struct
struct Marker;
```

```go
// Go
type Point struct {
    X, Y int
}
```

```swift
// Swift
struct Point {
    var x: Int
    var y: Int
}
```

```kotlin
// Kotlin
data class Point(val x: Int, val y: Int)
```

```java
// Java (JDK 14+)
record Point(int x, int y) {}
```

```csharp
// C#
record Point(int X, int Y);
// یا struct
struct PointS { public int X, Y; }
```

```scala
// Scala
case class Point(x: Int, y: Int)
```

```dart
// Dart
class Point {
  final int x, y;
  Point(this.x, this.y);
}
// یا record (Dart 3)
```

```haskell
-- Haskell
data Point = Point { x :: Int, y :: Int }
```

### 3.3 Union / Variant / Sum Type

```rust
// Rust
enum Shape {
    Circle(f64),
    Rectangle(f64, f64),
}
```

```swift
// Swift
enum Shape {
    case circle(Double)
    case rectangle(Double, Double)
}
```

```typescript
// TypeScript
type Shape = 
  | { kind: "circle"; radius: number }
  | { kind: "rectangle"; width: number; height: number };
```

```scala
// Scala
sealed trait Shape
case class Circle(radius: Double) extends Shape
case class Rectangle(w: Double, h: Double) extends Shape
```

```kotlin
// Kotlin
sealed class Shape {
    data class Circle(val radius: Double) : Shape()
    data class Rectangle(val w: Double, val h: Double) : Shape()
}
```

```haskell
-- Haskell
data Shape = Circle Double | Rectangle Double Double
```

```ocaml-like
// Gleam
pub type Shape {
  Circle(Float)
  Rectangle(Float, Float)
}
```

```csharp
// C# - Discriminated Union (پیشنهادی/کتابخانه‌ای)
// در C# 12+ با الگوها
```

### 3.4 Nullable / Optional

| زبان | نحو | توضیح |
|------|------|--------|
| **Kotlin** | `String?` | نوع nullable |
| **Swift** | `String?` / `Optional<String>` | enum با `some`/`none` |
| **Rust** | `Option<T>` | enum با `Some(T)` / `None` |
| **Scala** | `Option[T]` | `Some(T)` / `None` |
| **Haskell** | `Maybe a` | `Just a` / `Nothing` |
| **Go** | pointer / zero value | `*T` یا `interface{}` |
| **Java** | `Optional<T>` | کلاس wrapper |
| **C#** | `T?` (برای value types) | `Nullable<T>` |
| **TypeScript** | `T \| null \| undefined` | union type |
| **Dart** | `String?` | null safety (Dart 2.12+) |
| **Elixir** | `nil` | مقدار خاص |
| **Erlang** | `undefined` | - |
| **Ruby** | `nil` | شیء از کلاس `NilClass` |
| **Python** | `None` / `Optional[T]` | - |
| **Gleam** | `Option(a)` | `Some(a)` / `None` |
| **Zig** | `?T` | optional type |
| **Carbon** | `Optional(T)` | - |

### 3.5 Enum

```rust
// Rust
enum Color { Red, Green, Blue }
enum Message { Quit, Move { x: i32, y: i32 }, Write(String) }
```

```swift
// Swift
enum Color { case red, green, blue }
enum Compass { case north, south, east, west }
```

```kotlin
// Kotlin
enum class Color { RED, GREEN, BLUE }
```

```java
// Java
enum Color { RED, GREEN, BLUE }
```

```csharp
// C#
enum Color { Red, Green, Blue }
```

```go
// Go - enum صریح ندارد، از iota استفاده می‌شود
const (
    Red = iota
    Green
    Blue
)
```

```scala
// Scala
object Color extends Enumeration {
  val Red, Green, Blue = Value
}
```

```dart
// Dart
enum Color { red, green, blue }
```

```typescript
// TypeScript
enum Color { Red, Green, Blue }
// یا string enum
enum Direction { Up = "UP", Down = "DOWN" }
```

```haskell
-- Haskell
data Color = Red | Green | Blue deriving (Eq, Show)
```

```elixir
# Elixir - اتم‌ها
:red, :green, :blue
```

```erlang
% Erlang
red, green, blue % اتم‌ها
```

---

## 4. مجموعه‌ها (Collections)

### 4.1 آرایه / لیست (Array / List)

#### آرایه ثابت (Fixed-size Array)

| زبان | نحو | ویژگی |
|------|------|--------|
| **C** | `int arr[10];` | اندازه ثابت، بدون bounds check |
| **C++** | `std::array<int, 10>` | اندازه ثابت در کامپایل |
| **Rust** | `[i32; 10]` | ایمن، bounds-checked |
| **Go** | `[10]int` | value type |
| **Swift** | - | آرایه پویا دارد |
| **Zig** | `[10]i32` | ثابت |
| **Carbon** | `[i32; 10]` | - |

#### لیست پویا (Dynamic Array / List)

| زبان | نوع | رشد خودکار |
|------|------|-------------|
| **Python** | `list` | ✅ (over-allocation) |
| **JavaScript** | `Array` | ✅ |
| **Java** | `ArrayList<T>` | ✅ |
| **C#** | `List<T>` | ✅ |
| **C++** | `std::vector<T>` | ✅ |
| **Go** | `[]T` (slice) | ✅ (با append) |
| **Rust** | `Vec<T>` | ✅ |
| **Kotlin** | `MutableList<T>` / `ArrayList<T>` | ✅ |
| **Swift** | `Array<T>` | ✅ |
| **Dart** | `List<T>` | ✅ |
| **Ruby** | `Array` | ✅ |
| **PHP** | `array` (indexed) | ✅ |
| **Scala** | `ArrayBuffer[T]`, `List[T]` | ✅ / immutable |
| **Haskell** | `[a]` | immutable linked list |
| **Elixir** | `List` | immutable linked list |
| **Erlang** | List | immutable linked list |
| **Zig** | `std.ArrayList(T)` | ✅ |
| **Gleam** | `List(a)` | immutable |

**مثال‌ها:**

```python
# Python
nums = [1, 2, 3]
nums.append(4)
```

```javascript
// JavaScript
const nums = [1, 2, 3];
nums.push(4);
```

```java
// Java
List<Integer> nums = new ArrayList<>(Arrays.asList(1, 2, 3));
nums.add(4);
```

```rust
// Rust
let mut nums = vec![1, 2, 3];
nums.push(4);
```

```go
// Go
nums := []int{1, 2, 3}
nums = append(nums, 4)
```

```haskell
-- Haskell
nums = [1, 2, 3] ++ [4]
```

```elixir
# Elixir
nums = [1, 2, 3] ++ [4]
```

### 4.2 نگاشت / دیکشنری (Map / Dictionary)

| زبان | نوع | مرتب؟ | Thread-safe؟ |
|------|------|--------|--------------|
| **Python** | `dict` | ✅ (از 3.7) | ❌ |
| **JavaScript** | `Map`, `Object` | ✅ (Map) | ❌ |
| **Java** | `HashMap`, `TreeMap`, `LinkedHashMap`, `ConcurrentHashMap` | بسته به نوع | ✅ (CHM) |
| **C#** | `Dictionary<K,V>`, `SortedDictionary`, `ConcurrentDictionary` | - | ✅ |
| **C++** | `std::map` (RB-tree), `std::unordered_map` (hash) | map: ✅ | ❌ |
| **Go** | `map[K]V` | ❌ | ❌ |
| **Rust** | `HashMap<K,V>`, `BTreeMap<K,V>` | BTreeMap: ✅ | ❌ |
| **Swift** | `Dictionary<K,V>` | ❌ | ❌ |
| **Kotlin** | `Map<K,V>`, `MutableMap`, `LinkedHashMap`, `TreeMap` | LinkedHashMap: ✅ | ❌ |
| **Dart** | `Map<K,V>`, `LinkedHashMap`, `SplayTreeMap` | LinkedHashMap: ✅ | ❌ |
| **Ruby** | `Hash` | ✅ (از 1.9) | ❌ |
| **PHP** | `array` (associative) | ✅ | ❌ |
| **Scala** | `Map[K,V]`, `HashMap`, `TreeMap`, `LinkedHashMap` | - | ✅ (immutable) |
| **Haskell** | `Map k v` (Data.Map), `HashMap` (unordered) | Map: ✅ | - |
| **Elixir** | `Map` | ❌ (order not guaranteed) | ✅ (immutable) |
| **Erlang** | `maps`, `dict`, `gb_trees` | - | ✅ |
| **Zig** | `std.HashMap(K,V, ...)` | ❌ | ❌ |
| **Gleam** | `Dict(k, v)` | ❌ | ✅ (immutable) |
| **Carbon** | - | - | - |

**مثال‌ها:**

```python
# Python
user = {"name": "Ali", "age": 30}
user["city"] = "Tehran"
```

```javascript
// JavaScript
const user = new Map();
user.set("name", "Ali");
// یا
const user2 = { name: "Ali", age: 30 };
```

```java
// Java
Map<String, Object> user = new HashMap<>();
user.put("name", "Ali");
```

```rust
// Rust
use std::collections::HashMap;
let mut user = HashMap::new();
user.insert("name", "Ali");
```

```go
// Go
user := map[string]any{
    "name": "Ali",
    "age":  30,
}
```

```elixir
# Elixir
user = %{name: "Ali", age: 30}
user = Map.put(user, :city, "Tehran")
```

```haskell
-- Haskell
import qualified Data.Map as M
user = M.fromList [("name", "Ali"), ("age", 30)]
```

### 4.3 مجموعه (Set)

| زبان | نوع | مرتب؟ |
|------|------|--------|
| **Python** | `set`, `frozenset` | ❌ |
| **JavaScript** | `Set`, `WeakSet` | ❌ (insertion order) |
| **Java** | `HashSet`, `TreeSet`, `LinkedHashSet` | بسته به نوع |
| **C#** | `HashSet<T>`, `SortedSet<T>` | - |
| **C++** | `std::set` (ordered), `std::unordered_set` | - |
| **Go** | - (با `map[K]struct{}` شبیه‌سازی) | - |
| **Rust** | `HashSet<T>`, `BTreeSet<T>` | - |
| **Swift** | `Set<T>` | ❌ |
| **Kotlin** | `Set<T>`, `MutableSet`, `TreeSet`, `LinkedHashSet` | - |
| **Dart** | `Set<T>`, `LinkedHashSet`, `SplayTreeSet` | - |
| **Ruby** | `Set` (کلاس استاندارد) | ❌ |
| **PHP** | `array_unique` / `SplObjectStorage` | - |
| **Scala** | `Set[T]`, `TreeSet`, `HashSet` | - |
| **Haskell** | `Set a` (Data.Set), `HashSet` | Set: ✅ |
| **Elixir** | `MapSet` | ❌ |
| **Erlang** | `sets`, `gb_sets` | - |
| **Zig** | `std.AutoHashMap(T, void)` | ❌ |
| **Gleam** | `Set(a)` | ❌ |

**مثال‌ها:**

```python
# Python
s = {1, 2, 3}
s.add(4)
```

```rust
// Rust
use std::collections::HashSet;
let mut s = HashSet::from([1, 2, 3]);
s.insert(4);
```

```elixir
# Elixir
s = MapSet.new([1, 2, 3])
s = MapSet.put(s, 4)
```

### 4.4 سایر مجموعه‌ها

#### صف (Queue) و پشته (Stack)

| زبان | Queue | Stack |
|------|-------|-------|
| **Python** | `collections.deque` | `list` (با `append`/`pop`) |
| **Java** | `Queue`, `LinkedList`, `ArrayDeque` | `Stack` (منسوخ) / `Deque` |
| **C++** | `std::queue`, `std::priority_queue` | `std::stack` |
| **C#** | `Queue<T>`, `PriorityQueue<T>` | `Stack<T>` |
| **Go** | با channel یا slice | با slice |
| **Rust** | `VecDeque<T>` | `Vec<T>` |
| **Elixir** | - | `[head \| tail]` (لیست) |
| **Erlang** | `queue` module | List |

#### Tuple / Record خاص

| زبان | نوع | توضیح |
|------|------|--------|
| **Elixir** | `Keyword List` | لیستی از تاپل‌های `{atom, value}` |
| **Erlang** | `proplists` | لیست property |
| **PHP** | `array` | هم آرایه هم دیکشنری |
| **JavaScript** | `WeakMap`, `WeakSet` | حافظه ضعیف |

---

## 5. بررسی زبان‌به‌زبان

### 5.1 Python

```python
# Primitive
x: int = 10
y: float = 3.14
b: bool = True
s: str = "hello"

# Composite
t: tuple[int, str] = (1, "a")
# Named tuple
from typing import NamedTuple
class Point(NamedTuple):
    x: int
    y: int

# Collections
lst: list[int] = [1, 2, 3]
d: dict[str, int] = {"a": 1}
st: set[int] = {1, 2, 3}
fs: frozenset[int] = frozenset([1, 2])

# Special
opt: int | None = None  # Python 3.10+
```

**ویژگی‌ها:**
- نوع‌دهی پویا (dynamic typing)
- type hints اختیاری
- همه چیز شیء است
- اعداد صحیح با دقت دلخواه

### 5.2 JavaScript / TypeScript

```javascript
// JavaScript
let n = 10;           // number
let s = "hello";      // string
let b = true;         // boolean
let arr = [1, 2, 3];  // array
let obj = { a: 1 };   // object
let m = new Map();
let st = new Set();
let sym = Symbol("id");
let big = 10n;        // BigInt
```

```typescript
// TypeScript
let n: number = 10;
let s: string = "hello";
let b: boolean = true;
let arr: number[] = [1, 2, 3];
let tuple: [string, number] = ["a", 1];
let obj: { name: string; age: number } = { name: "Ali", age: 30 };
let u: string | number = "hello";
type Result = { ok: true; data: string } | { ok: false; error: string };
```

**ویژگی‌ها:**
- همه چیز شیء است (حتی اعداد)
- `typeof null === "object"` (باگ تاریخی)
- TypeScript type system بسیار قدرتمند
- `Map` و `Set` از ES6

### 5.3 Java

```java
// Primitive
int n = 10;
double d = 3.14;
boolean b = true;
char c = 'A';

// Object
Integer nObj = 10;       // autoboxing
String s = "hello";

// Collections
List<Integer> list = new ArrayList<>();
Map<String, Integer> map = new HashMap<>();
Set<Integer> set = new HashSet<>();

// Record (JDK 14+)
record Point(int x, int y) {}

// Optional
Optional<String> opt = Optional.of("hello");

// Enum
enum Color { RED, GREEN, BLUE }
```

**ویژگی‌ها:**
- تمایز primitive/reference
- Generics (type erasure)
- Records برای داده‌های immutable
- Stream API

### 5.4 C#

```csharp
// Primitive
int n = 10;
double d = 3.14;
bool b = true;
char c = 'A';
decimal money = 99.99m;

// Nullable
int? nullableInt = null;
string? nullableString = null;

// Collections
List<int> list = new() { 1, 2, 3 };
Dictionary<string, int> dict = new() { ["a"] = 1 };
HashSet<int> set = new() { 1, 2, 3 };

// Tuple
var t = (1, "hello");
var named = (Name: "Ali", Age: 30);

// Record
record Point(int X, int Y);

// Pattern matching
object obj = 5;
if (obj is int i) Console.WriteLine(i);
```

**ویژگی‌ها:**
- value type (`struct`) vs reference type (`class`)
- `Nullable<T>` برای value types
- Records (C# 9+)
- Pattern matching پیشرفته

### 5.5 C++

```cpp
// Primitive
int n = 10;
double d = 3.14;
bool b = true;

// Containers
#include <vector>
#include <map>
#include <set>
#include <tuple>
#include <array>
#include <unordered_map>

std::vector<int> vec = {1, 2, 3};
std::array<int, 3> arr = {1, 2, 3};
std::map<std::string, int> m;
std::unordered_map<std::string, int> um;
std::set<int> s;
std::tuple<int, double, std::string> t{1, 2.0, "hi"};

// Optional, Variant, Any (C++17)
#include <optional>
#include <variant>
#include <any>

std::optional<int> opt = 5;
std::variant<int, std::string> v = "hello";
std::any a = 42;

// Smart pointers
std::unique_ptr<int> up = std::make_unique<int>(10);
std::shared_ptr<int> sp = std::make_shared<int>(10);
```

**ویژگی‌ها:**
- کنترل دقیق حافظه
- Templates برای generic programming
- RAII
- move semantics

### 5.6 C

```c
// Primitive
int n = 10;
double d = 3.14;
char c = 'A';
_Bool b = 1; // یا bool با <stdbool.h>

// Composite
struct Point { int x, y; };
union Value { int i; float f; char c; };
enum Color { RED, GREEN, BLUE };

// Array
int arr[10];
int matrix[3][4];

// Pointer
int *p = &n;

// String
char str[] = "hello";
```

**ویژگی‌ها:**
- پایین‌ترین سطح
- pointer-based
- بدون collections سطح بالا
- مدیریت دستی حافظه

### 5.7 Go

```go
// Primitive
var n int = 10
var f float64 = 3.14
var b bool = true
var s string = "hello"

// Composite
type Point struct {
    X, Y int
}

// Collections
arr := [3]int{1, 2, 3}         // array
slice := []int{1, 2, 3}        // slice
m := map[string]int{"a": 1}    // map

// Interface
var i interface{} = 42
var anyVal any = "hello" // Go 1.18+

// Channel
ch := make(chan int)

// Pointer
p := &n
```

**ویژگی‌ها:**
- slice به جای array پویا
- map داخلی
- interface ضمنی
- channel برای همزمانی
- بدون class، بدون inheritance

### 5.8 Rust

```rust
// Primitive
let n: i32 = 10;
let f: f64 = 3.14;
let b: bool = true;
let c: char = 'A';

// Composite
struct Point { x: i32, y: i32 }
enum Shape {
    Circle(f64),
    Rectangle(f64, f64),
}

// Collections
use std::collections::{HashMap, HashSet, BTreeMap, VecDeque};
let mut v: Vec<i32> = vec![1, 2, 3];
let mut m: HashMap<String, i32> = HashMap::new();
let mut s: HashSet<i32> = HashSet::new();

// Tuple
let t: (i32, f64, &str) = (1, 2.0, "hi");

// Option & Result
let opt: Option<i32> = Some(5);
let res: Result<i32, String> = Ok(10);

// Smart pointers
use std::rc::Rc;
use std::sync::Arc;
use std::boxed::Box;
let b = Box::new(5);
let rc = Rc::new(5);
```

**ویژگی‌ها:**
- مالکیت (ownership)
- borrow checker
- zero-cost abstractions
- `Option` و `Result` به جای null/exception
- lifetime

### 5.9 Kotlin

```kotlin
// Primitive (در JVM به صورت boxed/unboxed)
val n: Int = 10
val f: Double = 3.14
val b: Boolean = true
val c: Char = 'A'

// Nullable
val s: String? = null

// Collections
val list: List<Int> = listOf(1, 2, 3)
val mutableList: MutableList<Int> = mutableListOf(1, 2, 3)
val map: Map<String, Int> = mapOf("a" to 1)
val set: Set<Int> = setOf(1, 2, 3)

// Data class
data class Point(val x: Int, val y: Int)

// Sealed class
sealed class Result {
    data class Success(val data: String) : Result()
    data class Error(val msg: String) : Result()
}

// Pair & Triple
val p = Pair(1, "one")
val t = Triple(1, "one", true)
```

**ویژگی‌ها:**
- null safety در سطح زبان
- data class
- sealed class
- extension functions
- coroutine

### 5.10 Swift

```swift
// Primitive
let n: Int = 10
let f: Double = 3.14
let b: Bool = true
let c: Character = "A"
let s: String = "hello"

// Optional
var opt: String? = nil
if let value = opt { print(value) }

// Collections
let arr: [Int] = [1, 2, 3]
var dict: [String: Int] = ["a": 1]
let set: Set<Int> = [1, 2, 3]

// Tuple
let point: (Int, Int) = (3, 4)
let labeled: (x: Int, y: Int) = (3, 4)

// Struct
struct Point {
    var x: Int
    var y: Int
}

// Enum
enum Direction {
    case north, south, east, west
}

// Protocol
protocol Drawable {
    func draw()
}
```

**ویژگی‌ها:**
- value type پیش‌فرض برای struct
- optional chaining
- pattern matching
- protocol-oriented programming
- ARC

### 5.11 Dart

```dart
// Primitive
int n = 10;
double f = 3.14;
bool b = true;
String s = "hello";

// Nullable (null safety)
String? nullable = null;

// Collections
List<int> list = [1, 2, 3];
Map<String, int> map = {'a': 1};
Set<int> set = {1, 2, 3};

// Record (Dart 3+)
var point = (3, 4);
var person = (name: 'Ali', age: 30);

// Class
class Point {
  final int x, y;
  Point(this.x, this.y);
}

// Enum
enum Color { red, green, blue }

// Sealed class (Dart 3)
sealed class Result {}
class Success extends Result {}
class Error extends Result {}
```

**ویژگی‌ها:**
- sound null safety
- Records و Patterns (Dart 3)
- Dart 3 با sealed classes
- AOT و JIT compilation

### 5.12 Ruby

```ruby
# Primitive
n = 10            # Integer
f = 3.14          # Float
b = true          # TrueClass
s = "hello"       # String
sym = :symbol     # Symbol

# Collections
arr = [1, 2, 3]           # Array
hash = { "a" => 1 }       # Hash
set = Set.new([1, 2, 3])  # Set

# Range
r = 1..10

# Nil
x = nil  # NilClass

# Everything is an object
5.times { |i| puts i }
```

**ویژگی‌ها:**
- همه چیز شیء
- duck typing
- Hash به جای Map
- Symbol نوع خاصی است
- block و Proc

### 5.13 PHP

```php
// Scalar
$n = 10;             // int
$f = 3.14;           // float
$b = true;           // bool
$s = "hello";        // string

// Compound
$arr = [1, 2, 3];              // array (indexed)
$map = ["a" => 1, "b" => 2];   // array (associative)
$obj = new stdClass();

// PHP 7.4+ typed properties
class User {
    public int $id;
    public string $name;
}

// PHP 8+
enum Color { case Red; case Green; case Blue; }
readonly class Point { public function __construct(public int $x, public int $y) {} }

// Union types
function foo(int|string $x): int|false { ... }

// Null
$x = null;
```

**ویژگی‌ها:**
- array همه‌کاره (indexed + associative)
- type hints تدریجی
- attributes (PHP 8)
- enums (PHP 8.1)
- readonly classes (PHP 8.2)

### 5.14 Scala

```scala
// Primitive (همه چیز شیء)
val n: Int = 10
val f: Double = 3.14
val b: Boolean = true
val c: Char = 'A'

// Collections
val list: List[Int] = List(1, 2, 3)
val vector: Vector[Int] = Vector(1, 2, 3)
val map: Map[String, Int] = Map("a" -> 1)
val set: Set[Int] = Set(1, 2, 3)

// Tuple
val t = (1, "hello", true)
val first = t._1

// Case class
case class Point(x: Int, y: Int)

// Sealed trait
sealed trait Shape
case class Circle(r: Double) extends Shape
case class Rectangle(w: Double, h: Double) extends Shape

// Option
val opt: Option[Int] = Some(5)

// Either
val either: Either[String, Int] = Right(10)
```

**ویژگی‌ها:**
- ترکیب FP و OOP
- immutable collections پیش‌فرض
- case class
- pattern matching
- type classes (implicits/givens)

### 5.15 Erlang

```erlang
% Primitive
N = 10,              % integer (arbitrary precision)
F = 3.14,            % float
B = true,            % boolean (atom)
A = hello,           % atom
S = "hello",         % string (list of integers)

% Composite
Point = {3, 4},      % tuple
Person = {person, "Ali", 30},

% List
L = [1, 2, 3],
L2 = [H|T] = L,      % head/tail

% Map (ERLANG 17+)
M = #{name => "Ali", age => 30},

% Binary
Bin = <<"hello">>,

% Record
-record(person, {name, age}).
P = #person{name = "Ali", age = 30}.
```

**ویژگی‌ها:**
- immutable variables
- actor model
- pattern matching عمیق
- let-it-crash philosophy
- hot code swapping

### 5.16 Elixir

```elixir
# Primitive
n = 10            # Integer
f = 3.14          # Float
b = true          # Boolean
a = :atom         # Atom
s = "hello"       # String (UTF-8 binary)

# Composite
tuple = {1, 2, 3}
keyword = [name: "Ali", age: 30]  # [{:name, "Ali"}, {:age, 30}]

# Collections
list = [1, 2, 3]
map = %{name: "Ali", age: 30}
mapset = MapSet.new([1, 2, 3])

# Struct
defmodule User do
  defstruct [:name, :age]
end
u = %User{name: "Ali", age: 30}

# Pattern matching
%{name: name} = map

# Nil
x = nil
```

**ویژگی‌ها:**
- بر پایه BEAM VM
- immutable
- pattern matching
- pipe operator `|>`
- actor model (Erlang)
- metaprogramming با macros

### 5.17 Zig

```zig
// Primitive
const n: i32 = 10;
const f: f64 = 3.14;
const b: bool = true;
const c: u8 = 'A';

// Optional
var opt: ?i32 = null;

// Error Union
const FileError = error { NotFound, PermissionDenied };
fn read() FileError![]const u8 { ... }

// Composite
const Point = struct { x: i32, y: i32 };
const Shape = union(enum) {
    circle: f64,
    rectangle: struct { w: f64, h: f64 },
};

// Array & Slice
var arr: [3]i32 = .{ 1, 2, 3 };
const slice: []const i32 = arr[0..];

// Collections
const ArrayList = std.ArrayList;
const HashMap = std.HashMap;
var list = ArrayList(i32).init(allocator);
var map = HashMap([]const u8, i32, ...).init(allocator);

// Enum
const Color = enum { red, green, blue };
```

**ویژگی‌ها:**
- بدون hidden allocation
- comptime execution
- error union
- manual memory management با allocator
- no hidden control flow

### 5.18 Carbon

```carbon
// Primitive (طراحی در حال تکامل - تا 2026)
var n: i32 = 10;
var f: f64 = 3.14;
var b: bool = true;

// Optional
var opt: Optional(i32) = None;

// Class
class Point {
  var x: i32;
  var y: i32;
}

// Tuple
var t: (i32, f64) = (1, 2.0);

// Choice type (union)
choice Shape {
  circle(f64),
  rectangle(f64, f64),
}
```

**ویژگی‌ها:**
- جانشین مدرن برای C++
- interoperability با C++
- generics با interface
- طراحی در حال تکامل (experimental)

### 5.19 Gleam

```gleam
// Primitive
let n: Int = 10
let f: Float = 3.14
let b: Bool = True
let s: String = "hello"
let a: Atom = :hello

// Collections
let list: List(Int) = [1, 2, 3]
let tuple: #(Int, String) = #(1, "hello")
let dict: Dict(String, Int) = dict.new()
let set: Set(Int) = set.new()

// Custom type
pub type Shape {
  Circle(Float)
  Rectangle(Float, Float)
}

// Option
let opt: Option(Int) = Some(5)

// Result
let res: Result(Int, String) = Ok(10)

// Record
pub type User {
  User(name: String, age: Int)
}
```

**ویژگی‌ها:**
- روی BEAM VM اجرا می‌شود
- type inference قوی
- immutable
- pattern matching
- pipe operator `|>`
- syntax مدرن و تمیز

### 5.20 Haskell

```haskell
-- Primitive
n = 10 :: Int
f = 3.14 :: Double
b = True :: Bool
c = 'A' :: Char
s = "hello" :: String  -- [Char]

-- Tuple
t = (1, "hello", True) :: (Int, String, Bool)

-- List
lst = [1, 2, 3] :: [Int]

-- Map
import qualified Data.Map as M
m = M.fromList [("a", 1), ("b", 2)] :: M.Map String Int

-- Set
import qualified Data.Set as S
st = S.fromList [1, 2, 3] :: S.Set Int

-- Algebraic Data Type
data Shape = Circle Double | Rectangle Double Double

-- Maybe
mb = Just 5 :: Maybe Int

-- Either
e = Right 10 :: Either String Int

-- Type class
class Eq a where
  (==) :: a -> a -> Bool
```

**ویژگی‌ها:**
- pure functional
- lazy evaluation
- type classes
- monads
- strong static typing
- Hindley-Milner type inference

---

## 6. جدول مقایسه‌ای جامع

### 6.1 مقایسه Collections

| زبان | Array/List | Map/Dict | Set | Tuple | Queue |
|------|------------|----------|-----|-------|-------|
| **Python** | `list` | `dict` | `set` | `tuple` | `deque` |
| **JavaScript** | `Array` | `Map`/`{}` | `Set` | `[]` | - |
| **TypeScript** | `T[]` | `Map<K,V>` | `Set<T>` | `[A,B]` | - |
| **Java** | `List` | `Map` | `Set` | `Pair`/`record` | `Queue` |
| **C#** | `List<T>` | `Dictionary` | `HashSet` | `(,)` | `Queue<T>` |
| **C++** | `vector` | `map`/`unordered_map` | `set` | `tuple` | `queue` |
| **C** | `array` | - | - | `struct` | - |
| **Go** | `[]T` | `map[K]V` | `map[K]struct{}` | - | `channel` |
| **Rust** | `Vec<T>` | `HashMap` | `HashSet` | `(,)` | `VecDeque` |
| **Kotlin** | `List` | `Map` | `Set` | `Pair`/`Triple` | - |
| **Swift** | `Array` | `Dictionary` | `Set` | `(,)` | - |
| **Dart** | `List` | `Map` | `Set` | `Record` | - |
| **Ruby** | `Array` | `Hash` | `Set` | `Array` | - |
| **PHP** | `array` | `array` | - | - | `SplQueue` |
| **Scala** | `List`/`Vector` | `Map` | `Set` | `Tuple` | - |
| **Haskell** | `[]` | `Data.Map` | `Data.Set` | `(,)` | - |
| **Elixir** | `List` | `Map` | `MapSet` | `{,}` | - |
| **Erlang** | `list` | `maps` | `sets` | `{,}` | `queue` |
| **Zig** | `ArrayList` | `HashMap` | - | `.{,}` | - |
| **Gleam** | `List` | `Dict` | `Set` | `#(,)` | - |

### 6.2 مقایسه نوع‌دهی

| زبان | نوع‌دهی | Null Safety | Generics | Pattern Matching |
|------|---------|-------------|----------|------------------|
| **Python** | Dynamic | Optional hints | No | ✅ (3.10+) |
| **JavaScript** | Dynamic | ❌ | ❌ | ❌ |
| **TypeScript** | Static (erased) | ✅ | ✅ | ✅ (limited) |
| **Java** | Static | Optional | ✅ (erased) | ✅ (21+) |
| **C#** | Static | ✅ (nullable ref) | ✅ (reified) | ✅ |
| **C++** | Static | Optional | ✅ | ✅ (limited) |
| **C** | Static | ❌ | ❌ | ❌ |
| **Go** | Static | ❌ | ✅ (1.18+) | ✅ (type switch) |
| **Rust** | Static | ✅ (`Option`) | ✅ (monomorphized) | ✅ |
| **Kotlin** | Static | ✅ | ✅ (erased) | ✅ |
| **Swift** | Static | ✅ | ✅ | ✅ |
| **Dart** | Sound static | ✅ | ✅ | ✅ (3+) |
| **Ruby** | Dynamic | ❌ | ❌ | ✅ (case/in) |
| **PHP** | Gradual | ❌ | ❌ | ✅ (8+) |
| **Scala** | Static | ✅ (`Option`) | ✅ | ✅ |
| **Haskell** | Static | ✅ (`Maybe`) | ✅ | ✅ |
| **Elixir** | Dynamic | ✅ (`nil`) | ❌ | ✅ |
| **Erlang** | Dynamic | ❌ | ❌ | ✅ |
| **Zig** | Static | ✅ (`?T`) | ✅ (comptime) | ✅ |
| **Carbon** | Static | ✅ (`Optional`) | ✅ | ✅ |
| **Gleam** | Static | ✅ (`Option`) | ✅ | ✅ |

### 6.3 مقایسه ویژگی‌های خاص

| زبان | Immutable Default | Concurrency Model | Memory Model |
|------|-------------------|-------------------|--------------|
| **Python** | ❌ | GIL + threads | GC |
| **JavaScript** | ❌ | Event loop | GC |
| **Java** | ❌ | Threads + virtual threads | GC |
| **C#** | ❌ | Threads + async/await | GC |
| **C++** | ❌ | Threads | Manual |
| **C** | ❌ | Threads | Manual |
| **Go** | ❌ | Goroutines + channels | GC |
| **Rust** | ❌ (by default) | async + threads | Manual (ownership) |
| **Kotlin** | ❌ | Coroutines | GC |
| **Swift** | ❌ | async/await | ARC |
| **Dart** | ❌ | Isolates + async | GC |
| **Ruby** | ❌ | Threads + Ractors | GC |
| **PHP** | ❌ | Process-per-request | GC |
| **Scala** | ✅ (collections) | Futures + Akka | GC |
| **Haskell** | ✅ | STM + sparks | GC (lazy) |
| **Elixir** | ✅ | Actors (BEAM) | GC (per-process) |
| **Erlang** | ✅ | Actors (BEAM) | GC (per-process) |
| **Zig** | ❌ | async (removed) | Manual (allocator) |
| **Carbon** | ❌ | - | - |
| **Gleam** | ✅ | Actors (BEAM) | GC (per-process) |

---

## 7. جمع‌بندی و توصیه‌ها

### 7.1 انتخاب زبان بر اساس نیاز

| نیاز | زبان پیشنهادی |
|------|----------------|
| **سیستمی و عملکرد بالا** | C, C++, Rust, Zig |
| **وب و frontend** | JavaScript, TypeScript |
| **Backend عمومی** | Python, Go, Java, C#, Kotlin |
| **همزمانی بالا** | Erlang, Elixir, Go |
| **برنامه‌نویسی تابعی خالص** | Haskell, Elixir, Gleam |
| **موبایل** | Swift (iOS), Kotlin (Android), Dart (Flutter) |
| **علم داده** | Python, Scala |
| **امنیت نوع بالا** | Rust, Haskell, TypeScript |
| **ساده‌گرایی** | Go, Python |
| **آینده‌نگر** | Carbon, Gleam, Zig |

### 7.2 روندهای مدرن (تا 2026)

1. **Null Safety**: اکثر زبان‌های جدید (Kotlin, Swift, Dart, Rust) null safety را در سطح زبان پیاده کرده‌اند.
2. **Pattern Matching**: از یک ویژگی niche به یک استاندارد تبدیل شده است.
3. **Algebraic Data Types**: enumهای غنی (Rust, Swift, Scala) رایج شده‌اند.
4. **Immutability**: زبان‌های جدید به طور پیش‌فرض immutable هستند.
5. **Type Inference**: حتی زبان‌های static typing به سمت inference قوی حرکت کرده‌اند.
6. **Records/Tuples**: افزودن نوع‌های داده‌ای سبک (C# records, Dart records, Java records).
7. **Gradual Typing**: PHP, Python, JavaScript در حال افزودن type hints هستند.

### 7.3 نکات کلیدی

- **هیچ زبان کاملی وجود ندارد** - هر زبان trade-offهای خاص خود را دارد.
- **نوع داده مناسب = کد بهتر** - انتخاب نوع داده درست، خوانایی و عملکرد را بهبود می‌دهد.
- **Immutable داده‌ها = همزمانی آسان‌تر** - در برنامه‌های concurrent.
- **Type System قوی = باگ کمتر** - بسیاری از خطاها در زمان کامپایل کشف می‌شوند.

---

## منابع و مراجع

- مستندات رسمی هر زبان
- "Programming Language Pragmatics" - Michael L. Scott
- "Types and Programming Languages" - Benjamin C. Pierce
- "Crafting Interpreters" - Robert Nystrom
- [https://en.wikipedia.org/wiki/Comparison_of_programming_languages](https://en.wikipedia.org/wiki/Comparison_of_programming_languages)

---

> 📝 **توجه:** این راهنما تا سپتامبر 2026 به‌روز شده است. برخی زبان‌ها مانند Carbon همچنان در حال توسعه هستند و ممکن است ویژگی‌های جدیدی اضافه شود.

**پایان سند**