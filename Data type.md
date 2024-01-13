
## Data Types
### what data type does JavaScript have and how do they differ?
JavaScript has eight data types:  Undefined,Null,Boolean,Number,String,Object, Symol,and BigInt.
Where Symbol and BigInt are new data types in ES6:

- Symbol represents a unique and immutable data type created to resolve possible global variable conflicts.
- BigInt is numeric type  of data that can represent intergers in any precision format. BigInti can be used to safely store and manipulate large intergers, even if the number is outside the range of safe intergers that number can represent.
### These data can be divided into raw data types and referenece data types:

- stack: raw data type（ Undefined、Null、Boolean、Number、String ）
- heap:Reference data types(  Object arrays and functions)

### The diffence between the two types is the storage location:

- The original data types is a simple data segment directly stored in the stack, which  occupies a  small space and have a fixed size, and belongs to the frequently used data, so it's  stored in the stack;
- An Object whose data type is stored in the heap,occupying a large space and hanving an unfixed size. If stored in the stack, it will affect the performance of the program. The reference data types stored a pointer on the stack that points to the starting address of entity in the heap. When the interpreter looks for a reference value, it first retrieves its address in the stack  and retrieves the entity from the heap.
### The concepts of heap and stack exist in data structueres and operating system memory, where:
#### In data structure

-  the access mode of  the data in the stack  is first in , last out.
- the heap is priority queue that is stored by priority , which can be specified by size.

#### In operating system, memory is divided into stack and heap areas:

- The stack memory is automatically allocated and released by the compiler to store that parameter values of functions and the values of local varaiables. It operates like a  stack in data structure.
- Heap area memory is usually freed by the developer allocation , and if the developer doesn't free it, it may be reclaimed by the garbage collection mechanism at the end of the program.

