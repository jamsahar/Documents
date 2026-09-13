# درس دوم — ساختارهای داده (Data Structures) و مقایسه زبان‌ها

## فهرست مطالب
1. مقدمه
2. Array
3. List و Linked List
4. Vector و Dynamic Array
5. Stack
6. Queue
7. Deque
8. Set
9. Hash Table
10. Map / Dictionary
11. Tree
12. Binary Search Tree
13. AVL و Red-Black Tree
14. Heap و Priority Queue
15. Graph
16. Trie
17. B-Tree و B+Tree
18. Skip List
19. Union-Find
20. Segment Tree و Fenwick Tree
21. Persistent Data Structures
22. Probabilistic Data Structures
23. مقایسه پیچیدگی زمانی
24. مقایسه جامع ۲۰ زبان برنامه‌نویسی
25. جمع‌بندی

---

## 1. مقدمه

**Data Structure** روشی برای سازمان‌دهی و نگهداری داده است تا عملیات‌هایی مانند دسترسی، جست‌وجو، درج، حذف و پیمایش با هزینه مناسب انجام شوند.

تفاوت مهم:

```text
Data Type  = ماهیت و نوع مقدار
Data Structure = سازمان‌دهی مجموعه‌ای از مقادیر
Algorithm = روش پردازش آن داده
```

ساختار مناسب مستقیماً روی Performance، Memory Usage، Scalability و سادگی الگوریتم اثر می‌گذارد.

---

## 2. Array

Array مجموعه‌ای از عناصر با دسترسی index-based است.

ویژگی‌های معمول:
- دسترسی تصادفی سریع: O(1)
- حافظه پیوسته در بسیاری از پیاده‌سازی‌ها
- اندازه ثابت در بسیاری از زبان‌ها
- مناسب برای cache locality

| زبان | Array |
|---|---|
| Python | `list` به‌عنوان sequence پویا؛ `array` کتابخانه‌ای |
| JavaScript/TypeScript | `Array` |
| Java | `T[]` |
| C# | `T[]` |
| C++ | built-in array, `std::array` |
| C | C arrays |
| Go | `[N]T` |
| Rust | `[T; N]` |
| Kotlin | `Array<T>`, primitive arrays |
| Swift | `Array` |
| Dart | `List` |
| Ruby | `Array` |
| PHP | `array` (ordered map-like) |
| Scala | `Array[T]` |
| Erlang | tuple/list/binary؛ array سنتی نوع اصلی نیست |
| Elixir | list/tuple؛ array سنتی نوع اصلی نیست |
| Zig | `[N]T` |
| Carbon | در حال تکامل |
| Haskell | Arrayها و sequenceهای کتابخانه‌ای |
| Gleam | List؛ array به شکل کلاسیک ساختار اصلی نیست |

---

## 3. List و Linked List

List بسته به زبان می‌تواند linked list یا dynamic sequence باشد.

### Linked List

هر node معمولاً شامل داده و reference به node بعدی است.

| عملیات | Singly Linked List |
|---|---:|
| Access | O(n) |
| Search | O(n) |
| Insert at head | O(1) |
| Delete at head | O(1) |
| Insert after known node | O(1) |

| زبان | List / Linked List |
|---|---|
| Python | `list` linked list نیست؛ dynamic array است |
| JavaScript/TypeScript | `Array`؛ linked list معمولاً دستی/کتابخانه |
| Java | `LinkedList` |
| C# | `LinkedList<T>` |
| C++ | `std::list`, `std::forward_list` |
| C | دستی با struct + pointer |
| Go | `container/list` |
| Rust | `LinkedList` در std وجود دارد، ولی `Vec` معمولاً انتخاب رایج‌تری است |
| Kotlin | collections/JVM، `LinkedList` از Java نیز قابل استفاده |
| Swift | Array رایج‌تر؛ linked list معمولاً دستی/کتابخانه |
| Dart | `List`؛ linked list معمولاً library/custom |
| Ruby | `Array`؛ linked list معمولاً custom |
| PHP | `array` یا `SplDoublyLinkedList` |
| Scala | `List` ذاتاً immutable linked list است |
| Erlang | `list` یک ساختار linked-list-like و immutable است |
| Elixir | `list` یک ساختار linked-list-like و immutable است |
| Zig | معمولاً با pointer/struct یا library |
| Carbon | در حال تکامل |
| Haskell | `[]` لیست immutable و linked-list-like |
| Gleam | `List` immutable |

