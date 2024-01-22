# Memory Management



**Heap Allocation**

The process of managing memory in the VM is handled by the allocator and the garbage collector. These components operate on an area of memory that is reserved for VM processing called the Java™ heap.

The allocator assigns areas of the heap for Java objects. Objects are considered as live when they have a chain of references to them that start from root references, such as those found in thread stacks. When that reference or pointer no longer exists, the objects are considered as garbage.

The garbage collector reclaims memory by removing objects when they are no longer required.

**The allocator**

In general, allocation requires a heap lock to synchronize concurrent threads that try to access the same area of memory at the same time. When an object is allocated, the heap lock is released. If there is insufficient space to allocate the object, allocation fails, the heap lock is released, and the garbage collector is called. If GC manages to recover some space on the heap, the allocator can resume operations. If GC does not recover enough space, it returns an OutOfMemoryError exception.
Acquiring a heap lock for every allocation would be an intensive operation with an impact to performance. To get around this problem, small objects are allocated to allocation caches.


**Allocation caches**

To improve performance, allocation caches are reserved in the heap for different threads. These allocation caches are known as thread local heaps (TLH) and allow each thread to allocate memory from its cache without acquiring the heap lock. Objects are allocated from the TLH unless there is insufficient space remaining in the TLH to satisfy the request. In this situation, the allocation might proceed directly from the heap for larger objects by using a heap lock or the TLH might be refreshed for smaller objects.

If a thread allocates a lot of objects, the allocator gives that thread a larger TLH to reduce contention on the heap lock.
A TLH is predefined with an initial default size of 2 KB. On every TLH refresh, the requested size for that thread is increased by an increment (default 4 KB). The requested size can grow up to a predefined maximum (default 128 KB). If a TLH refresh fails to complete, a GC cycle is triggered.

After every GC cycle, the requested size of the TLH for each thread is reduced, sometimes by as much as 50%, to take account of threads that reduce their allocation rate and no longer need large TLHs.

For very inactive threads, the requested size can even drop below the initial value, down to the predefined minimum (512/768 bytes). For very active threads, the maximum TLH requested size might be reached before the next GC occurs.

Larger TLHs can help reduce heap lock contention, but might also reduce heap utilization and increase heap fragmentation.
The following options control the requested TLH size:
* 		-Xgc:tlhMaximumSize=<bytes>
* 		-Xgc:tlhInitialSize=<bytes>
* 		-Xgc:tlhIncrementSize=<bytes>
Typically, when the maximum TLH size is increased, you should also increase the increment proportionally, so that active threads can reach the maximum requested TLH size more quickly.

**Heap Configurations**

Depending on the memory management strategy in force, the Java heap can be configured in a number of ways. The simplest configuration consists of a single area of memory, often referred to as a flat heap. Other configurations divide the heap into different areas or regions, which might contain objects of different ages (generations) or sizes.

**Area based heaps**

The default GC policy for OpenJ9 uses a heap configuration that is divided into two main areas: the nursery area for new object allocation, and the tenure area for objects that continue to be reachable for a longer period of time. Most objects have short lifecycles and can be reclaimed by the garbage collector more quickly by focusing only on the nursery area. Global GC cycles that cause application pauses in order to clear and defragment the tenure area are less frequent.

**SOA and LOA**

All area-based heaps subdivide part of the heap into the Small Object Area (SOA) and the Large Object Area (LOA).

The allocator initially attempts to allocate objects in the SOA, regardless of size. If the allocation cannot be satisfied the following actions are possible, depending on object size:
* 		If the object is smaller than 64 KB, an allocation failure occurs, which triggers a GC action.
* 		If the object is larger than 64 KB, the allocator attempts to allocate the object in the LOA. If the allocation cannot be satisfied, an allocation failure occurs, which triggers a GC action.
* 
The GC action that is triggered by the allocation failure depends on the GC policy in force.

The overall size of the LOA is calculated when the heap is initialized, and recalculated at the end of each global GC cycle. The garbage collector can expand or contract the LOA, depending on usage, to avoid allocation failures.

You can control the size of the LOA by using the -Xloainitial, -Xloaminimum, and -Xloamaximum command line options. If the LOA is not used, the garbage collector contracts the LOA after a few cycles, down to the value of -Xloaminimum. You can also specify -Xnoloa to prevent an LOA being created.

An SOA and LOA are used by the OpenJ9 GC policies: gencon, optavgpause and optthruput. For the gencon policy, the LOA and SOA are contained within the tenure area, which is designated for ageing objects.

Region based heaps

The Java heap can also be subdivided into multiple regions. The balanced GC policy uses a heap that is divided into thousands of equal size regions in order to manage multiple generations of objects. The metronome GC policy also uses multiple regions, which are grouped by size-class to manage a singe generation of objects.

