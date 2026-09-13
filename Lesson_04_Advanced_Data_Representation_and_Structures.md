# درس چهارم — Advanced Data Representation & Structures

> تمرکز: نمایش واقعی داده در حافظه، performance، ساختارهای پیشرفته، داده توزیع‌شده و internals مربوط به AI/RAG.

## فهرست مطالب

- 4.1 — Bit، Byte و Word
- 4.2 — Binary و Hexadecimal
- 4.3 — Signed و Unsigned
- 4.4 — Endianness
- 4.5 — Alignment و Padding
- 4.6 — IEEE 754
- 4.7 — NaN و Infinity
- 4.8 — Overflow و Underflow
- 4.9 — Unicode
- 4.10 — UTF-8 / UTF-16 / UTF-32
- 4.11 — Grapheme Cluster
- 4.12 — Unicode Normalization
- 4.13 — Memory Layout
- 4.14 — Stack در برابر Heap
- 4.15 — Lifetime
- 4.16 — CPU Cache
- 4.17 — Cache Line
- 4.18 — AoS در برابر SoA
- 4.19 — Advanced Data Structures
- 4.20 — Probabilistic Data Structures
- 4.21 — Database Index
- 4.22 — Inverted Index
- 4.23 — LSM Tree
- 4.24 — Data Modeling
- 4.25 — Schema
- 4.26 — Schema Evolution
- 4.27 — Functional Data Structures
- 4.28 — Distributed Data
- 4.29 — Consistency
- 4.30 — CRDT
- 4.31 — Event Sourcing
- 4.32 — CQRS
- 4.33 — Idempotency
- 4.34 — AI/LLM Data Internals
- 4.35 — Token
- 4.36 — Vocabulary
- 4.37 — Tensor
- 4.38 — Tensor Rank
- 4.39 — DType
- 4.40 — Quantization
- 4.41 — Embedding
- 4.42 — Similarity
- 4.43 — Vector Index
- 4.44 — RAG Internals
- 4.45 — Chunking
- 4.46 — Metadata
- 4.47 — Hybrid Search
- 4.48 — RAG Quality
- 4.49 — Agent Data Model
- 4.50 — Checkpoint
- 4.51 — Memory در Agent
- 4.52 — Event و Trace
- 4.53 — جدول نهایی زبان‌ها
- 4.54 — مهم‌ترین تفاوت Zig و Carbon
- 4.55 — چهار سطح نهایی Data Knowledge
- 4.56 — جمع‌بندی درس چهارم

---

## 4.1 — Bit، Byte و Word

تمام داده‌های دیجیتال در نهایت به bit تبدیل می‌شوند:

```text
Bit → Byte → Word → Memory → Data Structure → Application
```

- Bit: کوچک‌ترین واحد داده، `0` یا `1`
- `1 Byte = 8 bits`
- `1 Nibble = 4 bits`
- یک Byte از دو nibble تشکیل می‌شود.

```text
1010 1101
 ↑↑↑↑ ↑↑↑↑
 nibble nibble
```

Word وابسته به architecture است:

| Architecture | Word رایج |
|---|---:|
| 8-bit | 8 bit |
| 16-bit | 16 bit |
| 32-bit | 32 bit |
| 64-bit | 64 bit |

> word size، pointer size، register size و data type size الزاماً همیشه یکی نیستند.

## 4.2 — Binary و Hexadecimal

برای `Decimal = 255`:

| سیستم | مقدار |
|---|---:|
| Decimal | 255 |
| Binary | 11111111 |
| Hexadecimal | FF |
| Octal | 377 |

نمونه‌های مهم:

```text
0xFF
0x00
0x7F
0x8000
0xFFFFFFFF
```

کاربردها: memory dump، network packet، file format، color codes، permissions، machine code، cryptography و debugging.

## 4.3 — Signed و Unsigned

برای 8 بیت:

| Type | Range |
|---|---|
| `uint8` | 0 … 255 |
| `int8` | -128 … 127 |

Signed معمولاً از Two's Complement استفاده می‌کند. این موضوع در binary protocol، image processing، networking، embedded، cryptography و serialization مهم است.

## 4.4 — Endianness

برای:

```text
0x12345678
```

**Big Endian**

```text
12 34 56 78
```

**Little Endian**

```text
78 56 34 12
```

| موضوع | Big Endian | Little Endian |
|---|---|---|
| Most Significant Byte | ابتدا | انتها |
| Least Significant Byte | انتها | ابتدا |