---

## 4. Vector و Dynamic Array

Dynamic Array ظرفیت داخلی بیشتری نگه می‌دارد و هنگام پرشدن resize می‌شود.

| عملیات | Dynamic Array |
|---|---:|
| Index access | O(1) |
| Append amortized | O(1) |
| Insert middle | O(n) |
| Delete middle | O(n) |
| Search unsorted | O(n) |

| زبان | نمونه |
|---|---|
| Python | `list` |
| JavaScript/TypeScript | `Array` |
| Java | `ArrayList` |
| C# | `List<T>` |
| C++ | `std::vector` |
| C | custom dynamic array |
| Go | `slice` |
| Rust | `Vec<T>` |
| Kotlin | `MutableList`, `ArrayList` |
| Swift | `Array` |
| Dart | `List` |
| Ruby | `Array` |
| PHP | `array` |
| Scala | `ArrayBuffer`, `Vector` |
| Erlang | list؛ array-like structures via libraries |
| Elixir | list؛ arrays سنتی نیستند |
| Zig | dynamic array structures مانند `ArrayList` در نسخه‌های مربوطه |
| Carbon | در حال تکامل |
| Haskell | `Vector` library |
| Gleam | `List` و ساختارهای library |

---

## 5. Stack

Stack از اصل **LIFO** استفاده می‌کند.

کاربردها:
- Call stack
- Undo/Redo
- Parsing
- DFS
- Expression evaluation

| زبان | پیاده‌سازی رایج |
|---|---|
| Python | `list` |
| JS/TS | `Array` |
| Java | `Deque` / `ArrayDeque` |
| C# | `Stack<T>` |
| C++ | `std::stack` |
| C | array/linked list دستی |
| Go | slice |
| Rust | `Vec` |
| Kotlin | MutableList/ArrayDeque |
| Swift | Array |
| Dart | List |
| Ruby | Array |
| PHP | array |
| Scala | collections |
| Erlang | list |
| Elixir | list |
| Zig | array/slice/library |
| Carbon | evolving |
| Haskell | list/custom structures |
| Gleam | List/custom structures |

---

## 6. Queue

Queue از اصل **FIFO** استفاده می‌کند.

کاربرد:
- Job processing
- BFS
- Message processing
- Scheduling

| زبان | پیاده‌سازی رایج |
|---|---|
| Python | `collections.deque` |
| JS/TS | Array یا library |
| Java | `Queue`, `ArrayDeque` |
| C# | `Queue<T>` |
| C++ | `std::queue` |
| C | array/circular buffer/manual |
| Go | slice/channel/library |
| Rust | `VecDeque` |
| Kotlin | ArrayDeque |
| Swift | Array/custom deque |
| Dart | Queue |
| Ruby | Array |
| PHP | `SplQueue` |
| Scala | Queue collections |
| Erlang | `queue` |
| Elixir | `:queue` |
| Zig | library/custom |
| Carbon | evolving |
| Haskell | library structures |
| Gleam | library/custom |

---

## 7. Deque

Deque امکان افزودن و حذف از هر دو طرف را فراهم می‌کند.

| زبان | نمونه |
|---|---|
| Python | `collections.deque` |
| Java | `ArrayDeque` |
| C# | library/custom |
| C++ | `std::deque` |
| Go | library/custom |
| Rust | `VecDeque` |
| Kotlin | `ArrayDeque` |
| Swift | custom/library |
| Dart | `Queue` |
| PHP | SPL structures |
| Scala | collections |
| Erlang | `queue` |
| Elixir | `:queue` |
| Zig | library/custom |
| Carbon | evolving |
| Haskell | library |
| Gleam | library/custom |

---

## 8. Set

Set داده‌های یکتا را نگه می‌دارد.

عملیات مهم:
- Membership
- Union
- Intersection
- Difference

