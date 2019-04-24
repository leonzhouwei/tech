# JDK 8
## List
| 名称 | 线程安全 | 数据结构 | 允许 null | 默认初始容量 | 扩容策略 | 备注 |
| --- | :-----: | :-----: | :------: | ---------: | ------: | --- |
| ArrayList | 不安全 | 数组 | 允许 | 10 | 1.5 * old | |
| LinkedList | 不安全 | 双链表 | 允许 | N/A | N/A | 作为 List 使用时，最好换用低复杂度的 [TreeList](https://commons.apache.org/proper/commons-collections/apidocs/org/apache/commons/collections4/list/TreeList.html) |
| CopyOnWriteArrayList | 安全 | 数组 + 快照 | 允许 | 0 | +1 | |

## Map
| 名称 | 线程安全 | 数据结构 | 允许 null key | 允许 null value | 有序性 | 默认初始容量 | 扩容策略 | 备注 |
| --- | :-----: | ------- | :----------: | :------------: | :----: | ---------: | ------: | --- |
| HashMap | 不安全 | 多个(单链表或者红黑树)组成的数组 | 允许 | 允许 | 无序 | 16 | 2 * old |
| IdentityHashMap | 不安全 | 数组 | 允许 | 允许 | 无序 | 32 | ? |
| LinkedHashMap | 不安全 | 多个双链表组成的数组 | 允许 | 允许 | 有序(access-order 或者 insertion-order) | 16 | 2 * old |
| TreeMap | 不安全 | 红黑树 | 不允许 | 允许 | 有序 | N/A | N/A |
| EnumMap | 不安全 | 数组 | 不允许 | 允许 | 有序 | N/A | N/A |
| ConcurrentHashMap | 安全 | 多个(单链表或者红黑树)组成的数组 | 不允许 | 不允许 | 无序 | 16 | 2 * old |
| ConcurrentSkipListMap | 安全 | 跳表 | 不允许 | 不允许 | 有序 | N/A | ? |

## Set
| 名称 | 线程安全 | 数据结构 | 允许 null | 有序性 | 备注 |
| --- | :-----: | ------- | :------: | :---: | :--: |
| HashSet | 不安全 | HashMap | 允许 | 无序 | |
| LinkedHashSet | 不安全 | LinkedHashMap | 允许 | 有序(insertion-order) |
| TreeSet | 不安全 | TreeMap | 不允许 | 有序 |
| ConcurrentSkipListSet | 安全 | ConcurrentSkipListMap | 不允许 | 有序 |
| CopyOnWriteArraySet | 安全 | CopyOnWriteArrayList | 允许 | 无序 |

## Queue
| 名称 | 线程安全 | 数据结构 | 允许 null | 默认初始容量 | 扩容策略 | 备注 |
| --- | :-----: | :-----: | :------: | ---------: | ------: | --- |
| ArrayDeque | 不安全 | 数组 | 不允许 | 16 | 2 * old | head 从数组的最大下标开始变小，tail 从 0 开始变大 |
| PriorityQueue | 不安全 | [平衡最小二叉堆](http://blog.csdn.net/lcore/article/details/9100073) | 不允许 | 11 | old < 64 则 2 * old; 否则 1.5 * old | 空穴, sift up，sift down |
| ConcurrentLinkedQueue | 安全 | 单链表 + CAS | 不允许 | N/A | N/A |
| ConcurrentLinkedDeque | 安全 | 双链表 + CAS | 不允许 | N/A | N/A |
| ArrayBlockingQueue | 安全 | 循环数组 | 不允许 | N/A | 定长, 不可扩容 | 1. 有 fair 选项; 2. 有一把公共的 ReentrantLock 与 notFull、notEmpty 两个 Condition 管理队列满或空时的阻塞状态 |
| LinkedBlockingQueue | 安全 | 单链表 | 不允许 | N/A | 定长或无界 | 利用链表的特征，分离了 takeLock 与 putLock 两把锁，继续用 notEmpty、notFull 管理队列满或空时的阻塞状态 |
| LinkedBlockingDeque | 安全 | 双链表 | 不允许 | N/A | 定长或无界 | 利用链表的特征，分离了 takeLock 与 putLock 两把锁，继续用 notEmpty、notFull 管理队列满或空时的阻塞状态  |
| PriorityBlockingQueue | 安全 | [平衡最小二叉堆](http://blog.csdn.net/lcore/article/details/9100073) | 不允许 | 11 | old < 64 则 2 * old; 否则 1.5 * old | 空穴, sift up，sift down |
| DelayQueue | 安全 | PriorityQueue | 不允许 | 见 PriorityQueue | 见 PriorityQueue | ScheduledThreadPoolExecutor 用了类似的结构 |
| SynchronousQueue | 安全 | N/A | 不允许 | 1 | N/A | 有 fair 选项 |
| LinkedTransferQueue | 安全 | 单链表 + CAS | 不允许 | N/A | N/A |
