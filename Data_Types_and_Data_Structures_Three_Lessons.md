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

### Pointer

آدرس حافظه را نگه می‌دارد و در زبان‌هایی مانند C/C++ اهمیت زیادی دارد.

### Reference

به یک Object یا مقدار دیگر ارجاع می‌دهد و معمولاً abstraction بالاتری از
Pointer دارد.

## Date/Time، UUID و Big Integer

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

  ویژگی        Array                       List           Tuple
  ------------ --------------------------- -------------- -----------------
  ترتیب        معمولاً دارد                 دارد           دارد
  تغییرپذیری   وابسته به زبان              معمولاً دارد    اغلب ندارد
  اندازه       ثابت/محدود در برخی زبان‌ها   پویا           ثابت
  کاربرد       داده‌های indexed             مجموعه عمومی   چند مقدار مرتبط
  مثال         `int[10]`                   `[1,2,3]`      `(x,y)`

## Mutable و Immutable

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