| زبان | Set |
|---|---|
| Python | `set` |
| JavaScript/TypeScript | `Set` |
| Java | `Set`, `HashSet`, `TreeSet` |
| C# | `HashSet<T>` |
| C++ | `std::set`, `std::unordered_set` |
| C | library/custom |
| Go | معمولاً `map[T]struct{}` |
| Rust | `HashSet`, `BTreeSet` |
| Kotlin | `Set`, `HashSet` |
| Swift | `Set` |
| Dart | `Set` |
| Ruby | `Set` |
| PHP | library/SPL/custom patterns |
| Scala | `Set` |
| Erlang | `sets` |
| Elixir | `MapSet` |
| Zig | hash-map/set structures در std |
| Carbon | evolving |
| Haskell | `Data.Set` |
| Gleam | Set در standard/library ecosystem |

---

## 9. Hash Table

Hash Table داده را با تابع hash سازمان‌دهی می‌کند.

میانگین عملیات:

```text
Lookup  ≈ O(1)
Insert  ≈ O(1)
Delete  ≈ O(1)
```

در بدترین حالت می‌تواند O(n) شود.

مفاهیم مهم:
- Hash Function
- Collision
- Load Factor
- Rehashing
- Bucket
- Open Addressing
- Chaining

| زبان | Hash Table |
|---|---|
| Python | `dict`, `set` |
| JS/TS | `Map`, `Set` |
| Java | `HashMap`, `HashSet` |
| C# | `Dictionary`, `HashSet` |
| C++ | `unordered_map`, `unordered_set` |
| C | custom/library |
| Go | `map` |
| Rust | `HashMap`, `HashSet` |
| Kotlin | `HashMap`, `HashSet` |
| Swift | `Dictionary`, `Set` |
| Dart | `Map`, `Set` |
| Ruby | `Hash`, `Set` |
| PHP | `array` + hash-table implementation |
| Scala | `HashMap`, `HashSet` |
| Erlang | `map`, ETS |
| Elixir | `Map`, ETS |
| Zig | hash map structures |
| Carbon | evolving |
| Haskell | `HashMap` library |
| Gleam | Map |

---

## 10. Map / Dictionary

Map رابطه key/value را نگه می‌دارد.

| زبان | Map |
|---|---|
| Python | `dict` |
| JavaScript/TypeScript | `Map` / object |
| Java | `Map`, `HashMap` |
| C# | `Dictionary<TKey,TValue>` |
| C++ | `map`, `unordered_map` |
| C | custom |
| Go | `map[K]V` |
| Rust | `HashMap`, `BTreeMap` |
| Kotlin | `Map`, `HashMap` |
| Swift | `Dictionary` |
| Dart | `Map` |
| Ruby | `Hash` |
| PHP | `array` |
| Scala | `Map` |
| Erlang | `map()` |
| Elixir | `Map` |
| Zig | hash maps |
| Carbon | evolving |
| Haskell | `Map`, `HashMap` libraries |
| Gleam | `Map` |

---

## 11. Tree

Tree ساختاری سلسله‌مراتبی است.

کاربرد:
- File systems
- AST
- Organization hierarchy
- Indexes
- Decision trees

انواع مهم:
- Binary Tree
- BST
- AVL
- Red-Black
- B-Tree
- B+Tree
- Trie
- Segment Tree

---

## 12. Binary Search Tree

BST شرط زیر را دارد:

```text
left < node < right
```

در BST متوازن:

```text
Search ≈ O(log n)
Insert ≈ O(log n)
Delete ≈ O(log n)
```

اما BST نامتوازن می‌تواند به O(n) برسد.

---

## 13. AVL و Red-Black Tree

هر دو balanced search tree هستند.

| ویژگی | AVL | Red-Black |
|---|---|---|
| Balance | سخت‌گیرانه‌تر | انعطاف‌پذیرتر |
| Search | عالی | عالی |
| Updates | rotation بیشتر ممکن است | معمولاً مناسب update |
| کاربرد | lookup-heavy | general-purpose ordered map/set |

در بسیاری از زبان‌ها مستقیماً API یکسانی برای این دو وجود ندارد و implementation در library/runtime متفاوت است.

---

## 14. Heap و Priority Queue