ترتیب byteها هنگام تبادل فایل و packet اهمیت دارد.

## 4.5 — Alignment و Padding

مثال:

```c
struct Example {
    char a;
    int b;
}
```

ممکن است اندازه به جای 5، مثلاً 8 byte شود:

```text
a
padding
padding
padding
b b b b
```

| مفهوم | معنی |
|---|---|
| Alignment | آدرس مناسب برای type |
| Padding | فضای اضافه برای alignment |
| Packing | حذف/کاهش padding |
| ABI | قرارداد binary بین compiler و platform |
| Layout | ترتیب واقعی fieldها در memory |

در C/C++/Rust/Zig و interoperability مهم است.

## 4.6 — IEEE 754

Floating-point معمولاً تقریبی ذخیره می‌شود.

مدل ساده:

```text
sign | exponent | fraction/significand
```

در float32:

```text
1 bit | 8 bits | 23 bits
```

به همین دلیل:

```text
0.2 + 0.4
```

ممکن است دقیقاً برابر representation ذخیره‌شده برای `0.6` نباشد.

## 4.7 — NaN و Infinity

| مقدار | معنی |
|---|---|
| `0` | صفر |
| `-0` | صفر منفی |
| `Infinity` | بی‌نهایت |
| `-Infinity` | منفی بی‌نهایت |
| `NaN` | Not a Number |

مثلاً در floating-point:

```text
1 / 0 → Infinity
0 / 0 → NaN
```

رفتار دقیق به زبان و نوع عددی بستگی دارد.

## 4.8 — Overflow و Underflow

مفاهیم مهم:

- Overflow
- Underflow
- Wraparound
- Saturation
- Exception
- Panic
- Undefined Behavior

برای `uint8`، عبارت `255 + 1` بسته به زبان و context رفتار متفاوتی دارد.

## 4.9 — Unicode

برای کار حرفه‌ای با متن باید این مفاهیم را شناخت:

- Unicode
- Code Point
- Encoding
- UTF-8
- UTF-16
- UTF-32
- Grapheme Cluster
- Normalization

```text
Byte ≠ Code Point ≠ Grapheme Cluster
```

این موضوع در فارسی، عربی، emoji، ترکیب حروف، جستجو، validation و text length اهمیت دارد.

## 4.10 — UTF-8 / UTF-16 / UTF-32

| Encoding | ویژگی |
|---|---|
| UTF-8 | 1 تا 4 byte |
| UTF-16 | واحدهای 16-bit |
| UTF-32 | واحدهای 32-bit |

UTF-8، ASCII-compatible، بسیار رایج در web و مناسب فایل‌های متنی است.

## 4.11 — Grapheme Cluster

ممکن است:

```text
bytes ≠ code points ≠ grapheme clusters
```

باشد. بنابراین `string.length` لزوماً تعداد کاراکترهای قابل مشاهده را نشان نمی‌دهد.

## 4.12 — Unicode Normalization

فرم‌های مهم:

- NFC
- NFD
- NFKC
- NFKD

کاربردها: Search، Database matching، Usernames، Validation، Security و Deduplication.

## 4.13 — Memory Layout

به‌صورت مفهومی:

```text
Process Memory
│
├── Code / Text
├── Read-only Data
├── Global / Static Data
├── Heap
└── Stack
```

Layout واقعی به OS، compiler، runtime و architecture وابسته است.

## 4.14 — Stack در برابر Heap

| ویژگی | Stack | Heap |
|---|---|---|
| Allocation | معمولاً بسیار سریع | معمولاً پیچیده‌تر |
| Lifetime | معمولاً scope-based | dynamic |
| اندازه | محدودتر | بزرگ‌تر |
| مدیریت | runtime/compiler | allocator/GC/programmer |
| کاربرد | call frames/local state | dynamic objects |

> هر local variable الزاماً روی stack و هر object الزاماً روی heap نیست؛ compiler می‌تواند optimization انجام دهد.

## 4.15 — Lifetime

```text
Create → Use → No longer needed → Destroy / Reclaim
```

| زبان | مدیریت |
|---|---|
| Python | GC/reference counting |
| JavaScript | GC |
| Java | GC |
| C# | GC |
| Go | GC |
| C++ | RAII/manual/resource ownership |
| Rust | ownership + lifetime |
| Zig | programmer-controlled allocation |
| Carbon | memory model در حال تکامل |

## 4.16 — CPU Cache

Hierarchy:

