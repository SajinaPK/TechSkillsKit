# JIT Compiler
  
  
A system implementing a JIT compiler typically continuously analyses the code being executed and identifies parts of the code where the speedup gained from compilation or recompilation would outweigh the overhead of compiling that code.  
  
JIT compilation is a combination of the two traditional approaches to translation to machine code—ahead-of-time compilation (AOT), and interpretation—and combines some advantages and drawbacks of both.[2] Roughly, JIT compilation combines the speed of compiled code with the flexibility of interpretation, with the overhead of an interpreter and the additional overhead of compiling and linking (not just interpreting). JIT compilation is a form of dynamic compilation, and allows adaptive optimization such as dynamic recompilation and microarchitecture-specific speedups.  
  
  
1. The compilation can be optimized to the targeted CPU and the operating system model where the application runs. For example, JIT can choose SSE2 vector CPU instructions when it detects that the CPU supports them. To obtain this level of optimization specificity with a static compiler, one must either compile a binary for each intended platform/architecture, or else include multiple versions of portions of the code within a single binary.  
2. The system is able to collect statistics about how the program is actually running in the environment it is in, and it can rearrange and recompile for optimum performance. However, some static compilers can also take profile information as input.  
3. The system can do global code optimizations (e.g. inlining of library functions) without losing the advantages of dynamic linking and without the overheads inherent to static compilers and linkers. Specifically, when doing global inline substitutions, a static compilation process may need run-time checks and ensure that a virtual call would occur if the actual class of the object overrides the inlined method, and boundary condition checks on array accesses may need to be processed within loops. With just-in-time compilation in many cases this processing can be moved out of loops, often giving large increases of speed.
4. Although this is possible with statically compiled garbage collected languages, a bytecode system can more easily rearrange executed code for better cache utilization.
  
  
The Just-In-Time (JIT) compiler is a component of the runtime environment that improves the performance of Java™ applications by compiling bytecodes to native machine code at run time.

Java programs consists of classes, which contain platform-neutral bytecodes that can be interpreted by a JVM on many different computer architectures. At run time, the JVM loads the class files, determines the semantics of each individual bytecode, and performs the appropriate computation. The additional processor and memory usage during interpretation means that a Java application performs more slowly than a native application. The JIT compiler helps improve the performance of Java programs by compiling bytecodes into native machine code at run time.

The JIT compiler is enabled by default. When a method has been compiled, the JVM calls the compiled code of that method directly instead of interpreting it. Theoretically, if compilation did not require processor time and memory usage, compiling every method could allow the speed of the Java program to approach that of a native application.

JIT compilation does require processor time and memory usage. When the JVM first starts up, thousands of methods are called. Compiling all of these methods can significantly affect startup time, even if the program eventually achieves very good peak performance.

In practice, methods are not compiled the first time they are called. For each method, the JVM maintains an invocation count, which starts at a predefined compilation threshold value and is decremented every time the method is called. When the invocation count reaches zero, a just-in-time compilation for the method is triggered. Therefore, often-used methods are compiled soon after the JVM has started, and less-used methods are compiled much later, or not at all. The JIT compilation threshold helps the JVM start quickly and still have improved performance. The threshold value was selected to obtain an optimal balance between startup times and long-term performance.

The JIT compiler can compile a method at different optimization levels: cold, warm, hot, veryHot, or scorching (see optlevel in -Xjit). Higher optimization levels are expected to provide better performance, but they also have a higher compilation cost in terms of CPU and memory. The initial or default optimization level for a method is warm, but sometimes the JIT heuristics downgrade the optimization level to cold to improve startup time.

A method can be re-compiled to a higher optimization level through different mechanisms. One of these mechanisms is sampling: the JIT compiler maintains a dedicated sampling thread which wakes up periodically and determines which Java methods appear more often at the top of the stack. Such methods are deemed to be more important for performance, and they are candidates for being re-optimized at the higher levels of hot, veryHot, or scorching.

You can disable the JIT compiler, in which case the entire Java program will be interpreted. Disabling the JIT compiler is not recommended except to diagnose or work around JIT compilation problems.