Heap برای Priority Queue بسیار مناسب است.

### Min Heap

```text
parent <= children
```

### Max Heap

```text
parent >= children
```

| عملیات | پیچیدگی معمول |
|---|---:|
| Peek | O(1) |
| Insert | O(log n) |
| Extract | O(log n) |
| Build Heap | O(n) |

| زبان | Priority Queue / Heap |
|---|---|
| Python | `heapq` |
| JS/TS | library |
| Java | `PriorityQueue` |
| C# | `PriorityQueue` |
| C++ | `priority_queue` |
| C | custom |
| Go | `container/heap` |
| Rust | `BinaryHeap` |
| Kotlin | Java collections/library |
| Swift | library/custom |
| Dart | library/custom |
| Ruby | library/custom |
| PHP | `SplPriorityQueue` |
| Scala | `PriorityQueue` |
| Erlang | `gb_trees`/queue/library patterns |
| Elixir | Erlang/Elixir libraries |
| Zig | library |
| Carbon | evolving |
| Haskell | priority-queue libraries |
| Gleam | library |

---

## 15. Graph

Graph از node/vertex و edge تشکیل می‌شود.

انواع:
- Directed
- Undirected
- Weighted
- Unweighted
- Cyclic
- Acyclic
- DAG

نمایش:

### Adjacency Matrix

فضای تقریبی:

```text
O(V²)
```

### Adjacency List

فضای تقریبی:

```text
O(V + E)
```

| زبان | Graph |
|---|---|
| Python | library/custom |
| JS/TS | library/custom |
| Java | library/custom |
| C# | library/custom |
| C++ | STL containers + custom |
| C | custom |
| Go | custom/library |
| Rust | crates/custom |
| Kotlin | library/custom |
| Swift | custom/library |
| Dart | custom/library |
| Ruby | custom/library |
| PHP | custom/library |
| Scala | collections/library |
| Erlang | graph libraries |
| Elixir | graph libraries |
| Zig | custom/library |
| Carbon | evolving |
| Haskell | graph libraries |
| Gleam | graph libraries |

---

## 16. Trie

Trie برای جست‌وجوی prefix بسیار مناسب است.

کاربرد:
- Autocomplete
- Dictionary
- Routing
- Token prefix search

زمان جست‌وجوی یک رشته معمولاً به طول رشته وابسته است:

```text
O(L)
```

---

## 17. B-Tree و B+Tree

برای storage و database بسیار مهم‌اند.

ویژگی:
- branching factor بالا
- کاهش تعداد disk/page access
- مناسب indexهای بزرگ

**B+Tree** معمولاً داده‌های واقعی را در leafها نگه می‌دارد و leafها را برای range scan به هم متصل می‌کند.

---

## 18. Skip List

ساختاری probabilistic برای sequence مرتب است.

پیچیدگی مورد انتظار:

```text
Search  O(log n)
Insert  O(log n)
Delete  O(log n)
```

برای بعضی سیستم‌های in-memory و concurrent کاربرد دارد.

---

## 19. Union-Find

برای مسئله‌های connectivity مناسب است.

عملیات:
- `find`
- `union`

با path compression و union by rank/size، هزینه amortized بسیار نزدیک به O(1) است:

```text
O(α(n))
```

---

## 20. Segment Tree و Fenwick Tree

### Segment Tree

برای range query و update:

```text
Query  O(log n)
Update O(log n)
```

### Fenwick Tree

برای prefix sums و برخی عملیات تجمعی:

```text
Query  O(log n)
Update O(log n)
```

---

## 21. Persistent Data Structures

ساختاری است که نسخه‌های قبلی داده را حفظ می‌کند.

ویژگی:
- immutable
- versioned
- structural sharing

در Functional Programming بسیار مهم است.

زبان‌های مهم برای مطالعه:
- Haskell
- Scala
- Rust
- Gleam
- Elixir

---

## 22. Probabilistic Data Structures

| ساختار | کاربرد |
|---|---|
| Bloom Filter | membership تقریبی |
| Count-Min Sketch | frequency تقریبی |
| HyperLogLog | cardinality تقریبی |
| Cuckoo Filter | membership |
| Skip List | ordered probabilistic structure |