```text
CPU Registers → L1 → L2 → L3 → RAM → SSD → HDD
```

- **Temporal Locality:** استفاده اخیر احتمال استفاده مجدد را بالا می‌برد.
- **Spatial Locality:** آدرس‌های نزدیک به آدرس استفاده‌شده احتمالاً نیز استفاده می‌شوند.

## 4.17 — Cache Line

CPU معمولاً block یا cache line را منتقل می‌کند، نه یک byte منفرد.

```text
[A][B][C][D][E][F]
```

معمولاً locality خوبی دارد.

در مقابل:

```text
A → X → M → Q → B
```

ممکن است cache locality ضعیف‌تری داشته باشد.

## 4.18 — AoS در برابر SoA

### Array of Structures

```text
Person
Person
Person
Person
```

هر Person شامل `age`, `salary`, `score` است.

### Structure of Arrays

```text
ages[]
salaries[]
scores[]
```

| مورد | AoS | SoA |
|---|---|---|
| object-centric | عالی | ضعیف‌تر |
| column processing | ضعیف‌تر | عالی |
| SIMD | معمولاً سخت‌تر | مناسب |
| analytics | متوسط | بسیار مناسب |
| ECS/game engine | بستگی دارد | بسیار رایج |

در AI، GPU، analytics و high-performance computing مهم است.

## 4.19 — Advanced Data Structures

| Structure | کاربرد |
|---|---|
| AVL Tree | balanced search |
| Red-Black Tree | ordered map/set |
| B-Tree | database |
| B+Tree | database/range |
| Skip List | ordered probabilistic |
| Union-Find | connectivity |
| Segment Tree | range queries |
| Fenwick Tree | prefix sums |
| Persistent Structure | versioned state |
| Rope | text editing |
| Interval Tree | interval queries |
| Suffix Array | text processing |

## 4.20 — Probabilistic Data Structures

### Bloom Filter

```text
YES → شاید وجود داشته باشد
NO  → قطعاً وجود ندارد
```

مزیت: مصرف حافظه بسیار کم.

### Count-Min Sketch

برای تخمین frequency بدون نگهداری تمام counterها.

### HyperLogLog

برای تخمین تعداد uniqueها با حافظه بسیار کمتر از exact counting.

## 4.21 — Database Index

بدون index ممکن است:

```text
Full Table Scan
```

انجام شود.

ساختارهای مهم:

- B-Tree
- B+Tree
- Hash Index
- Bitmap Index
- Inverted Index
- Spatial Index
- Vector Index

## 4.22 — Inverted Index

به جای:

```text
Document → Words
```

می‌سازیم:

```text
Word → Documents
```

مثلاً:

```text
"python" → Doc1, Doc4, Doc9
"agent"  → Doc2, Doc4
"rag"    → Doc3, Doc4, Doc8
```

اساس بسیاری از Full Text Search، Search Engine، BM25 و Enterprise Search است.

## 4.23 — LSM Tree

LSM = Log-Structured Merge Tree

```text
Write
 ↓
MemTable
 ↓
SSTable
 ↓
Compaction
 ↓
Larger SSTables
```

مزیت: Sequential Write + Batching. مناسب workloadهای write-heavy.

## 4.24 — Data Modeling

| مفهوم | معنی |
|---|---|
| Entity | دارای identity |
| Value Object | value محور |
| Aggregate | consistency boundary |
| DTO | انتقال داده |
| Command | درخواست تغییر |
| Event | رخداد |
| Read Model | مدل مخصوص read |
| Domain Model | مدل کسب‌وکار |

## 4.25 — Schema

مثال:

```text
Employee
 ├── id
 ├── name
 ├── department
 ├── salary
 └── hire_date
```

Schema می‌تواند شامل Type، Required، Nullable، Default، Range، Pattern، Enum، Constraint و Relationship باشد.

## 4.26 — Schema Evolution

نسخه اول:

```text
Employee
 ├── id
 └── name
```

نسخه دوم:

```text
Employee
 ├── id
 ├── name
 └── department
```

این یک additive change است.

روش امن:

```text
Add → Deploy → Read → Backfill → Validate → Deprecate → Remove
```

## 4.27 — Functional Data Structures

مفاهیم:

- Immutable
- Persistent
- Structural Sharing
- ADT
- Pattern Matching
- Higher-Order Function

مثلاً:

```text
new_state = update(state)
```

که state قبلی قابل استفاده باقی می‌ماند.