How the JIT compiler optimizes code

To help the JIT compiler analyze the method, its bytecodes are first reformulated in an internal representation called trees, which resembles machine code more closely than bytecodes. Analysis and optimizations are then performed on the trees of the method. At the end, the trees are translated into native code.

The compilation consists of the following phases. All phases except native code generation are cross-platform code.

Phase 1 - inlining
Inlining is the process by which the trees of smaller methods are merged, or "inlined", into the trees of their callers. This speeds up frequently executed method calls. Two inlining algorithms with different levels of aggressiveness are used, depending on the current optimization level. Optimizations performed in this phase include:
* 		Trivial inlining
* 		Call graph inlining
* 		Tail recursion elimination
* 		Virtual call guard optimizations

Phase 2 - local optimizations
Local optimizations analyze and improve a small section of the code at a time. Many local optimizations implement tried and tested techniques used in classic static compilers. The optimizations include:
* 		Local data flow analyses and optimizations
* 		Register usage optimization
* 		Simplifications of Java idioms
These techniques are applied repeatedly, especially after global optimizations, which might have pointed out more opportunities for improvement.

Phase 3 - control flow optimizations
Control flow optimizations analyze the flow of control inside a method (or specific sections of it) and rearrange code paths to improve their efficiency. The optimizations are:
* 		Code reordering, splitting, and removal
* 		Loop reduction and inversion
* 		Loop striding and loop-invariant code motion
* 		Loop unrolling and peeling
* 		Loop versioning and specialization
* 		Exception-directed optimization
* 		Switch analysis

Phase 4 - global optimizations
Global optimizations work on the entire method at once. They are more "expensive", requiring larger amounts of compilation time, but can provide a great increase in performance. The optimizations are:
* 		Global data flow analyses and optimizations
* 		Partial redundancy elimination
* 		Escape analysis
* 		GC and memory allocation optimizations
* 		Synchronization optimizations

Phase 5 - native code generation
Native code generation processes vary, depending on the platform architecture. Generally, during this phase of the compilation, the trees of a method are translated into machine code instructions; some small optimizations are performed according to architecture characteristics. The compiled code is placed into a part of the JVM process space called the code cache; the location of the method in the code cache is recorded, so that future calls to it will call the compiled code. At any given time, the JVM process consists of the JVM executable files and a set of JIT-compiled code that is linked dynamically to the bytecode interpreter in the JVM.


How much memory does the code cache consume?
The JIT compiler uses memory intelligently. When the code cache is initialized, it uses relatively little memory. As more methods are compiled into native code, the code cache grows dynamically to accommodate the needs of the program. Space that is previously occupied by discarded or recompiled methods is reclaimed and reused. When the size of the code cache reaches a predefined maximum limit, it stops growing. The JIT compiler then stops compiling methods to avoid exhausting the system memory and affecting the stability of the application or the operating system.


A compiler in 3 parts:

Lexing, Parsing, Semantic Analysis (Front -end).  ——>  Optimization ( Middle-end).   ———>.    Code generation (backend)


Lexing -  breakup input string into tokens
Parsing - generate Abstract Syntax Tree (AST) from tokens and grammar
Semantic Analysis - Analyze AST to understand the code and generate IL

in JIT source is the bytecode, we generate the IL from bytecode.

Intermediate Language (IL)
	Bytecodes are not good for analysis. So translate bytecodes to IL or IR (representation). This stage is ILGen. In our JIT its called trees.
	A node represents an expression. A node’s children represent operands.
Code Generation
	Translate IL to machine code. Done in phases. Simple (peephole) optimization is done. Selects instrucitons. Assign registers. Encode instructions in binary.


Example:


a += b;  
a = (a-b)*2;  

iload a  
iload b  
iadd  
istore a  
iload a  
iload b  
isub  
bipush 2  
imul  
istore a  

A day in the life of a method:   ILGen. <— VM. <—          Binary encoding  
								|						        |  
							    Optimizer -> tree evaluation -> register assignment  