مزیت اصلی: کاهش حافظه و افزایش سرعت با پذیرش خطای کنترل‌شده.

---

## 23. مقایسه پیچیدگی زمانی

| ساختار | Access | Search | Insert | Delete |
|---|---:|---:|---:|---:|
| Array | O(1) | O(n) | O(n) | O(n) |
| Dynamic Array append | O(1) | O(n) | amortized O(1) | O(n) |
| Linked List | O(n) | O(n) | O(1) با node | O(1) با node |
| Hash Table | — | avg O(1) | avg O(1) | avg O(1) |
| Balanced BST | — | O(log n) | O(log n) | O(log n) |
| Heap | root O(1) | O(n) | O(log n) | O(log n) |
| Trie | — | O(L) | O(L) | O(L) |

---

# 24. مقایسه جامع ۲۰ زبان برنامه‌نویسی

زبان‌های مورد بررسی:

**Python، JavaScript/TypeScript، Java، C#، C++، C، Go، Rust، Kotlin، Swift، Dart، Ruby، PHP، Scala، Erlang، Elixir، Zig، Carbon، Haskell، Gleam**

> **Carbon:** وضعیت آن evolving است؛ جدول‌های مربوط به Carbon مفهومی هستند و نباید API یا syntax آن را مانند زبان‌های بالغ فرض کرد.

## 24.1 مقایسه کلی

| ویژگی | Python | JS/TS | Java | C# | C++ | C | Go | Rust | Kotlin | Swift | Dart | Ruby | PHP | Scala | Erlang | Elixir | Zig | Carbon | Haskell | Gleam |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Type System | Dynamic/Gradual | Dynamic + TS static | Static | Static | Static | Static | Static | Static | Static | Static | Static | Dynamic | Dynamic | Static | Dynamic | Dynamic | Static | evolving | Static | Static |
| GC | Yes | Yes | Yes | Yes | No | No | Yes | No | Yes | ARC | Yes | GC | GC | Yes | Yes | Yes | No | evolving | GC | GC/managed runtime |
| Ownership | No | No | GC | GC | RAII | Manual | GC | Yes | GC | ARC/value semantics | GC | GC | GC | GC | VM-managed | VM-managed | Explicit allocator | evolving | GC | managed |
| Pointer | محدود | reference model | reference | reference | Yes | Yes | Yes | raw/reference | reference | unsafe pointers | محدود | reference | reference | reference | hidden | hidden | Yes | evolving | reference/managed | managed |
| Generics | typing | generics | generics | generics | templates | macros/manual | generics | generics | generics | generics | generics | generics | generics | generics | patterns/modules | protocols/macros | comptime | evolving | typeclasses | generics |
| Array | list/array | Array | array | array | array/vector | array | array/slice | array/Vec | Array | Array | List | Array | array | Array | tuple/list | tuple/list | array/slice | evolving | Array | List |
| Map | dict | Map/object | HashMap | Dictionary | map/unordered_map | custom | map | HashMap | Map | Dictionary | Map | Hash | array/hash | Map | map | Map | hash maps | evolving | Map | Map |
| Set | set | Set | HashSet | HashSet | set/unordered_set | custom | map pattern | HashSet | Set | Set | Set | Set | library/custom | Set | sets | MapSet | library | evolving | Set | Set |
| Tuple | native | TS tuple | record/class | ValueTuple | tuple | no | no | native | Pair/data classes | tuple-like constructs | record/class | Array | array | native | native | native | tuple | evolving | native | tuple |
| Functional Style | متوسط | زیاد | زیاد | زیاد | زیاد | کم | متوسط | زیاد | زیاد | زیاد | متوسط | متوسط | متوسط | بسیار زیاد | بسیار زیاد | بسیار زیاد | متوسط | evolving | بسیار زیاد | بسیار زیاد |
| Concurrency | threads/async | event loop | threads/futures | Task | threads/coroutines | threads | goroutines | async/threads | coroutines | async/tasks | isolates/async | threads/processes | processes/extensions | Futures/actors | processes | processes | threads/async patterns | evolving | concurrency libraries | BEAM processes |
| Low-level Control | محدود | محدود | متوسط | متوسط | بسیار زیاد | بسیار زیاد | زیاد | بسیار زیاد | متوسط | زیاد | متوسط | محدود | محدود | متوسط | کمتر | کمتر | بسیار زیاد | evolving | متوسط | کمتر |
| Ecosystem | بسیار بزرگ | بسیار بزرگ | بسیار بزرگ | بسیار بزرگ | بسیار بزرگ | بسیار بزرگ | بزرگ | بزرگ | بزرگ | بزرگ | بزرگ | بزرگ | بسیار بزرگ | بزرگ | تخصصی/پایدار | رو به رشد | رو به رشد | نوپا | بزرگ | رو به رشد |
| Status | بالغ | بالغ | بالغ | بالغ | بالغ | بالغ | بالغ | بالغ | بالغ | بالغ | بالغ | بالغ | بالغ | بالغ | بالغ | بالغ | بالغ/رو به رشد | evolving | بالغ | بالغ/رو به رشد |