کاربرد: concurrency، undo/redo، versioning، distributed systems و functional programming.

## 4.28 — Distributed Data

مسائل مهم:

- Replication
- Partitioning
- Sharding
- Consistency
- Consensus
- Ordering
- Conflict
- Retry
- Duplicate

## 4.29 — Consistency

| مدل | مفهوم |
|---|---|
| Strong Consistency | مشاهده state جدید |
| Eventual Consistency | همگرایی در زمان |
| Linearizability | رفتار شبیه یک نسخه واحد |
| Causal Consistency | حفظ روابط علّی |

## 4.30 — CRDT

CRDT در برخی مدل‌های distributed state امکان merge بدون coordination شدید را فراهم می‌کند.

```text
Node A
   \
    Merge
   /
Node B
```

اصل:

```text
Local Update + Deterministic Merge
```

اما برای هر مسئله‌ای مناسب نیست.

## 4.31 — Event Sourcing

به جای فقط state نهایی:

```text
Balance = 100
```

eventها ذخیره می‌شوند:

```text
Deposit 100
Withdraw 20
Deposit 20
```

و state با replay بازسازی می‌شود:

```text
Events → Replay → State
```

## 4.32 — CQRS

**Command Query Responsibility Segregation**

```text
             ┌── Command Model
Request ─────┤
             └── Query Model
```

مناسب سیستم‌هایی که read و write characteristics متفاوت دارند.

## 4.33 — Idempotency

اگر request دوبار اجرا شد، نتیجه نباید ناخواسته دوبار اعمال شود.

```text
Request
Request again
```

مثلاً Payment با `Idempotency-Key` کنترل می‌شود.

## 4.34 — AI/LLM Data Internals

Pipeline:

```text
Text
 ↓
Tokenizer
 ↓
Token IDs
 ↓
Embedding
 ↓
Tensor
 ↓
Transformer
 ↓
Logits
 ↓
Probability
 ↓
Token
 ↓
Text
```

## 4.35 — Token

```text
Text → Tokens → Token IDs
```

هر token یک ID دارد و tokenization می‌تواند subword-based باشد.

## 4.36 — Vocabulary

```text
Token → ID
```

مثلاً:

```json
{
  "hello": 1234,
  "world": 5678
}
```

## 4.37 — Tensor

Tensor تعمیم آرایه چندبعدی است.

```text
[batch, sequence, hidden]
```

برای:

```text
batch = 2
sequence = 512
hidden = 4096
```

داریم:

```text
Shape = [2, 512, 4096]
```

## 4.38 — Tensor Rank

| Tensor | Rank |
|---|---:|
| Scalar | 0 |
| Vector | 1 |
| Matrix | 2 |
| 3D Tensor | 3 |
| 4D Tensor | 4 |

مثلاً `[batch, channels, height, width]` یک tensor چهاربعدی است.

## 4.39 — DType

| DType | کاربرد |
|---|---|
| FP32 | precision بالا |
| FP16 | memory کمتر |
| BF16 | ML بسیار رایج |
| INT8 | quantized inference |
| INT4 | memory بسیار کمتر |
| UINT8 | برخی داده‌های خام |

بنابراین:

```text
Tensor =
Shape + DType + Data + Layout/Stride
```

## 4.40 — Quantization

```text
FP32 → FP16 → INT8 → INT4
```

هدف:

```text
Memory ↓
Bandwidth ↓
Potential Speed ↑
```

در مقابل ممکن است Accuracy کاهش یابد.

Trade-off:

```text
Memory ↔ Speed ↔ Accuracy
```

## 4.41 — Embedding

```text
Document
 ↓
Embedding Model
 ↓
[0.12, -0.42, 0.87, ...]
```

Embedding یک vector عددی برای نمایش ویژگی‌های معنایی داده است.

## 4.42 — Similarity

روش‌ها:

- Cosine Similarity: مقایسه زاویه دو vector
- Dot Product: `A · B`
- Euclidean Distance: `distance(A,B)`

| Metric | کاربرد |
|---|---|
| Cosine | semantic similarity |
| Dot Product | retrieval/model-dependent |
| Euclidean | geometric distance |

## 4.43 — Vector Index

روش‌های مهم:

- Flat
- HNSW
- IVF
- PQ
- Hybrid

### HNSW

Graph-based approximate nearest neighbor:

```text
Query
 ↓
Navigate Graph
 ↓
Nearest Candidates
 ↓
Top K
```

## 4.44 — RAG Internals

