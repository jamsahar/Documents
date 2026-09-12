# Data Types & Data Structures --- سه درس جامع

## فهرست عناوین

1.  [درس اول --- انواع Data Type و Data
    Structure](#درس-اول--انواع-data-type-و-data-structure)
    1.  [دسته‌بندی اصلی Data Typeها](#دسته‌بندی-اصلی-data-typeها)
    2.  [انواع عددی](#انواع-عددی)
    3.  [Boolean و Character و String](#boolean-و-character-و-string)
    4.  [Collectionها](#collectionها)
    5.  [Array، List و Vector](#array-list-و-vector)
    6.  [Tuple](#tuple)
    7.  [Set](#set)
    8.  [Map / Dictionary](#map--dictionary)
    9.  [Object، Class، Struct و Record](#object-class-struct-و-record)
    10. [Enum](#enum)
    11. [Binary Data](#binary-data)
    12. [Optional، Union و Variant](#optional-union-و-variant)
    13. [Function، Iterator و Generator](#function-iterator-و-generator)
    14. [Stack، Queue و Deque](#stack-queue-و-deque)
    15. [Linked List، Tree، Heap، Graph و
        Trie](#linked-list-tree-heap-graph-و-trie)
    16. [Pointer و Reference](#pointer-و-reference)
    17. [Date/Time، UUID و Big Integer](#datetime-uuid-و-big-integer)
    18. [Data Type در زبان‌های متداول](#data-type-در-زبانهای-متداول)
    19. [Data Type در برابر Data
        Structure](#data-type-در-برابر-data-structure)
    20. [داده‌های تخصصی AI/LLM](#دادههای-تخصصی-aillm)
2.  [درس دوم --- مقایسه عمیق و مدل‌سازی
    داده](#درس-دوم--مقایسه-عمیق-و-مدل‌سازی-داده)
    1.  [Master List](#master-list)
    2.  [مقایسه Array/List/Tuple](#مقایسه-arraylisttuple)
    3.  [Mutable و Immutable](#mutable-و-immutable)
    4.  [Ordered/Unordered و
        Homogeneous/Heterogeneous](#orderedunordered-و-homogeneousheterogeneous)
    5.  [Generics و Type Alias](#generics-و-type-alias)
    6.  [Optional، Result و Async Types](#optional-result-و-async-types)
    7.  [Binary Types و Serialization](#binary-types-و-serialization)
    8.  [Tensor، Embedding و AI Data](#tensor-embedding-و-ai-data)
    9.  [Message، Tool Call و Agent
        State](#message-tool-call-و-agent-state)
    10. [مدل داده RAG](#مدل-داده-rag)
    11. [نقشه یادگیری](#نقشه-یادگیری)
3.  [درس سوم --- مباحث حرفه‌ای و تکمیلی](#درس-سوم--مباحث-حرفهای-و-تکمیلی)
    1.  [Type System](#type-system)
    2.  [Memory Model](#memory-model)
    3.  [Mutability، Copy و Sharing](#mutability-copy-و-sharing)
    4.  [Equality، Identity و Hashing](#equality-identity-و-hashing)
    5.  [Type Conversion](#type-conversion)
    6.  [Generics و Advanced Types](#generics-و-advanced-types)
    7.  [Complexity و انتخاب
        Collection](#complexity-و-انتخاب-collection)
    8.  [Serialization و Data
        Interchange](#serialization-و-data-interchange)
    9.  [Database Data Types](#database-data-types)
    10. [Concurrency و Data Safety](#concurrency-و-data-safety)
    11. [Distributed Systems Data](#distributed-systems-data)
    12. [AI/LLM Data Models](#aillm-data-models)
    13. [RAG Data Models](#rag-data-models)
    14. [زنجیره کامل دانش](#زنجیره-کامل-دانش)

------------------------------------------------------------------------

# درس اول --- انواع Data Type و Data Structure

## دسته‌بندی اصلی Data Typeها

Data Type مشخص می‌کند یک مقدار چه نوع داده‌ای است، چه عملیاتی روی آن مجاز
است و معمولاً چگونه در حافظه نمایش داده می‌شود.

گروه‌های مهم:

-   Numeric
-   Boolean
-   Character
-   String
-   Array
-   List
-   Vector
-   Tuple
-   Set
-   Map / Dictionary
-   Object / Class
-   Struct
-   Record
-   Enum
-   Binary / Bytes
-   Optional / Nullable
-   Union / Variant
-   Function / Lambda
-   Iterator / Generator
-   Date / Time
-   UUID
-   Pointer / Reference
-   Void
-   Any / Dynamic
-   Complex Number
-   Big Integer

## انواع عددی

### جدول مقایسه انواع عددی

  ------------------------------------------------------------------------------------------------------------------------
  مفهوم    Python              JavaScript/TypeScript   Java           C#          C++              Go           Rust
  -------- ------------------- ----------------------- -------------- ----------- ---------------- ------------ ----------
  صحیح     `int`               `number`                `int`          `int`       `int`            `int`        `i32`
  معمولی                                                                                                        

  صحیح     `int`               `bigint`                `long`         `long`      `long long`      `int64`      `i64`
  بزرگ                                                                                                          

  اعشاری   `float`             `number`                `float`        `float`     `float`          `float32`    `f32`

  اعشاری   `float`             `number`                `double`       `double`    `double`         `float64`    `f64`
  دقیق‌تر                                                                                                        

  اعشاری   `decimal.Decimal`   کتابخانه/BigInt الگو    `BigDecimal`   `decimal`   کتابخانه         `math/big`   کتابخانه
  مالی                                                                                             یا کتابخانه  

  مختلط    `complex`           کتابخانه                کتابخانه       کتابخانه    `std::complex`   کتابخانه     کتابخانه
  ------------------------------------------------------------------------------------------------------------------------

> نکته: اندازه دقیق Integer و رفتار Overflow در همه زبان‌ها یکسان نیست؛
> به نوع انتخاب‌شده و پیاده‌سازی وابسته است.

### Integer

اعداد صحیح مانند `-10`, `0`, `42`.

### Float / Double

اعداد اعشاری با دقت شناور.

### Decimal

برای محاسبات دقیق اعشاری، به‌خصوص مالی.

### Big Integer

برای اعداد صحیح بسیار بزرگ.

### Complex

اعداد مختلط مانند `3 + 4j`.

نکته: نمایش اعشاری دودویی می‌تواند باعث خطاهای ظاهری شود؛ مثلاً در
JavaScript:

``` javascript
const a = 0.2 + 0.4;
const b = 0.6;
console.log(a, b, a === b);
```

برای محاسبات حساس، Decimal یا روش‌های عددی مناسب استفاده کنید.

## Boolean و Character و String

### جدول مقایسه Boolean، Character و String

  --------------------------------------------------------------------------------------------------------------------------
  مفهوم       Python       JavaScript/TypeScript   Java              C#                C++             Go         Rust
  ----------- ------------ ----------------------- ----------------- ----------------- --------------- ---------- ----------
  Boolean     `bool`       `boolean`               `boolean`         `bool`            `bool`          `bool`     `bool`

  Character   `str`        `string` با یک کاراکتر  `char`            `char`            `char` /        `rune`     `char`
              تک‌کاراکتری                                                               `char32_t`                 

  String      `str`        `string`                `String`          `string`          `std::string`   `string`   `String` /
                                                                                                                  `&str`

  Mutable     خیر          معمولاً immutable        `StringBuilder`   `StringBuilder`   `std::string`   قابل تغییر `String`
  String                   primitive                                                                   از طریق    
                                                                                                       `[]byte`   

  Unicode     بله          بله                     بله               بله               وابسته به       UTF-8 برای UTF-8 برای
                                                                                       نوع/encoding    `string`   `String`
  --------------------------------------------------------------------------------------------------------------------------

### تفاوت مهم Encoding و Character

`Character`، `Code Point` و `Byte` یک مفهوم نیستند. برای متن بین‌المللی
باید Unicode و Encodingهایی مانند UTF-8 را نیز بشناسید.

-   `Boolean`: معمولاً `true/false`
-   `Character`: یک کاراکتر
-   `String`: دنباله‌ای از کاراکترها

مثال Python:

``` python
active = True
letter = "A"
name = "Alice"
```

در برخی زبان‌ها Character نوع مستقل دارد؛ در برخی دیگر String تک‌کاراکتری
است.

## Collectionها

### جدول مقایسه Collectionهای رایج

  ------------------------------------------------------------------------------
  ساختار           ترتیب       Duplicate   دسترسی با   Lookup      کاربرد اصلی
                                           Index                   
  ---------------- ----------- ----------- ----------- ----------- -------------
  Array            دارد        دارد        سریع        معمولاً O(n) داده‌های
                                                                   indexed

  List/Dynamic     دارد        دارد        سریع        معمولاً O(n) مجموعه عمومی
  Array                                                            

  Tuple            دارد        دارد        معمولاً دارد معمولاً O(n) چند مقدار
                                                                   ثابت

  Set              معمولاً بدون ندارد       ندارد       Hash Set:   عضویت و حذف
                   تضمین ترتیب                         معمولاً O(1) تکرار

  Map/Dictionary   کلیدمحور    Key تکراری  با Key      Hash Map:   Lookup
                               ندارد                   معمولاً O(1) 

  Stack            ترتیب LIFO  دارد        هدف اصلی    \-          Undo/Call
                                           نیست                    stack

  Queue            ترتیب FIFO  دارد        هدف اصلی    \-          Job/Message
                                           نیست                    processing

  Deque            دوطرفه      دارد        وابسته به   \-          صف دوطرفه
                                           پیاده‌سازی               
  ------------------------------------------------------------------------------

> پیچیدگی‌ها معمولی/میانگین هستند و به پیاده‌سازی و شرایط اجرا وابسته‌اند.

Collection ساختاری برای نگهداری چند مقدار است.

انواع متداول:

-   Array
-   List
-   Vector
-   Set
-   Map
-   Tuple
-   Stack
-   Queue
-   Deque

انتخاب Collection باید بر اساس نیازهای دسترسی، جست‌وجو، درج، حذف، ترتیب و
حافظه انجام شود.

## Array، List و Vector

### جدول مقایسه Array، List و Vector در زبان‌های متداول

  ---------------------------------------------------------------------------
  زبان              Array ثابت/زبان‌اصلی Dynamic Array /    Vector نام متداول
                                        List               
  ----------------- ------------------- ------------------ ------------------
  Python            `array`/لیست؛ Array `list`             `list` یا
                    کلاسیک مستقل مانند                     کتابخانه‌های عددی
                    C ندارد                                

  JavaScript        `Array`             `Array`            `TypedArray` در
                                                           کاربردهای خاص

  TypeScript        `T[]` / `Array<T>`  `Array<T>`         اصطلاح عمومی

  Java              `T[]`               `ArrayList<T>`     `Vector<T>` قدیمی

  C#                `T[]`               `List<T>`          `Vector<T>` در
                                                           کتابخانه‌های عددی

  C++               `std::array<T,N>`   `std::vector<T>`   `std::vector<T>`

  Go                `[N]T`              `[]T`              `slice`

  Rust              `[T; N]`            `Vec<T>`           `Vec<T>`
  ---------------------------------------------------------------------------

### انتخاب سریع

-   اندازه ثابت و Layout مشخص → Array
-   رشد پویا و دسترسی با Index → Dynamic Array/List/Vector
-   داده‌های عددی سنگین → ساختارهای تخصصی Vector/Tensor

### Array

معمولاً مجموعه‌ای با اندیس و اندازه مشخص یا ساختار متراکم.

``` text
[10, 20, 30, 40]
```

### List

در بسیاری از زبان‌ها مجموعه‌ای انعطاف‌پذیر و معمولاً قابل تغییر.

### Vector

در بسیاری از زبان‌ها آرایه پویا است؛ در AI نیز Vector معنای دیگری به‌عنوان
بردار عددی دارد.

بنابراین «Vector» می‌تواند هم Data Structure و هم AI Data Representation
باشد.

## Tuple

### جدول Tuple در زبان‌های متداول

  --------------------------------------------------------------------------------
  زبان              Tuple بومی        تغییرپذیری معمول  مثال
  ----------------- ----------------- ----------------- --------------------------
  Python            بله               Immutable         `(10, 20)`

  TypeScript        بله               از نظر نوعی       `[number, string]`
                                      Tuple؛ mutable    
                                      مگر readonly      

  Java              به‌صورت عمومی نوع  وابسته به         `record`/کلاس
                    Tuple built-in    پیاده‌سازی         
                    ندارد                               

  C#                بله               `ValueTuple` قابل `(10, "AI")`
                                      تغییر             

  C++               بله               قابل تغییر        `std::tuple<int,string>`

  Go                خیر به‌صورت Tuple  \-                `struct`
                    عمومی                               

  Rust              بله               پیش‌فرض قابل تغییر `(10, "AI")`
                                      در صورت `mut`     
  --------------------------------------------------------------------------------

Tuple مجموعه‌ای مرتب است که در بسیاری از زبان‌ها برای داده‌های ثابت یا
چندتایی استفاده می‌شود.

Python:

``` python
point = (10, 20)
person = ("Ali", 30, True)
```

مزایا:

-   ساختار مرتب
-   مناسب برای چند مقدار مرتبط
-   در Python تغییرناپذیر

## Set

### جدول Set در زبان‌های متداول

  ----------------------------------------------------------------------------
  زبان              Set رایج               Ordered Set       Hash-based
  ----------------- ---------------------- ----------------- -----------------
  Python            `set`                  `dict` ترتیب      بله
                                           insertion دارد؛   
                                           set برای ترتیب به 
                                           آن تکیه نمی‌کند    

  JavaScript        `Set`                  insertion order   پیاده‌سازی داخلی
                                           حفظ می‌شود         

  Java              `HashSet`              `LinkedHashSet` / بله
                                           `TreeSet`         

  C#                `HashSet<T>`           نوع تخصصی برای    بله
                                           sorted/ordered    
                                           بسته به نیاز      

  C++               `std::unordered_set`   `std::set`        هر دو

  Go                Set built-in ندارد؛    با map خام تضمین  map
                    `map[T]struct{}` الگو  مرتب‌سازی وجود     
                    است                    ندارد             

  Rust              `HashSet`              `BTreeSet`        هر دو
  ----------------------------------------------------------------------------

Set مجموعه‌ای از مقادیر بدون تکرار است.

``` python
tags = {"ai", "rag", "python"}
```

کاربردها:

-   حذف Duplicate
-   عضویت
-   Union
-   Intersection
-   Difference

## Map / Dictionary

### جدول Map / Dictionary

  --------------------------------------------------------------------------------------
  زبان              Hash Map            Ordered/Sorted Map        مثال
  ----------------- ------------------- ------------------------- ----------------------
  Python            `dict`              ترتیب insertion حفظ می‌شود `{"id": 1}`

  JavaScript        `Map` / Object      `Map` insertion order     `new Map()`
                                        دارد                      

  TypeScript        `Map<K,V>`          معمولاً با ساختار/کتابخانه `Map<string,number>`
                                        دیگر                      

  Java              `HashMap`           `LinkedHashMap` /         `Map<K,V>`
                                        `TreeMap`                 

  C#                `Dictionary<K,V>`   `SortedDictionary<K,V>`   `Dictionary`

  C++               `unordered_map`     `map`                     `std::map`

  Go                `map[K]V`           باید جداگانه مرتب‌سازی شود `map[string]int`

  Rust              `HashMap<K,V>`      `BTreeMap<K,V>`           `HashMap`
  --------------------------------------------------------------------------------------

Map رابطه Key → Value است.

Python:

``` python
user = {
    "id": 1001,
    "name": "Ali",
    "active": True
}
```

JavaScript:

``` javascript
const user = {
  id: 1001,
  name: "Ali",
  active: true
};
```

کاربردها:

-   Lookup
-   Configuration
-   Metadata
-   JSON-like data
-   Indexing

## Object، Class، Struct و Record

### مقایسه Object/ Class / Struct / Record

  --------------------------------------------------------------------------------------------
  مفهوم      Python        Java           C#         C++        Go                Rust
  ---------- ------------- -------------- ---------- ---------- ----------------- ------------
  Class      `class`       `class`        `class`    `class`    \-                `struct` با
                                                                                  `impl`

  Struct     \-            معمولاً         `struct`   `struct`   `struct`          `struct`
                           class/record                                           

  Record     `dataclass`   `record`       `record`   \-         `struct` + روش‌های `struct`
             الگو                                               قراردادی          

  Object     همه           instance       instance   instance   value/reference   value/type
             instanceها                                         types             instances
  --------------------------------------------------------------------------------------------

### Object

نمونه‌ای از یک نوع/کلاس که داده و رفتار را می‌تواند در خود داشته باشد.

### Class

تعریف ساختار و رفتار Object.

### Struct

معمولاً نوع داده‌ای سبک برای نگهداری چند فیلد.

### Record

برای داده‌های ساخت‌یافته، مخصوصاً داده‌هایی که هویت آن‌ها بیشتر بر اساس
مقادیر فیلدهاست.

## Enum

### جدول Enum در زبان‌های متداول

  زبان         Enum                      قابلیت‌های مهم
  ------------ ------------------------- --------------------------------------------------
  Python       `enum.Enum`               نام‌دار، قابل توسعه
  TypeScript   `enum` یا Union Literal   Union اغلب سبک‌تر است
  Java         `enum`                    می‌تواند field و method داشته باشد
  C#           `enum`                    معمولاً بر پایه نوع صحیح
  C++          `enum` / `enum class`     `enum class` type-safeتر است
  Go           Enum مستقل ندارد          معمولاً `const` + type
  Rust         `enum`                    بسیار قدرتمند؛ مناسب Sum Type و Pattern Matching

Enum مجموعه‌ای از مقادیر نام‌دار محدود است.

``` text
Status = NEW | RUNNING | DONE | FAILED
```

کاربرد:

-   State
-   Status
-   Mode
-   Category
-   Permissions

## Binary Data

برای فایل و داده خام:

-   bytes
-   byte array
-   buffer
-   blob
-   binary stream

مثال Python:

``` python
data = b"hello"
```

## Optional، Union و Variant

### جدول Advanced Value Types

  ---------------------------------------------------------------------------------------------------------------------------------
  مفهوم         Python            TypeScript              Java              C#                C++                   Rust
  ------------- ----------------- ----------------------- ----------------- ----------------- --------------------- ---------------
  Optional      `Optional[T]` /   `T \| undefined/null`   `Optional<T>`     `T?`              `std::optional<T>`    `Option<T>`
                `T \| None`                                                                                         

  Union         `T \| U`          `T \| U`                الگوی             `T` محدودتر؛      `std::variant<T,U>`   `enum`
                                                          class/interface   الگوهای دیگر                            

  Result        `Result`          Result pattern          الگو/کتابخانه     الگو/کتابخانه     `std::expected`       `Result<T,E>`
                کتابخانه‌ای/الگو                                                                                     

  Nullability   `None`            `null`/`undefined`      reference می‌تواند Nullable          pointer/null          `Option`
                                                          null باشد         Reference/Value                         به‌عنوان الگوی
                                                                            Types                                   اصلی
  ---------------------------------------------------------------------------------------------------------------------------------

### Optional / Nullable

یک مقدار ممکن است وجود داشته باشد یا نداشته باشد:

``` text
Optional[String]
```

### Union

یک مقدار می‌تواند یکی از چند نوع باشد:

``` text
String | Integer
```

### Variant

نوعی container برای چند شکل داده که در هر لحظه یکی از حالت‌ها را نگه
می‌دارد.

## Function، Iterator و Generator

### جدول Function/Iterator/Generator

  --------------------------------------------------------------------------------------------------------------------------------------------
  مفهوم       Python     JS/TS         Java                C#                            C++               Go               Rust
  ----------- ---------- ------------- ------------------- ----------------------------- ----------------- ---------------- ------------------
  Function    بله        بله           Lambda/Functional   Delegate/Lambda               Lambda/Function   Function Value   Closure/Function
  Value                                Interface                                         Object                             Pointer

  Iterator    `iter()`   Iterator      `Iterator<T>`       `IEnumerable<T>`/Enumerator   Iterator pattern  range/iterator   `Iterator` trait
                         Protocol                                                                          patterns         

  Generator   `yield`    `function*`   Stream/Iterator؛    `yield`                       Coroutine/C++20   `yield` در زبان  `Iterator`/async
                                       generator عمومی                                                     ندارد؛ iterator  streams
                                       کلاسیک ندارد                                                        pattern          
  --------------------------------------------------------------------------------------------------------------------------------------------

Function نیز در زبان‌های مدرن می‌تواند یک مقدار قابل نگهداری و ارسال باشد.

``` python
def add(a, b):
    return a + b
```

### Iterator

داده‌ها را مرحله‌به‌مرحله ارائه می‌کند.

### Generator

برای تولید lazy داده‌ها، بدون ساخت کل مجموعه در حافظه.

``` python
def numbers():
    for i in range(10):
        yield i
```

## Stack، Queue و Deque

### جدول پیاده‌سازی Stack/Queue/Deque

  زبان         Stack                  Queue                         Deque
  ------------ ---------------------- ----------------------------- --------------------------
  Python       `list`, `deque`        `collections.deque`           `collections.deque`
  JavaScript   `Array`                `Array`/کتابخانه              کتابخانه
  Java         `Deque`/`ArrayDeque`   `Queue`                       `ArrayDeque`
  C#           `Stack<T>`             `Queue<T>`                    `LinkedList<T>`/کتابخانه
  C++          `std::stack`           `std::queue`                  `std::deque`
  Go           slice                  slice/channel بسته به مسئله   slice/پیاده‌سازی
  Rust         `Vec`/`VecDeque`       `VecDeque`                    `VecDeque`

### Stack

LIFO:

``` text
Last In → First Out
```

عملیات اصلی:

-   push
-   pop
-   peek

### Queue

FIFO:

``` text
First In → First Out
```

عملیات:

-   enqueue
-   dequeue

### Deque

Double-ended queue؛ افزودن و حذف از هر دو سمت.

## Linked List، Tree، Heap، Graph و Trie

### جدول Data Structureهای پیشرفته

  -------------------------------------------------------------------------
  ساختار            شکل               عملیات/مزیت کلیدی کاربرد
  ----------------- ----------------- ----------------- -------------------
  Linked List       Node → Node       درج/حذف با        ساختارهای خاص
                                      Reference مناسب   

  Tree              سلسله‌مراتبی       جست‌وجوی ساختاری   فایل، Index

  BST               Tree مرتب         Search در حالت    جست‌وجو
                                      متعادل O(log n)   

  Heap              Tree خاص          Min/Max سریع      Priority Queue

  Graph             Node + Edge       مدل‌سازی رابطه     شبکه و Knowledge
                                                        Graph

  Trie              Prefix Tree       Prefix Search     Dictionary/Search

  Hash Table        Buckets + Hash    Lookup میانگین    Map/Set
                                      O(1)              
  -------------------------------------------------------------------------

### Linked List

هر Node به Node بعدی یا قبلی اشاره دارد.

### Tree

ساختار سلسله‌مراتبی.

نمونه‌ها:

-   Binary Tree
-   BST
-   AVL Tree
-   B-Tree

### Heap

برای دسترسی سریع به Minimum/Maximum و پیاده‌سازی Priority Queue.

### Graph

مجموعه‌ای از Node و Edge.

کاربرد:

-   شبکه‌ها
-   Dependency
-   Knowledge Graph
-   Routing

### Trie

ساختار درختی برای Prefix Search و داده‌های متنی.

## Pointer و Reference

### مقایسه Pointer و Reference

  ----------------------------------------------------------------------------
  زبان              Pointer           Reference          مدیریت حافظه
  ----------------- ----------------- ------------------ ---------------------
  Python            مستقیم در اختیار  Object Reference   GC/Reference
                    برنامه‌نویس نیست                      Counting + مدیریت
                                                         runtime

  JavaScript        pointer خام ندارد Reference          GC
                                      semantics          

  Java              pointer خام ندارد Object References  GC

  C#                Reference Types؛  `ref`/`in`/`out`   GC
                    pointer با                           
                    `unsafe`                             

  C++               Pointer و         هر دو              دستی/RAII
                    Reference                            

  Go                Pointer دارد      reference type     GC
                                      patterns           

  Rust              `*const/*mut`     `&T` / `&mut T`    Ownership/Borrowing
                    unsafe                               
  ----------------------------------------------------------------------------

### Pointer

آدرس حافظه را نگه می‌دارد و در زبان‌هایی مانند C/C++ اهمیت زیادی دارد.

### Reference

به یک Object یا مقدار دیگر ارجاع می‌دهد و معمولاً abstraction بالاتری از
Pointer دارد.

## Date/Time، UUID و Big Integer

### جدول انواع سیستمی

  ------------------------------------------------------------------------------------------------------------------------------------------
  مفهوم       Python       JavaScript/TS   Java           C#                 C++                       Go              Rust
  ----------- ------------ --------------- -------------- ------------------ ------------------------- --------------- ---------------------
  Date/Time   `datetime`   `Date`,         `java.time`    `DateTime`,        `<chrono>`                `time.Time`     `std::time`/crateها
                           Temporal در                    `DateTimeOffset`                                             
                           محیط‌های جدید                                                                                

  UUID        `uuid`       کتابخانه/Web    `UUID`         `Guid`             کتابخانه                  `google/uuid`   crateهای UUID
                           API                                                                         یا مشابه        

  Big Integer `int`        `BigInt`        `BigInteger`   `BigInteger`       `boost::multiprecision`   `math/big`      `num-bigint`
  ------------------------------------------------------------------------------------------------------------------------------------------

### Date/Time

برای:

-   تاریخ
-   زمان
-   Timestamp
-   Time Zone
-   Duration

### UUID

شناسه تقریباً یکتا برای Objectها، Sessionها، Requestها و Recordها.

### Big Integer

برای اعداد بزرگ‌تر از محدوده معمول Integer.

## Data Type در زبان‌های متداول

  ----------------------------------------------------------------------------------------------------------------------------------------------------
  مفهوم      Python              JavaScript/TS    Java           C#                   C++                        Go                 Rust
  ---------- ------------------- ---------------- -------------- -------------------- -------------------------- ------------------ ------------------
  Integer    int                 number/bigint    int/long       int/long             int/long                   int/int64          i32/i64

  Float      float               number           float/double   float/double         float/double               float32/64         f32/f64

  Boolean    bool                boolean          boolean        bool                 bool                       bool               bool

  String     str                 string           String         string               string                     string             String/&str

  Array      list/array          Array            T\[\]          T\[\]                T\[\]                      \[N\]T             \[T;N\]

  Dynamic    list                Array            ArrayList      List`<T>`{=html}     vector                     \[\]T              Vec`<T>`{=html}
  List                                                                                                                              

  Tuple      tuple               tuple in TS      record-like /  ValueTuple           tuple                      struct             tuple
                                                  custom                                                                            

  Set        set                 Set              Set            HashSet              set                        map\[T\]struct{}   HashSet

  Map        dict                Map/object       Map            Dictionary           map/unordered_map          map                HashMap

  Optional   None                null/undefined   Optional       nullable             optional                   pointer/value      Option
                                                                                                                 pattern            

  Result     exceptions/custom   Promise/result   custom         Result-like/custom   expected                   error              Result
                                 patterns                                                                                           

  Binary     bytes               Uint8Array       byte\[\]       byte\[\]             vector`<uint8_t>`{=html}   \[\]byte           Vec`<u8>`{=html}
  ----------------------------------------------------------------------------------------------------------------------------------------------------

## Data Type در برابر Data Structure

**Data Type** بیشتر مشخص می‌کند «چه نوع مقداری» داریم.

**Data Structure** مشخص می‌کند «چگونه چند داده را سازمان‌دهی و نگهداری
کنیم».

مثال:

``` text
string
    ↓
List[string]
    ↓
Document
    ↓
RAG Index
```

## داده‌های تخصصی AI/LLM

### جدول Data Typeهای AI/LLM

  نوع داده         شکل معمول                کاربرد
  ---------------- ------------------------ ----------------------------
  Token            Integer/ID               واحد پردازش متن
  Token ID         Integer                  ورودی/خروجی Tokenizer
  Tensor           N-D Array                مدل‌های عصبی
  Vector           1-D Numeric Array        Embedding و محاسبات برداری
  Embedding        Float Vector             نمایش معنایی
  Logits           Float Vector/Tensor      امتیاز خام خروجی مدل
  Probability      Float Distribution       احتمال Tokenها
  Attention Mask   Integer/Boolean Tensor   کنترل Attention
  Message          Record/Object            پیام LLM
  Tool Call        Structured Object        فراخوانی ابزار
  Tool Result      Structured Object        پاسخ ابزار
  Agent State      Object/Record            وضعیت اجرای Agent
  Memory Item      Record                   داده حافظه Agent

در سیستم‌های AI با انواع داده جدیدی مواجه می‌شویم:

-   Token
-   Token ID
-   Tensor
-   Vector
-   Embedding
-   Logits
-   Probability Distribution
-   Attention Mask
-   Message
-   Tool Call
-   Tool Result
-   Document
-   Chunk
-   Metadata
-   Knowledge Graph Node/Edge
-   Agent State
-   Memory Item

------------------------------------------------------------------------

# درس دوم --- مقایسه عمیق و مدل‌سازی داده

## Master List

فهرست عملی انواع مهم:

``` text
Primitive
├── Integer
├── Float
├── Decimal
├── Boolean
├── Character
└── String

Collections
├── Array
├── List
├── Vector
├── Tuple
├── Set
├── Map
├── Stack
├── Queue
└── Deque

Structures
├── Linked List
├── Tree
├── Heap
├── Graph
├── Trie
└── Hash Table

Advanced Types
├── Enum
├── Optional
├── Nullable
├── Union
├── Variant
├── Result
├── Generic
└── Function Type

System Types
├── Pointer
├── Reference
├── Iterator
├── Generator
├── Future/Promise/Task
└── Coroutine

AI Types
├── Token
├── Tensor
├── Vector
├── Embedding
├── Logits
├── Attention Mask
├── Message
├── Tool Call
├── Agent State
└── Memory
```

## مقایسه Array/List/Tuple

### مقایسه تکمیلی در زبان‌های متداول

  -------------------------------------------------------------------------------------------------------------
  ویژگی     Python             JS/TS        Java            C#             C++            Go        Rust
  --------- ------------------ ------------ --------------- -------------- -------------- --------- -----------
  Array     محدود/کتابخانه‌ای   TypedArray   `T[]`           `T[]`          `std::array`   `[N]T`    `[T;N]`
  ثابت                                                                                              

  Dynamic   `list`             `Array`      `ArrayList`     `List<T>`      `vector`       `slice`   `Vec<T>`
  Array                                                                                             

  Tuple     `tuple`            TS Tuple     `record`/کلاس   `ValueTuple`   `tuple`        struct    tuple

  Index     بله                بله          بله             بله            بله            slice بله Vec/array
  Access                                                                                            بله
  -------------------------------------------------------------------------------------------------------------

  ویژگی        Array                       List           Tuple
  ------------ --------------------------- -------------- -----------------
  ترتیب        معمولاً دارد                 دارد           دارد
  تغییرپذیری   وابسته به زبان              معمولاً دارد    اغلب ندارد
  اندازه       ثابت/محدود در برخی زبان‌ها   پویا           ثابت
  کاربرد       داده‌های indexed             مجموعه عمومی   چند مقدار مرتبط
  مثال         `int[10]`                   `[1,2,3]`      `(x,y)`

## Mutable و Immutable

### مقایسه Mutability

  -----------------------------------------------------------------------
  زبان              نمونه Immutable   نمونه Mutable     نکته
  ----------------- ----------------- ----------------- -----------------
  Python            `tuple`, `str`    `list`, `dict`,   خود Object یا نوع
                                      `set`             تعیین‌کننده است

  JavaScript        `string`,         `Array`, Object,  `const` به‌معنای
                    primitiveها       Map, Set          immutable بودن
                                                        Object نیست

  Java              `String`, record  `ArrayList`,      Immutability با
                    معمولاً            mutable class     طراحی انجام می‌شود
                    value-oriented                      

  C#                `string`,         `List<T>`, class  `readonly`
                    recordهای مناسب                     محدودیت‌هایی دارد

  C++               `const` objects   معمولاً انواع عادی constness و
                                                        ownership جدا
                                                        هستند

  Go                String immutable  slice/map قابل    value/reference
                                      تغییر             semantics مهم است

  Rust              immutable به‌صورت  با `mut`          Borrow Checker
                    پیش‌فرض                              کنترل می‌کند
  -----------------------------------------------------------------------

### Mutable

بعد از ساخت قابل تغییر است.

``` python
items = [1, 2, 3]
items.append(4)
```

### Immutable

بعد از ساخت قابل تغییر نیست.

``` python
point = (10, 20)
```

مزایای Immutability:

-   Thread Safety بهتر
-   Predictability
-   کاهش Side Effect
-   مناسب برای Functional Programming
-   مناسب برای Cache و Sharing

## Ordered/Unordered و Homogeneous/Heterogeneous

### Ordered

ترتیب عناصر اهمیت دارد.

### Unordered

ترتیب عنصرها تضمین اصلی ساختار نیست.

### Homogeneous

همه عناصر یک نوع دارند.

### Heterogeneous

عناصر می‌توانند انواع متفاوت داشته باشند.

Python:

``` python
data = [10, "AI", True]
```

## Generics و Type Alias

### مقایسه Generics

  زبان         Generic Syntax       نمونه
  ------------ -------------------- -------------------
  Python       Type Hints/Generic   `list[T]`
  TypeScript   `<T>`                `Array<T>`
  Java         `<T>`                `List<T>`
  C#           `<T>`                `List<T>`
  C++          Template             `vector<T>`
  Go           `[T any]`            `func Map[T any]`
  Rust         `<T>`                `Vec<T>`

Generic امکان نوشتن ساختارهای type-safe و reusable را فراهم می‌کند.

مثال مفهومی:

``` text
List[T]
Map[K, V]
Result[T, E]
```

Type Alias برای نام‌گذاری نوع‌های پیچیده:

``` text
UserId = UUID
Embedding = Vector[Float]
```

## Optional، Result و Async Types

### جدول Optional/Result/Async

  -----------------------------------------------------------------------------------------------------------------------------------------------------
  مفهوم       Python             JS/TS              Java                     C#                 C++                Go                  Rust
  ----------- ------------------ ------------------ ------------------------ ------------------ ------------------ ------------------- ----------------
  Optional    `Optional[T]`      `T \| undefined`   `Optional<T>`            `T?`               `optional<T>`      pointer/value       `Option<T>`
                                                                                                                   pattern             

  Error       exception/Result   `Promise` + errors exception/Result pattern exception/Result   `expected<T,E>`    `(value, error)`    `Result<T,E>`
  Result      pattern                                                        pattern                                                   

  Async       coroutine          `Promise<T>`       `CompletableFuture<T>`   `Task<T>`          coroutine/future   goroutine/channel   `Future`/async
  Result                                                                                                                               

  Null-safe   `None`             optional chaining  `Optional`               `?.` / nullable    optional           explicit checks     `Option`
  idiom                                                                                                                                
  -----------------------------------------------------------------------------------------------------------------------------------------------------

### Optional

برای «مقدار ممکن است وجود نداشته باشد».

### Result

برای مدل‌سازی موفقیت/خطا به‌صورت explicit:

``` text
Result[Success, Error]
```

### Future / Promise / Task

نماینده نتیجه‌ای که در آینده آماده می‌شود.

کاربرد:

-   Async I/O
-   API Calls
-   Agent execution
-   Parallel processing

### Coroutine

واحد اجرای قابل suspend/resume، بسیار مهم در برنامه‌نویسی asynchronous.

## Binary Types و Serialization

### مقایسه Binary Representation

  ------------------------------------------------------------------------------------------
  زبان              Byte Type              Buffer/Array        Serialization رایج
  ----------------- ---------------------- ------------------- -----------------------------
  Python            `bytes`, `bytearray`   `memoryview`        JSON/pickle/کتابخانه‌ها

  JS/TS             `Uint8Array`           `ArrayBuffer`       JSON/structured
                                                               clone/کتابخانه

  Java              `byte[]`               `ByteBuffer`        JSON/Protobuf/Serialization
                                                               frameworks

  C#                `byte[]`               `Memory<byte>`      JSON/Protobuf

  C++               `uint8_t`/containers   `vector<uint8_t>`   JSON/Protobuf/کتابخانه

  Go                `[]byte`               slice               JSON/Protobuf

  Rust              `Vec<u8>`              slices              Serde/Protobuf و مشابه
  ------------------------------------------------------------------------------------------

داده برای انتقال یا ذخیره‌سازی معمولاً Serialize می‌شود.

فرمت‌ها:

-   JSON
-   XML
-   YAML
-   CSV
-   MessagePack
-   Protocol Buffers
-   Avro

مثال:

``` text
Object
  ↓ serialize
JSON / Protobuf
  ↓ transport
Network
  ↓ deserialize
Object
```

## Tensor، Embedding و AI Data

### Tensor

آرایه چندبعدی از داده‌ها.

``` text
Scalar  = 0 dimension
Vector  = 1 dimension
Matrix  = 2 dimensions
Tensor  = N dimensions
```

Tensor معمولاً همراه Shape و Data Type تعریف می‌شود:

``` text
Tensor<float32>
shape = [batch, sequence, hidden]
```

### Embedding

بردار عددی که معنای یک Entity را در فضای برداری نمایش می‌دهد.

``` text
text → embedding model → [0.12, -0.03, ...]
```

### Logits

امتیازهای خام مدل قبل از تبدیل به Probability.

### Attention Mask

مشخص می‌کند مدل به کدام موقعیت‌ها توجه کند.

## Message، Tool Call و Agent State

### مقایسه مدل Message در اکوسیستم‌ها

  -----------------------------------------------------------------------
  مفهوم                   شکل داده                فیلدهای معمول
  ----------------------- ----------------------- -----------------------
  LLM Message             Record/Object           role, content, metadata

  Tool Call               Record/Object           tool_name, arguments,
                                                  call_id

  Tool Result             Record/Object           call_id, result, status

  Agent State             Record/Object           session, messages,
                                                  goal, context, memory

  Event                   Record/Object           id, type, timestamp,
                                                  payload

  Command                 Record/Object           name, arguments,
                                                  correlation_id
  -----------------------------------------------------------------------

### Message

در سیستم‌های LLM معمولاً شامل:

``` text
role
content
metadata
```

Roleها می‌توانند شامل:

-   system
-   user
-   assistant
-   tool

### Tool Call

``` text
tool_name
arguments
call_id
```

### Tool Result

``` text
call_id
result
status
metadata
```

### Agent State

نمونه مفهومی:

``` text
AgentState {
    session_id
    messages
    current_goal
    context
    memory
    tool_results
    metadata
}
```

## مدل داده RAG

### جدول اجزای RAG

  جزء                نوع داده معمول           کلید/فیلدهای مهم
  ------------------ ------------------------ -----------------------------------
  Document           Object/Record            id, title, source, text, metadata
  Chunk              Object/Record            id, document_id, text, position
  Metadata           Map/JSON                 department, date, version, tags
  Embedding          Vector`<float>`{=html}   dimensions, model
  Vector Record      Record                   id, vector, payload
  Retrieval Result   Record                   chunk, score, rank
  Reranking Result   Record                   item, relevance_score
  KG Node            Record                   id, type, properties
  KG Edge            Record                   source, target, relation

یک مدل معمول RAG:

``` text
Document
├── id
├── title
├── source
├── text
├── metadata
└── chunks

Chunk
├── id
├── document_id
├── text
├── position
├── metadata
└── embedding

Vector Record
├── chunk_id
├── embedding
├── metadata
└── payload

Retrieval Result
├── chunk
├── similarity_score
└── rank
```

### Knowledge Graph

``` text
Node
├── id
├── type
└── properties

Edge
├── source
├── target
├── relation
└── properties
```

## نقشه یادگیری

برای تسلط حرفه‌ای:

``` text
Primitive Types
      ↓
Collections
      ↓
Data Structures
      ↓
Algorithms
      ↓
Complexity
      ↓
Type System
      ↓
Memory Model
      ↓
Generics
      ↓
Serialization
      ↓
Database Types
      ↓
Concurrency
      ↓
Distributed Data
      ↓
AI Data Types
      ↓
RAG Data Models
      ↓
Agent State & Memory
```

------------------------------------------------------------------------

# درس سوم --- مباحث حرفه‌ای و تکمیلی

## Type System

### جدول Type System در زبان‌های متداول

  ------------------------------------------------------------------------------------
  زبان           Typing غالب      Type Inference  Generics       Pattern Matching
  -------------- ---------------- --------------- -------------- ---------------------
  Python         Dynamic/Strong   محدود/Runtime   Type Hints     `match`

  JavaScript     Dynamic/Weak‌تر   Runtime         ندارد؛ TS دارد محدود/الگوها
                 از بسیاری زبان‌ها                                

  TypeScript     Static روی JS    قوی             بله            Control-flow
                                                                 narrowing

  Java           Static/Strong    بله             بله            `switch`/patternهای
                                                                 جدید

  C#             Static/Strong    بله             بله            Pattern Matching قوی

  C++            Static           `auto`          Templates      محدودتر/گسترش‌یافته

  Go             Static           `:=`            بله            `switch`/type switch

  Rust           Static/Strong    بسیار قوی       بله            بسیار قوی
  ------------------------------------------------------------------------------------

### مفاهیم تکمیلی

-   Static vs Dynamic
-   Strong vs Weak
-   Type Inference
-   Type Safety
-   Nominal vs Structural Typing
-   Algebraic Data Types
-   Variance

Type System مجموعه قواعدی است که مشخص می‌کند چه نوع‌هایی وجود دارند و چه
عملیاتی بین آن‌ها مجاز است.

### Static Typing

نوع‌ها در زمان کامپایل بررسی می‌شوند.

نمونه:

-   Java
-   C#
-   C++
-   Rust
-   Go

### Dynamic Typing

نوع مقدار در Runtime تعیین/بررسی می‌شود.

نمونه:

-   Python
-   JavaScript
-   Ruby

### Strong vs Weak Typing

Strong Typing معمولاً تبدیل‌های ناخواسته را محدودتر می‌کند؛ Weak Typing
ممکن است coercion بیشتری انجام دهد.

### Type Inference

کامپایلر نوع را از مقدار یا expression استنتاج می‌کند.

### Type Safety

هدف این است که عملیات ناسازگار نوعی قبل از ایجاد خطا شناسایی شوند.

### Nominal vs Structural Typing

-   **Nominal:** سازگاری نوع بر اساس نام/اعلان نوع
-   **Structural:** سازگاری بر اساس شکل و اعضای نوع

## Memory Model

### جدول Memory Management

  زبان         Stack/Heap   GC                    مدیریت حافظه اصلی
  ------------ ------------ --------------------- ------------------------------
  Python       دارد         بله                   Runtime/GC
  JavaScript   دارد         بله                   Engine/GC
  Java         دارد         بله                   JVM/GC
  C#           دارد         بله                   CLR/GC
  C++          دارد         خیر به‌صورت GC عمومی   RAII/Smart Pointer/Manual
  Go           دارد         بله                   GC
  Rust         دارد         خیر                   Ownership/Borrowing/Lifetime

### مفاهیم مهم

-   Allocation
-   Deallocation
-   Object Lifetime
-   Stack
-   Heap
-   Garbage Collection
-   Ownership
-   Borrowing
-   Lifetime
-   Memory Leak
-   Use-after-free

### Stack

برای داده‌های با lifetime و ساختار اجرای مناسب؛ معمولاً سریع و مدیریت آن
ساده است.

### Heap

برای داده‌های dynamic و Objectهایی با lifetime انعطاف‌پذیر.

### Value vs Reference

-   Value: خود مقدار منتقل می‌شود.
-   Reference: ارجاع به Object/Storage منتقل می‌شود.

### Object Lifetime

چرخه حیات یک Object:

``` text
Allocate
   ↓
Initialize
   ↓
Use
   ↓
Release / Garbage Collection
```

### Garbage Collection

در زبان‌هایی مانند Java، C# و JavaScript بخش مهمی از مدیریت حافظه خودکار
است.

### Ownership و Borrowing

Rust با Ownership، Borrowing و Lifetime کنترل بسیار دقیقی بر حافظه ارائه
می‌دهد.

## Mutability، Copy و Sharing

موضوعات مهم:

-   Mutable
-   Immutable
-   Shallow Copy
-   Deep Copy
-   Clone
-   Reference Sharing
-   Copy-on-Write

### Shallow Copy

ساختار سطحی کپی می‌شود ولی References داخلی ممکن است مشترک بمانند.

### Deep Copy

ساختار و داده‌های تو در تو نیز کپی می‌شوند.

این تفاوت در Python، JavaScript و زبان‌های Object-Oriented بسیار مهم است.

## Equality، Identity و Hashing

### جدول Equality و Identity

  -----------------------------------------------------------------------------------------------------------
  مفهوم      Python     JS/TS       Java           C#                  C++                Rust
  ---------- ---------- ----------- -------------- ------------------- ------------------ -------------------
  Value      `==`       `===`       `equals()`     `Equals()` / `==`   `operator==`       `PartialEq/Eq`
  Equality              معمولاً                     بسته به نوع                            

  Identity   `is`       Reference   `==` برای      `ReferenceEquals`   Address/identity   pointer/reference
                        identity با reference                          مفهومی             identity بسته به
                        `===` در    identity                                              context
                        Objectها                                                          

  Hash       `hash()`   Map/Set     `hashCode()`   `GetHashCode()`     `std::hash`        `Hash` trait
                        داخلی                                                             
  -----------------------------------------------------------------------------------------------------------

> در زبان‌ها و نوع‌های مختلف، معنی `==` یکسان نیست؛ همیشه مستندات همان
> زبان/نوع را بررسی کنید.

سه مفهوم را از هم جدا کنید:

### Value Equality

آیا دو مقدار محتوای برابر دارند؟

### Reference Equality

آیا دو Reference به یک Object اشاره می‌کنند؟

### Identity

آیا خود Object یکی است؟

### Hashing

تبدیل یک مقدار به Hash برای ساختارهایی مانند Hash Table/Dictionary.

برای Keyهای Hashable معمولاً باید رابطه منطقی بین Equality و Hash برقرار
باشد.

## Type Conversion

### جدول Type Conversion

  --------------------------------------------------------------------------------------------------------------------------------------------------------
  عملیات          Python           JS/TS                     Java                   C#                   C++             Go                Rust
  --------------- ---------------- ------------------------- ---------------------- -------------------- --------------- ----------------- ---------------
  String → Int    `int()`          `Number()`/`parseInt()`   `Integer.parseInt()`   `int.Parse()`        `stoi`          `strconv.Atoi`    `parse()`

  Int → String    `str()`          `String()`                `String.valueOf()`     `ToString()`         `to_string()`   `strconv.Itoa`    `to_string()`

  Explicit Cast   `int()`/typing   `Number()`                `(int)`                `(int)`              `(int)`         explicit          `as` برای برخی
                                                                                                                         conversion        تبدیل‌ها

  Serialization   JSON libs        `JSON.stringify`          Jackson/Gson و مشابه   `System.Text.Json`   کتابخانه        `encoding/json`   Serde
  --------------------------------------------------------------------------------------------------------------------------------------------------------

انواع تبدیل:

-   Implicit Conversion
-   Explicit Cast
-   Parsing
-   Coercion
-   Serialization
-   Deserialization

مثال مفهومی:

``` text
"123"
  ↓ parse
123
  ↓ convert
123.0
```

نکته مهم: تبدیل نوع با Serialization یکی نیست. Serialization معمولاً برای
تبدیل یک Object به representation قابل ذخیره/انتقال انجام می‌شود.

## Generics و Advanced Types

### جدول Advanced Type Features

  ------------------------------------------------------------------------------------------------------------------
  ویژگی          Python            TypeScript       Java               C#              C++            Rust
  -------------- ----------------- ---------------- ------------------ --------------- -------------- --------------
  Generic        Type Hints        بله              بله                بله             Templates      بله

  Union          `A \| B`          `A \| B`         الگو               محدودتر         `variant`      `enum`

  Intersection   محدود             `A & B`          Interface          Interface       Template       Trait bounds
                                                    composition        composition     constraints    

  Sum Type       Union/Enum        Discriminated    sealed             discriminated   `variant`      `enum`
                                   Union            hierarchy/record   patterns                       

  Product Type   class/dataclass   interface/type   class/record       class/record    struct/class   struct/tuple

  Pattern        `match`           narrowing        جدیدتر             قوی             محدودتر        قوی
  Matching                                                                                            
  ------------------------------------------------------------------------------------------------------------------

موضوعات حرفه‌ای:

-   Generic Type
-   Type Parameter
-   Generic Constraint
-   Union Type
-   Intersection Type
-   Optional Type
-   Sum Type
-   Product Type
-   Algebraic Data Type
-   Type Alias
-   Pattern Matching
-   Variance
-   Covariance
-   Contravariance
-   Invariance

### Algebraic Data Types

دو الگوی مهم:

**Product Type**

چند مقدار با هم:

``` text
Person = Name × Age × Email
```

**Sum Type**

یکی از چند حالت:

``` text
Result = Success | Error
```

این مفاهیم پایه طراحی Type-safe هستند.

## Complexity و انتخاب Collection

انتخاب Data Structure باید با Complexity هماهنگ باشد.

  عملیات           Array      Dynamic Array/List       Hash Map   Balanced Tree
  -------------- ------- ----------------------- -------------- ---------------
  Index Access      O(1)                    O(1)             \-              \-
  Search            O(n)                    O(n)   O(1) average        O(log n)
  Insert            O(n)   O(1) amortized at end   O(1) average        O(log n)
  Delete            O(n)                    O(n)   O(1) average        O(log n)

مقادیر دقیق به پیاده‌سازی و شرایط بستگی دارند.

### Big-Oهای کلیدی

``` text
O(1)       Constant
O(log n)   Logarithmic
O(n)       Linear
O(n log n) Linearithmic
O(n²)      Quadratic
O(2^n)     Exponential
```

## Serialization و Data Interchange

### جدول فرمت‌های Serialization

  فرمت          Text/Binary   Schema            خوانایی انسان   حجم/سرعت    کاربرد رایج
  ------------- ------------- ----------------- --------------- ----------- -------------------
  JSON          Text          ضمنی/Schema جدا   زیاد            متوسط       REST/API
  XML           Text          XSD و مشابه       زیاد            زیادتر      Enterprise/Legacy
  YAML          Text          ضمنی/Schema جدا   زیاد            متوسط       Configuration
  CSV           Text          ضعیف              زیاد            کم          داده جدولی
  MessagePack   Binary        معمولاً ضمنی       کم              خوب         انتقال سریع
  Protobuf      Binary        قوی               کم              بسیار خوب   Microservices
  Avro          Binary        قوی               کم              خوب         Data Engineering

### Schema Evolution

در سیستم Enterprise، نسخه‌بندی Schema و backward/forward compatibility
اهمیت زیادی دارد.

Serialization برای ذخیره یا انتقال داده استفاده می‌شود.

### JSON

مناسب API و Web.

### XML

مناسب سیستم‌های legacy و ساختارهای سندمحور.

### YAML

خوانا و مناسب Configuration، با این ملاحظه که parsing آن باید امن و
کنترل‌شده باشد.

### CSV

مناسب داده‌های جدولی ساده.

### Protocol Buffers

Binary، سریع و schema-based.

### Avro

مناسب داده‌های schema-based و اکوسیستم‌های Data Engineering.

### Schema Evolution

در سیستم‌های Enterprise باید تغییر نسخه Schema مدیریت شود:

``` text
Schema V1
   ↓
Schema V2
   ↓
Compatibility
```

## Database Data Types

### جدول Database Data Types

  ----------------------------------------------------------------------------------------
  نوع مفهومی     PostgreSQL          SQL Server           MySQL            کاربرد
  -------------- ------------------- -------------------- ---------------- ---------------
  Integer        `integer`           `int`                `INT`            شمارنده/شناسه

  Big Integer    `bigint`            `bigint`             `BIGINT`         مقادیر بزرگ

  Decimal        `numeric`           `decimal`            `DECIMAL`        مالی

  Text           `text`              `varchar/nvarchar`   `TEXT/VARCHAR`   متن

  Timestamp      `timestamp`         `datetime2`          `datetime`       زمان

  UUID           `uuid`              `uniqueidentifier`   `char/binary` یا شناسه
                                                          الگو             

  JSON           `json/jsonb`        `json`               `JSON`           داده
                                                                           نیمه‌ساخت‌یافته

  Array          `type[]`            الگوی دیگر           محدودتر          چندمقداری

  Vector         extension/feature   وابسته به            وابسته           Embedding
                                     نسخه/راهکار                           
  ----------------------------------------------------------------------------------------

انواع مهم در پایگاه داده:

-   Integer
-   BigInt
-   Decimal/Numeric
-   Float
-   Boolean
-   Char/Varchar/Text
-   Date/Time
-   Timestamp
-   UUID
-   Binary/BLOB
-   JSON/JSONB
-   Array
-   Enum
-   Vector

### Domain Data Types

در طراحی حرفه‌ای فقط نوع خام کافی نیست. گاهی Value Object مناسب‌تر است:

``` text
EmailAddress
Money
UserId
ProductCode
PhoneNumber
```

این کار Validation و Domain Rules را بهتر می‌کند.

## Concurrency و Data Safety

### جدول مفاهیم Concurrency

  --------------------------------------------------------------------------------------------------------------------------------------------
  مفهوم          Python        JavaScript             Java                  C#                 C++             Go              Rust
  -------------- ------------- ---------------------- --------------------- ------------------ --------------- --------------- ---------------
  Thread         `threading`   Worker                 `Thread`              `Thread`           `std::thread`   goroutine       `std::thread`

  Lock/Mutex     `Lock`        Atomics/locks via      `Lock`/synchronized   `lock`/Monitor     `mutex`         `sync.Mutex`    `Mutex`
                               patterns                                                                                        

  Atomic         `atomic`      `Atomics`              `Atomic*`             `Interlocked`      `<atomic>`      `sync/atomic`   `Atomic*`

  Channel        queue/async   MessageChannel         BlockingQueue/Flow    Channel            libraries       built-in `chan` channels
                 patterns                                                                                                      

  Immutability   convention    primitive/structural   design                records/readonly   const/design    design          default
                               patterns                                     patterns                                           immutable
                                                                                                                               bindings
  --------------------------------------------------------------------------------------------------------------------------------------------

موضوعات مهم:

-   Thread Safety
-   Race Condition
-   Deadlock
-   Lock
-   Mutex
-   Semaphore
-   Atomic Operation
-   Concurrent Collection
-   Immutable Data
-   Actor Model

### Race Condition

وقتی نتیجه برنامه به ترتیب اجرای هم‌زمان عملیات وابسته شود.

### Immutable Data

یکی از راه‌های کاهش پیچیدگی Shared State است.

## Distributed Systems Data

### جدول Distributed Data

  -----------------------------------------------------------------------
  مفهوم                   تعریف کوتاه             مثال
  ----------------------- ----------------------- -----------------------
  Message                 داده‌ای برای ارسال بین   Agent → Tool
                          اجزا                    

  Event                   رخدادی که اتفاق افتاده  `OrderCreated`

  Event Stream            دنباله Eventها          Event Log

  Queue                   صف پردازش               Job Queue

  Topic                   کانال انتشار/اشتراک     Pub/Sub

  Cache                   کپی سریع داده           Redis-like cache

  Session                 وضعیت یک تعامل          User/Agent Session

  Distributed State       وضعیت مشترک بین Nodeها  Workflow State

  Event Sourcing          State از Eventها        Audit/Domain Systems
                          بازسازی می‌شود           

  CQRS                    تفکیک Command و Query   Enterprise Backend

  Idempotency Key         جلوگیری از اثر تکراری   Payment/API
  -----------------------------------------------------------------------

در سیستم‌های توزیع‌شده با این مفاهیم روبه‌رو می‌شویم:

-   Message
-   Event
-   Event Stream
-   Queue
-   Topic
-   Cache
-   Session
-   Distributed State
-   Serialization
-   Schema
-   Event Sourcing
-   CQRS
-   Idempotency
-   Consistency

### Event

رویدادی که رخ داده است:

``` text
OrderCreated
PaymentCompleted
DocumentIndexed
```

### Idempotency

یک عملیات idempotent در اجرای تکراری، نتیجه منطقی ناخواسته ایجاد نمی‌کند.
این موضوع برای API و سیستم‌های Agent بسیار مهم است.

## AI/LLM Data Models

### جدول ساختارهای داده AI/LLM

  -----------------------------------------------------------------------
  Data Model              فیلدهای نمونه           نقش
  ----------------------- ----------------------- -----------------------
  Token                   `text`, `id`            واحد متن

  Embedding               `vector`, `model`,      Semantic Search
                          `dimension`             

  Tensor                  `shape`, `dtype`,       محاسبات مدل
                          `device`, `data`        

  Message                 `role`, `content`,      Conversation
                          `metadata`              

  Tool Call               `name`, `arguments`,    Tool Use
                          `call_id`               

  Tool Result             `call_id`, `output`,    Tool Response
                          `status`                

  Memory Item             `id`, `content`,        Agent Memory
                          `type`, `timestamp`     

  Agent State             `session_id`,           Workflow/Agent
                          `messages`, `context`,  
                          `memory`                

  Model Response          `content`, `usage`,     خروجی LLM
                          `finish_reason`         
  -----------------------------------------------------------------------

### Tensor Metadata

در کار حرفه‌ای فقط خود Tensor کافی نیست؛ این موارد نیز مهم‌اند:

-   `shape`
-   `dtype`
-   `device`
-   `layout`
-   `requires_grad`
-   `quantization`

مدل‌های داده مهم AI:

  نوع              کاربرد
  ---------------- --------------------
  Token            واحد متن برای مدل
  Token ID         شناسه عددی Token
  Tensor           نمایش چندبعدی داده
  Vector           بردار عددی
  Embedding        نمایش معنایی
  Logits           امتیاز خام خروجی
  Probability      احتمال خروجی
  Attention Mask   کنترل توجه
  Message          پیام مکالمه
  Tool Call        درخواست ابزار
  Tool Result      نتیجه ابزار
  Agent State      وضعیت Agent
  Memory Item      واحد حافظه
  Document         سند
  Chunk            قطعه سند
  Metadata         اطلاعات توصیفی

## RAG Data Models

### جدول کامل‌تر RAG Data Model

  مدل                نمونه فیلدها                        مرحله
  ------------------ ----------------------------------- -----------------
  Source             URI/path, type, owner               Ingestion
  Document           id, title, text, source, metadata   Parsing
  Chunk              id, document_id, text, position     Chunking
  Embedding          vector, model, dimension            Embedding
  Vector Record      id, vector, payload                 Indexing
  Retrieval Result   id, score, chunk                    Retrieval
  Rerank Result      id, relevance_score                 Reranking
  Context            selected chunks, citations          Generation
  KG Node            id, type, properties                Knowledge Graph
  KG Edge            source, target, relation            Knowledge Graph
  Citation           document_id, chunk_id, span         Grounding

### Metadataهای Enterprise

`department`, `document_type`, `version`, `effective_date`,
`security_level`, `language`, `tags`, `owner`, `source`, `checksum` و
`access_policy` از نمونه‌های مهم هستند.

یک RAG Enterprise معمولاً این زنجیره را دارد:

``` text
Source
  ↓
Document
  ↓
Parsed Content
  ↓
Chunk
  ↓
Embedding
  ↓
Vector Record
  ↓
Similarity Search
  ↓
Retrieval Result
  ↓
Reranking
  ↓
Context
  ↓
LLM
  ↓
Answer
```

### Metadata

نمونه:

``` text
{
  document_id,
  source,
  department,
  document_type,
  title,
  date,
  version,
  language,
  access_level,
  tags
}
```

### Similarity Score

برای رتبه‌بندی نتایج بازیابی استفاده می‌شود؛ معیارهای متداول:

-   Cosine Similarity
-   Dot Product
-   Euclidean Distance

### Reranking Result

بعد از Retrieval اولیه، مدل Reranker می‌تواند نتایج را دوباره مرتب کند.

## زنجیره کامل دانش

### جدول سطح‌بندی نهایی دانش

    سطح موضوع                     خروجی مورد انتظار
  ----- ------------------------- ---------------------------
      1 Primitive Types           شناخت نوع‌های پایه
      2 Collections               انتخاب Collection مناسب
      3 Data Structures           طراحی ساختار داده
      4 Algorithms                حل مسئله
      5 Complexity                تحلیل هزینه
      6 Type System               Type-safe Design
      7 Memory Model              مدیریت منابع
      8 Generics/Advanced Types   طراحی reusable
      9 Equality/Hashing          رفتار صحیح Collectionها
     10 Serialization/Schema      انتقال و ذخیره داده
     11 Database Types            مدل‌سازی Persistence
     12 Concurrency               اجرای امن هم‌زمان
     13 Distributed Data          طراحی سیستم توزیع‌شده
     14 AI Data                   Tensor/Embedding/Token
     15 RAG Data                  Document/Chunk/Vector
     16 Agent Data                State/Message/Tool/Memory
     17 Enterprise AI             ترکیب همه لایه‌ها

برای یک مهندس نرم‌افزار و AI Engineer، تصویر کامل را می‌توان این‌گونه خلاصه
کرد:

``` text
Data
 ↓
Data Type
 ↓
Type System
 ↓
Memory Model
 ↓
Collection
 ↓
Data Structure
 ↓
Algorithm
 ↓
Complexity
 ↓
Generic / Advanced Type
 ↓
Equality / Identity / Hashing
 ↓
Mutability / Immutability
 ↓
Copy / Reference / Ownership
 ↓
Type Conversion
 ↓
Serialization
 ↓
Schema / Validation
 ↓
Database Data Type
 ↓
Concurrency
 ↓
Distributed Data
 ↓
Event / Message
 ↓
AI Data Type
 ↓
Tensor / Vector / Embedding
 ↓
Document / Chunk / Metadata
 ↓
RAG Data Model
 ↓
Agent State
 ↓
Memory
 ↓
Enterprise AI System
```

## جمع‌بندی نهایی

اگر هدف فقط برنامه‌نویسی مقدماتی باشد، دانستن Primitive Types، String،
Array/List، Set، Map، Tuple، Object و چند Data Structure اصلی کافی است.

اگر هدف **Software Engineering حرفه‌ای** باشد، باید Type System، Memory
Model، Complexity، Generics، Equality، Mutability، Serialization،
Database Types، Concurrency و Distributed Data را نیز یاد گرفت.

اگر هدف **AI/LLM/Agentic AI Engineering** باشد، این مباحث باید تا این
سطح ادامه پیدا کنند:

``` text
Tensor
Embedding
Vector
Token
Message
Tool Call
Tool Result
Document
Chunk
Metadata
Vector Record
Retrieval Result
Knowledge Graph
Agent State
Memory
```

بنابراین یک مهندس حرفه‌ای فقط «نوع داده» را نمی‌شناسد؛ بلکه می‌داند **داده
چگونه نمایش داده، ذخیره، کپی، مقایسه، منتقل، ایمن، ایندکس، بازیابی و در
نهایت در یک سیستم AI استفاده می‌شود.**