## 24.2 Sequence / Set / Map

| زبان | Sequence | Set | Map |
|---|---|---|---|
| Python | list | set | dict |
| JS/TS | Array | Set | Map/object |
| Java | List | Set | Map |
| C# | List | HashSet | Dictionary |
| C++ | vector/list/deque | set/unordered_set | map/unordered_map |
| C | arrays/custom | custom | custom |
| Go | slice | map pattern | map |
| Rust | Vec/array | HashSet/BTreeSet | HashMap/BTreeMap |
| Kotlin | List | Set | Map |
| Swift | Array | Set | Dictionary |
| Dart | List | Set | Map |
| Ruby | Array | Set | Hash |
| PHP | array | custom/SPL/library | array |
| Scala | List/Vector/Seq | Set | Map |
| Erlang | list | sets | map |
| Elixir | list | MapSet | Map |
| Zig | array/slice/dynamic array | library | hash map |
| Carbon | evolving | evolving | evolving |
| Haskell | List/Vector | Set | Map |
| Gleam | List | Set | Map |

## 24.3 Mutable vs Immutable

| زبان | وضعیت غالب |
|---|---|
| Python | mutable + immutable types |
| JS/TS | mutable objects/arrays |
| Java | mutable و immutable collections/objects |
| C# | mutable + immutable APIs |
| C++ | mutable by default |
| C | mutable by default |
| Go | mutable values |
| Rust | mutation explicit via `mut` |
| Kotlin | `val`/`var` و immutable collections |
| Swift | value semantics، `let`/`var` |
| Dart | mutable collections؛ `final` binding |
| Ruby | mutable objects |
| PHP | mutable arrays/objects |
| Scala | تأکید قوی بر immutable collections |
| Erlang | immutable |
| Elixir | immutable |
| Zig | mutable مگر محدود شود |
| Carbon | evolving |
| Haskell | immutable by default |
| Gleam | immutable |

## 24.4 Error Handling و Result

| زبان | الگوی رایج |
|---|---|
| Python | exceptions |
| JS/TS | exceptions / Promise rejection |
| Java | exceptions |
| C# | exceptions |
| C++ | exceptions / expected-like types |
| C | return codes / errno |
| Go | `(value, error)` |
| Rust | `Result<T,E>` |
| Kotlin | exceptions / `Result` |
| Swift | `throws`, `Result` |
| Dart | exceptions |
| Ruby | exceptions |
| PHP | exceptions |
| Scala | `Either`, `Try`, exceptions |
| Erlang | `{ok,V}` / `{error,R}` / supervision |
| Elixir | `{:ok,V}` / `{:error,R}` |
| Zig | error unions `!T` |
| Carbon | evolving |
| Haskell | `Either`, `Maybe`, exceptions |
| Gleam | `Result`, `Option` |

## 24.5 Memory Model