```text
Documents
 ↓
Parsing
 ↓
Cleaning
 ↓
Chunking
 ↓
Metadata
 ↓
Embedding
 ↓
Vector Store
 ↓
Query
 ↓
Retrieval
 ↓
Filtering
 ↓
Reranking
 ↓
Context
 ↓
LLM
 ↓
Answer
 ↓
Citation
```

## 4.45 — Chunking

| روش | مزیت |
|---|---|
| Fixed-size | ساده |
| Token-based | کنترل context |
| Sentence | خوانایی |
| Paragraph | semantic coherence |
| Recursive | عمومی |
| Semantic | کیفیت معنایی |
| Structure-aware | مناسب اسناد سازمانی |
| Parent-Child | context بهتر |

برای اسناد سازمانی معمولاً structure-aware chunking اهمیت زیادی دارد.

## 4.46 — Metadata

نمونه:

```text
document_id
department
document_type
title
date
version
section
page
source
security_level
language
```

کاربردها:

- filtering
- access control
- provenance
- citation
- retrieval

## 4.47 — Hybrid Search

یک RAG قوی می‌تواند ترکیب کند:

```text
Dense Search
+
BM25
+
Metadata Filter
+
Reranker
```

```text
Query
 ├── Vector Search
 ├── Keyword Search
 └── Metadata Filter
          ↓
        Fusion
          ↓
       Reranker
          ↓
         Top-K
```

## 4.48 — RAG Quality

| Metric | سؤال |
|---|---|
| Recall | آیا نتیجه صحیح پیدا شد؟ |
| Precision | چند نتیجه واقعاً مرتبط بودند؟ |
| MRR | اولین نتیجه صحیح کجاست؟ |
| NDCG | ranking چقدر خوب است؟ |
| Faithfulness | پاسخ مطابق context است؟ |
| Groundedness | پاسخ به source متکی است؟ |
| Citation Accuracy | citation درست است؟ |

## 4.49 — Agent Data Model

```text
Session
 ├── Messages
 ├── State
 ├── Workflow
 ├── Tool Calls
 ├── Tool Results
 ├── Memory
 ├── Events
 ├── Checkpoints
 └── Traces
```

### Message

```text
message_id
role
content
metadata
timestamp
```

### Tool Call

```text
call_id
tool_name
arguments
```

### Tool Result

```text
call_id
output
error
metadata
```

### State

```text
session_id
current_step
variables
messages
memory_refs
workflow_status
```

## 4.50 — Checkpoint

Checkpoint یعنی snapshot از state:

```text
State → Checkpoint → Continue
```

کاربردها: workflow recovery، retry، pause/resume، debugging، human-in-the-loop و fault tolerance.

## 4.51 — Memory در Agent

انواع:

- Short-Term Memory
- Long-Term Memory
- Episodic Memory
- Semantic Memory
- Procedural Memory
- Working Memory

مدل:

```text
MemoryItem
 ├── id
 ├── content
 ├── type
 ├── timestamp
 ├── importance
 ├── metadata
 └── embedding
```

## 4.52 — Event و Trace

برای enterprise observability:

```text
Event
Trace
Span
Metric
Log
```

| نوع | هدف |
|---|---|
| Log | اتفاق/پیام |
| Metric | عدد قابل اندازه‌گیری |
| Trace | مسیر یک عملیات |
| Span | یک مرحله از trace |
| Event | رخداد business/system |

## 4.53 — جدول نهایی زبان‌ها

| ویژگی | Python | JS/TS | Java | C# | C++ | Go | Rust | Zig | Carbon |
|---|---|---|---|---|---|---|---|---|---|
| Type System | Dynamic | Dynamic/Static TS | Static | Static | Static | Static | Static | Static | Static، در حال توسعه |
| GC | Yes | Yes | Yes | Yes | No | Yes | No | No | در حال طراحی |
| Ownership | Runtime | GC | GC | GC | RAII | GC | Ownership | Explicit | در حال طراحی |
| Borrowing | No | No | No | No | No | No | Yes | No | در حال توسعه |
| Pointer | محدود | No | No | محدود | Yes | Yes | Yes | Yes | systems-oriented |
| Generics | Yes | Yes | Yes | Yes | Templates | Yes | Yes | comptime | evolving |
| Tuple | Yes | TS | محدود | Yes | Yes | محدود | Yes | Yes | evolving |
| Enum | Yes | TS | Yes | Yes | const pattern | Yes | بسیار قدرتمند | Yes | evolving |
| Hash Map | dict | Map | HashMap | Dictionary | unordered_map | map | HashMap | hash maps | evolving |
| Dynamic Array | list | Array | ArrayList | List | vector | slice | Vec | ArrayList | evolving |
| Async | asyncio | Promise | futures/threads | Task | coroutine | goroutine | async/await | evolving | evolving |
| Low-level | متوسط | کم | متوسط | متوسط | بسیار بالا | بالا | بسیار بالا | بسیار بالا | بسیار بالا |
| Compile-time | محدود | TS type system | generics | generics | templates | محدود | const/macros | comptime | evolving |
| Ecosystem | بسیار بزرگ | بسیار بزرگ | بسیار بزرگ | بسیار بزرگ | بسیار بزرگ | بزرگ | بزرگ | رو به رشد | experimental |