In addition to regions, the balanced and metronome policies use structures called arraylets to store large arrays in the heap.

Arraylets

A Java heap that is subdivided into regions might not be able to contain a large enough region for data arrays. This problem is solved by using arraylets. An arraylet has a spine, which contains the class pointer and size, and leaves, which contain the data associated with the array. The spine also contains arrayoids, which are pointers to the respective arraylet leaves, as shown in the following diagram.



————————————————————

**Garbage Collection**

The Garbage Collector adapts heap size to keep occupancy between 40% and 70% for the following reasons:
* 		A heap occupancy greater than 70% causes more frequent GC cycles, which can reduce performance. You can alter this behavior by setting the -Xminf option.
* 		A heap occupancy less than 40% means infrequent GC cycles. However, these cycles are longer than necessary, causing longer pause times, which can reduce performance. You can alter this behavior by setting the -Xmaxf option.


If you do not set an initial or maximum heap size, the GC expands and shrinks the heap as required. However, if you fix the heap size by using the -Xms and -Xmx options, the GC does not expand or shrink the Java™ heap. 

To optimize application performance and keep within the 40 - 70% range, the maximum heap size setting should therefore be at least 43% larger than the maximum occupancy of the application. For example, if an application has a maximum occupancy of 70 MB, a maximum heap size of 100 MB should be set as shown in the following calculation:

70 + (70 * 43/100)

Setting the minimum and maximum heap size to the same value is typically not a good idea because garbage collection is delayed until the heap is full. Therefore, the first time that the GC runs, the process can take longer. 

Also, the heap is more likely to be fragmented and require a heap compaction. Start your application with the minimum heap size that your application requires. When the GC starts up, it runs frequently and efficiently because the heap is small.

If the GC cannot find enough garbage, it runs compaction. If the GC finds enough garbage, or any of the other conditions for heap expansion are met (see Heap allocation in the OpenJ9 user documentation), the GC expands the heap.

From the earlier description, you can see that the GC compacts the heap as the needs of the application rise, so that as the heap expands, it expands with a set of compacted objects in the bottom of the original heap. This process is an efficient way to manage the heap because compaction runs on the smallest-possible heap size at the time that compaction is found to be necessary. Compaction is performed with the minimum heap sizes as the heap grows. Some evidence exists that an application's initial set of objects tends to be the key or root set, so that compacting them early frees the remainder of the heap for more short-lived objects.

Eventually, the JVM has the heap at maximum size with all long-lived objects compacted at the bottom of the heap. The compaction occurred when compaction was in its least expensive phase. The amount of processing and memory usage that is required to expand the heap is almost trivial compared to the cost of collecting and compacting a very large fragmented heap.


Consider the description of the following command-line parameters and consider applying them to fine tune the way the heap is managed:
-Xminf and -Xmaxf
Minimum and maximum free space after garbage collection.
-Xmine and -Xmaxe
Minimum and maximum expansion amount.
-Xmint and -Xmaxt
Minimum and maximum garbage collection time threshold.

Pause times are too long.

If your application uses many short-lived objects, or is transaction-based (that is, objects in the transaction do not survive beyond the transaction commit), or if the heap space is fragmented, try using the -Xgcpolicy:gencon (gencon is the default) garbage collection policy. This policy treats short-lived objects differently from long-lived objects, and can reduce pause times and heap fragmentation.

In other situations, if a reduction in throughput is acceptable, try using the -Xgcpolicy:optavgpause policy. This policy reduces the pause times and makes them more consistent when the heap occupancy rises. It does, however, reduce throughput by approximately 5%, although this value varies with different applications.
I
f pause times are unacceptable during a global garbage collection, due to a large heap size, try using -Xgcpolicy:balanced. The balanced garbage collection policy can also address frequent class unloading issues, where many class loaders are being created, but require a global collection to unload. This policy is available for 64-bit platforms and must be used with the -Xcompressedrefs option. The policy is intended for environments where heap sizes are greater than 4 GB.

Here are some useful tips:

* 		Ensure that the heap never pages; that is, the maximum heap size must be able to be contained in physical memory.
* 		Avoid finalizers. You cannot guarantee when a finalizer will run, and often they cause problems. If you do use finalizers, try to avoid allocating objects in the finalizer method. A verbose:gc trace shows whether finalizers are being called.
* 		Avoid compaction. A verbose:gc trace shows whether compaction is occurring. Compaction is usually caused by requests for large memory allocations. Analyze requests for large memory allocations and avoid them if possible. If they are large arrays, for example, try to split them into smaller arrays.