| زبان | مدل |
|---|---|
| Python | مدیریت خودکار + GC/reference-counting implementation details |
| JS/TS | GC |
| Java | GC |
| C# | GC |
| C++ | RAII/manual/smart pointers |
| C | manual |
| Go | GC |
| Rust | ownership/borrowing |
| Kotlin | JVM GC |
| Swift | ARC |
| Dart | GC |
| Ruby | GC |
| PHP | GC/reference counting mechanisms |
| Scala | JVM GC |
| Erlang | BEAM + per-process GC |
| Elixir | BEAM + per-process GC |
| Zig | explicit allocator؛ بدون GC عمومی |
| Carbon | evolving |
| Haskell | GC |
| Gleam | BEAM GC |

## 24.6 Functional Programming

| زبان | سطح |
|---|---|
| Python | متوسط |
| JS/TS | زیاد |
| Java | زیاد |
| C# | زیاد |
| C++ | زیاد |
| C | کم |
| Go | متوسط |
| Rust | زیاد |
| Kotlin | زیاد |
| Swift | زیاد |
| Dart | متوسط |
| Ruby | متوسط |
| PHP | متوسط |
| Scala | بسیار زیاد |
| Erlang | بسیار زیاد |
| Elixir | بسیار زیاد |
| Zig | متوسط |
| Carbon | evolving |
| Haskell | بسیار زیاد |
| Gleam | بسیار زیاد |

## 24.7 Concurrency Model

| زبان | مدل مهم |
|---|---|
| Python | threads, async, multiprocessing |
| JS/TS | event loop, async/await, workers |
| Java | threads, executors, futures, virtual threads |
| C# | Task, async/await, threads |
| C++ | threads, atomics, coroutines |
| C | OS threads/processes |
| Go | goroutines, channels |
| Rust | async runtimes, threads, channels |
| Kotlin | coroutines |
| Swift | structured concurrency, async/await, actors |
| Dart | isolates, async/await |
| Ruby | threads/processes/fibers |
| PHP | request/process model; extensions/frameworks |
| Scala | Futures, actors/libraries |
| Erlang | BEAM processes + message passing |
| Elixir | BEAM processes + message passing + supervision |
| Zig | threads/low-level concurrency |
| Carbon | evolving |
| Haskell | lightweight threads/STM/concurrency libraries |
| Gleam | BEAM processes/message passing |

## 24.8 Systems Programming

| زبان | تناسب |
|---|---|
| Python | محدود تا متوسط |
| JS/TS | محدود |
| Java | متوسط |
| C# | متوسط |
| C++ | عالی |
| C | عالی |
| Go | عالی |
| Rust | عالی |
| Kotlin | متوسط |
| Swift | زیاد |
| Dart | محدود |
| Ruby | محدود |
| PHP | محدود |
| Scala | متوسط |
| Erlang | محدود |
| Elixir | محدود |
| Zig | بسیار عالی |
| Carbon | هدف پروژه؛ evolving |
| Haskell | متوسط |
| Gleam | محدود |

---

## 25. جمع‌بندی

ساختار داده را باید همراه با سه مفهوم مطالعه کرد:

```text
Data Type
    ↓
Data Structure
    ↓
Algorithm
    ↓
Complexity
```

و انتخاب ساختار داده باید بر اساس موارد زیر انجام شود:

1. نوع عملیات غالب
2. تعداد داده
3. الگوی دسترسی
4. نیاز به ترتیب
5. نیاز به uniqueness
6. نیاز به key/value
7. memory constraints
8. cache locality
9. concurrency
10. persistence
11. serialization
12. scalability

### نقشه یادگیری پیشنهادی

```text
Array
 ↓
Dynamic Array
 ↓
Linked List
 ↓
Stack / Queue / Deque
 ↓
Hash Table / Map / Set
 ↓
Tree / BST
 ↓
AVL / Red-Black
 ↓
Heap / Priority Queue
 ↓
Graph
 ↓
Trie
 ↓
B-Tree / B+Tree
 ↓
Skip List
 ↓
Union-Find
 ↓
Segment/Fenwick Tree
 ↓
Persistent Structures
 ↓
Probabilistic Structures
 ↓
Database / Distributed / AI Data Structures
```

### اصل طلایی

هیچ ساختار داده‌ای «بهترین» نیست.

بهترین انتخاب تابعی از:

```text
Workload
+
Memory
+
Access Pattern
+
Mutation Pattern
+
Concurrency
+
Latency
+
Scale
```

است.