## 4.54 — مهم‌ترین تفاوت Zig و Carbon

### Zig

Zig یک زبان systems programming است با تأکید بر:

```text
simplicity + explicitness + comptime + manual memory management
```

مفهوم بسیار مهم:

```text
Allocator
```

است و programmer معمولاً باید نسبت به allocation و lifetime آگاه باشد.

### Carbon

Carbon با هدف مسیر مدرن‌تری برای systems programming و تعامل بهتر با ecosystem موجود، به‌خصوص C++، طراحی شده است.

> **Carbon را نباید مانند Python، Java، C# یا C++ یک زبان کاملاً تثبیت‌شده با ecosystem بالغ فرض کرد.**

برای آموزش type system و آینده systems programming جالب است؛ اما برای production selection باید نسخه، compiler، tooling و ecosystem آن جداگانه بررسی شود.

## 4.55 — چهار سطح نهایی Data Knowledge

### Level 1 — Logical Data

```text
Integer
String
Boolean
Object
Array
Map
```

### Level 2 — Data Structure

```text
Stack
Queue
Tree
Heap
Graph
Hash Table
B-Tree
LSM
Trie
```

### Level 3 — Physical Representation

```text
Bit
Byte
Binary
Hex
Memory
Pointer
Alignment
Padding
Cache
Encoding
IEEE-754
```

### Level 4 — Modern System Data

```text
Database
Distributed State
Event
Tensor
Embedding
Vector
RAG
Message
Tool Call
Agent State
Memory
```

## 4.56 — جمع‌بندی درس چهارم

```text
                           DATA
                             │
              ┌──────────────┴──────────────┐
              │                             │
        Logical Data                  Physical Data
              │                             │
       ┌──────┼──────┐              ┌───────┼────────┐
       │      │      │              │       │        │
     Types Structures Objects      Bits    Memory  Encoding
       │      │                     │       │
       │      ├── Tree              │       ├── Stack
       │      ├── Graph             │       ├── Heap
       │      ├── Hash              │       └── Cache
       │      └── B-Tree            │
       │                            └── Byte/Alignment
       │
       └──────────────────────────────────────────┐
                                                  │
                                           System Data
                                                  │
                           ┌──────────────────────┼─────────────────┐
                           │                      │                 │
                        Database              Distributed          AI
                           │                      │                 │
                        Indexes              Events/State          Tensor
                           │                      │               Embedding
                      B+Tree/LSM              CRDT/CQRS           Vector
                           │                      │                 │
                           └──────────────────────┼─────────────────┘
                                                  │
                                                 RAG
                                                  │
                                  Document → Chunk → Embedding
                                                  │
                                           Retrieval → Rerank
                                                  │
                                                Agent
                                                  │
                                      Message → Tool → State
                                                  │
                                               Memory
```

### مسیر مفهومی کامل بعد از چهار درس

```text
Data
 ↓
Data Type
 ↓
Data Structure
 ↓
Algorithm
 ↓
Complexity
 ↓
Type System
 ↓
Memory Model
 ↓
Binary Representation
 ↓
Encoding
 ↓
Cache / Performance
 ↓
Database
 ↓
Index
 ↓
Concurrency
 ↓
Distributed Data
 ↓
Tensor
 ↓
Embedding
 ↓
Vector Index
 ↓
RAG
 ↓
Agent State
 ↓
Memory
```

## نتیجه

بعد از چهار درس، این مباحث در مجموع هسته دانشی بسیار مهمی برای ورود حرفه‌ای به **Software Engineering، Backend، Systems، Database، AI/LLM، RAG و Agentic AI** تشکیل می‌دهند.
