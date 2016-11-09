---
layout:     post
title:      Algorithms: Hash
keywords:   Hash
category:   Algorithms 
description: Hash Theory
tags:		[hash, algorithms]
---
Hash Basic Knowledge (some from geeksforgeeks)

Hash

1.	Suppose we want to design a system for storing employee records keyed using phone numbers. And we want following queries to be performed efficiently:

Insert a phone number and corresponding information.

Search a phone number and fetch the information.

Delete a phone number and related information.

2.	We can think of using the following data structures to maintain information about different phone numbers.

Array of phone numbers and records.

Linked List of phone numbers and records.

Balanced binary search tree with phone numbers as keys.

Direct Access Table.

3.	For arrays and linked lists, we need to search in a linear fashion, which can be costly in practice. If we use arrays and keep the data sorted, then a phone number can be searched in O(Logn) time using Binary Search, but insert and delete operations become costly as we have to maintain sorted order.

4.	With balanced binary search tree, we get moderate search, insert and delete times. All of these operations can be guaranteed to be in O(Logn) time.

5.	Hash Function: A function that converts a given big phone number to a small practical integer value. The mapped integer value is used as an index in hash table. In simple terms, a hash function maps a big number or string to a small integer that can be used as index in hash table.
A good hash function should have following properties

1) Efficiently computable.

2) Should uniformly distribute the keys (Each table position equally likely for each key)

6.	Hash Table: An array that stores pointers to records corresponding to a given phone number. An entry in hash table is NIL if no existing phone number has hash function value equal to the index for the entry.

7.	Collision Handling: Since a hash function gets us a small number for a big key, there is possibility that two keys result in same value. The situation where a newly inserted key maps to an already occupied slot in hash table is called collision and must be handled using some collision handling technique. Following are the ways to handle collisions:

8.	Chaining:The idea is to make each cell of hash table point to a linked list of records that have same hash function value. Chaining is simple, but requires additional memory outside the table.

9.	Open Addressing: In open addressing, all elements are stored in the hash table itself. Each table entry contains either a record or NIL. When searching for an element, we one by one examine table slots until the desired element is found or it is clear that the element is not in the table.


散列表（Hash table，也叫哈希表），是根据关键码值(Key value)而直接进行访问的数据结构。也就是说，它通过把关键码值映射到表中一个位置来访问记录，以加快查找的速度。这个映射函数叫做散列函数，存放记录的数组叫做散列表。
1）直接定址法
取关键字或者关键字的某个线性函数值为哈希地址。
2）数字分析法
3）平方取中法
取关键字平方后的中间几位为哈希地址。
4）折叠法
将关键字分割成位数相同的几部分（最后一部分的位数可以不通），然后取这几部分的叠加和（舍去进位）作为哈希地址。
5）取余数法
取关键字被某个不大于哈希表表长(HASH_TABLE_LENGTH)的数p除后所得的余数作为哈希地址。
H(key) = key % p          (其中p小于或者等于哈希表表长HASH_TABLE_LENGTH）
6）随机数法
取关键字的随机函数值作为它的哈希地址。

那么确定了哈希函数之后，就要解决哈希冲突的问题，常用的方法如下：
1）开放定址法
Hi = (H(key) + di) % M                            i = 1, 2, 3,..., k ( k <= M-1 )
其中：H(key)为哈希函数；M为哈希表表长；di为增量序列；di可能有下列三种取法：
a 线性探测再散列：di = 1, 2, 3, ..., M-1
b 二次探测再散列：di = (+,-)k^2，(k <= M/2)
c 随机探测再散列：di为随机数序列
2）再哈希法
3）链地址法
4）建立一个公共溢出区


java中的hashmap是如何实现的
HashMap实际上是一个“链表散列”的数据结构，即数组和链表的结合体。我们可以理解为“链表的数组”

腾讯面试题：
已知一个线性表(38，25，74，63，52，48)，采用的散列函数为H(Key)=Key%7，将元素散列到表长为7的哈希表中存储。若采用线性探测的开放定址法解决冲突，则在该散列表上进行等概率成功查找的平均查找长度为 ____ ；
若利用拉链法解决冲突，则在该散列表上进行等概率成功查找的平均查找长度为 ____
若利用拉链法解决冲突，则在该散列表上进行等概率成功查找的平均查找长度为 ____

百度：
搜索引擎会通过日志文件把用户每次检索使用的所有检索串都记录下来，每个查询串的长度为1-255字节。假设目前有一千万个记录（这些查询串的重复度比较高，虽然总数是1千万，但如果除去重复后，不超过3百万个。一个查询串的重复度越高，说明查询它的用户越多，也就是越热门。），请你统计最热门的10个查询串，要求使用的内存不能超过1G。

即，此问题的解决分为以下两个步骤：
　　第一步：Query统计
　　Query统计有以下俩个方法，可供选择：
　　1、直接排序法
　　首先我们最先想到的的算法就是排序了，首先对这个日志里面的所有Query都进行排序，然后再遍历排好序的Query，统计每个Query出现的次数了。
　　但是题目中有明确要求，那就是内存不能超过1G，一千万条记录，每条记录是255Byte，很显然要占据2.375G内存，这个条件就不满足要求了
让我们回忆一下数据结构课程上的内容，当数据量比较大而且内存无法装下的时候，我们可以采用外排序的方法来进行排序，这里我们可以采用归并排序，因为归并排序有一个比较好的时间复杂度O(nlogn)。
　　排完序之后我们再对已经有序的Query文件进行遍历，统计每个Query出现的次数，再次写入文件中。
　　综合分析一下，排序的时间复杂度是O(nlogn)，而遍历的时间复杂度是O(n)，因此该算法的总体时间复杂度就是O(n+nlogn)=O(nlogn)。
2. hash table
因为Hash Table的查询速度非常的快，几乎是O(1)的时间复杂度。
　　那么，我们的算法就有了：维护一个Key为Query字串，Value为该Query出现次数的HashTable，每次读取一个Query，如果该字串不在Table中，那么加入该字串，并且将Value值设为1；如果该字串在Table中，那么将该字串的计数加一即可。最终我们在O(n)的时间复杂度内完成了对该海量数据的处理。
　　本方法相比算法1：在时间复杂度上提高了一个数量级，为O(n)，但不仅仅是时间复杂度上的优化，该方法只需要IO数据文件一次，而算法1的IO次数较多的，因此该算法2比算法1在工程上有更好的可操作性。
　　第二步：找出Top 10
　　算法一：普通排序
    我想对于排序算法大家都已经不陌生了，这里不在赘述，我们要注意的是排序算法的时间复杂度是O(nlogn)，在本题目中，三百万条记录，用1G内存是可以存下的。
　　算法二：部分排序
　　题目要求是求出Top 10，因此我们没有必要对所有的Query都进行排序，我们只需要维护一个10个大小的数组，初始化放入10个Query，按照每个Query的统计次数由大到小排序，然后遍历这300万条记录，每读一条记录就和数组最后一个Query对比，如果小于这个Query，那么继续遍历，否则，将数组中最后一条数据淘汰，加入当前的Query。最后当所有的数据都遍历完毕之后，那么这个数组中的10个Query便是我们要找的Top10了。
　　不难分析出，这样，算法的最坏时间复杂度是N*K， 其中K是指top多少。
　　算法三：堆
　　在算法二中，我们已经将时间复杂度由NlogN优化到NK，不得不说这是一个比较大的改进了，可是有没有更好的办法呢？
　　分析一下，在算法二中，每次比较完成之后，需要的操作复杂度都是K，因为要把元素插入到一个线性表之中，而且采用的是顺序比较。这里我们注意一下，该数组是有序的，一次我们每次查找的时候可以采用二分的方法查找，这样操作的复杂度就降到了logK，可是，随之而来的问题就是数据移动，因为移动数据次数增多了。不过，这个算法还是比算法二有了改进。

假定有k个关键字互为同义词,若用线性探测法把这k个关键字存入哈希表中,至少要进行多少次探测?()
本人觉得此题无答案，解释如下：
有k个关键字相同，对第一个进行哈希值计算时对应位置没有存放数，直接插入，无需探测。
对第二个数插入时探测次数为1，
以此类推
第k个插入时探测数为k-1.
所以
1+2+……+k-1=k*（k-1）/2才正确。

装填因子增大，意味着哈希表的空间利用率在增大。
开哈希和闭哈希主要的区别在于，随着哈希表的密集度提高，使用闭哈希时，不仅会与相同哈希值的元素发生冲突，还容易与不同哈希值的元素发生冲突；而开哈希则不受哈希表疏密与否的影响，始终只会与相同哈希值的元素冲突而已。所以在密集度变大的哈希表中查找时，显然开哈希的平均搜索长度不会增长。

散列的基本思想是以结点的关键码作为自变量，通过散列函数将其映射到记录的存储地址。有时不同的关键码值经过同一散列函数计算后形成相同的存储地址，产生碰撞现象。由于处理碰撞的代价较大，应尽量避免。这就要求散列函数在作用于各记录关键码后的取值能同等均匀在存储空间上。


哈希法的平均查找长度不随表中结点数目的增加而增加,而是随负载因子的增大而增大()

采用开放定址法处理散列表的冲突时，其平均查找长度？
高于链接法处理冲突
参考willfcareer：http://blog.csdn.net/willfcareer/article/details/6687117
与开放定址法相比，拉链法其中优点有： 
1、拉链法处理冲突简单，且无堆积现象，即非同义词决不会发生冲突，因此平均查找长度较短；
2、由于拉链法中各链表上的结点空间是动态申请的，故它更适合于造表前无法确定表长的情况。

基于哈希的索引和基于树的索引有什么区别?
1、hash索引仅满足“=”、“IN”和“<=>”查询，不能使用范围查询
因为hash索引比较的是经常hash运算之后的hash值，因此只能进行等值的过滤，不能基于范围的查找，因为经过hash算法处理后的hash值的大小关系，并不能保证与处理前的hash大小关系对应。
2、hash索引无法被用来进行数据的排序操作
由于hash索引中存放的都是经过hash计算之后的值，而hash值的大小关系不一定与hash计算之前的值一样，所以数据库无法利用hash索引中的值进行排序操作。
3、对于组合索引，Hash 索引在计算 Hash 值的时候是组合索引键合并后再一起计算 Hash 值，而不是单独计算 Hash 值，所以通过组合索引的前面一个或几个索引键进行查询的时候，Hash 索引也无法被利用。
4、Hash 索引遇到大量Hash值相等的情况后性能并不一定就会比B-Tree索引高。
对于选择性比较低的索引键，如果创建 Hash 索引，那么将会存在大量记录指针信息存于同一个 Hash 值相关联。这样要定位某一条记录时就会非常麻烦，会浪费多次表数据的访问，而造成整体性能低下。

既希望较快的查找又便于线性表动态变化的查找方法是()
哈希法查找

拉链法解决冲突时，需要使用指针，指示下一个元素的存储位置

哈希表装填因子定义为：α= 填入表中的元素个数 / 哈希表的长度
α是哈希表装满程度的标志因子。由于表长是定值，α与“填入表中的元素个数”成正比，所以，α越大，填入表中的元素较多，产生冲突的可能性就越大；α越小，填入表中的元素较少，产生冲突的可能性就越小。

采用开址定址法解决冲突的哈希查找中,发生集聚的原因主要是()
解决冲突的算法选择不好

冲突处理的好，那么平均查找长度就小，否则就大。

对于一个线性表既要求能够进行较快速地的插入和删除,又要求存储结构能反映数据之间的逻辑关系,则应该用()
链式存储方式

有序表中所有元素以递增或递减方式排列，对数据之间的关系进行了描述，是一种逻辑结构。
顺序表是指用一组地址连续的存储单元依次存储数据元素的线性结构。
哈希表 用散列法存储的线性表叫散列表。
单链表 用一组地址任意的存储单元存放线性表中的数据元素，均只是一种存取结构，不是逻辑结构。

现有一完全的P2P共享协议，每次两个节点通讯后都能获取对方已经获取的全部信息，现在使得系统中每个节点都知道所有节点的文件信息，共17个节点，假设只能通过多次两个对等节点之间通讯的方式，则最少需要（）次通讯
30

深度优先搜索要借助栈；
广度优先搜索要借助队列；

数组的插入和删除可以 O(1)

有B+Tree/Hash_Map/STL Map三种数据结构。对于内存中数据，查找性能较好的数据结构是（Hash_Map），对于磁盘中数据，查找性能较好的数据结构是（B+Tree）。

拉链法的缺点是：指针需要额外的空间，故当结点规模较小时，开放定址法较为节省空间
在用拉链法构造的散列表中，删除结点的操作易于实现
拉链法处理冲突简单，且无堆积现象，即非同义词决不会发生冲突，因此平均查找长度较短

Hash，一般翻译做“散列”，也有直接音译为“哈希”的，就是把任意长度的输入（又叫做预映射， pre-image），通过散列算法，变换成固定长度的输出，该输出就是散列值。
构造方法
散列函数能使对一个数据序列的访问过程更加迅速有效，通过散列函数，数据元素将被更快地定位。
（详细构造方法可以参考hash函数中的【哈希表的构造方法】）
1．直接寻址法：取关键字或关键字的某个线性函数值为散列地址。即H(key)=key或H(key) = a·key + b，其中a和b为常数（这种散列函数叫做自身函数）
2． 数字分析法
3． 平方取中法
4． 折叠法
5． 随机数法
常用HASH函数
直接取余法：f(x):= x mod maxM ; maxM一般是不太接近 2^t 的一个质数。
乘法取整法：f(x):=trunc((x/maxX)*maxlongit) mod maxM，主要用于实数。
平方取中法：f(x):=(x*x div 1000 ) mod 1000000); 平方后取中间的，每位包含信息比较多。

已知一段文本有1382个字符，使用了1382个字节进行存储，这段文本全部是由a、b、c、d、e这5个字符组成，a出现了354次，b出现了483次，c出现了227次，d出现了96次，e出现了232次，对这5个字符使用哈夫曼（Huffman）算法进行编码，则以下哪些说法正确（）
使用哈夫曼算法编码后，用编码值来存储这段文本将花费最少的存储空间
A正确，Huffman树就是求最优解。可以有多套方案，但最终每套方案生成的编码长度都相同且都是最优解。
使用哈夫曼算法进行编码，a、b、c、d、e这5个字符对应的编码值是唯一确定的
B错误，我们可以将左子树定为1右子树定为0也可以反之，不同的方案获得的编码值是不同的，但每个字符的编码长度是固定的。
使用哈夫曼算法进行编码，a、b、c、d、e这5个字符对应的编码值可以有多套，但每个字符编码的位（bit）数是确定的
C正确，不同的方案影响的只是通向节点的路径为0还是1，而不会影响Huffman树的层次结构
b这个字符的哈夫曼编码值位数应该最短，d这个字符的哈夫曼编码值位数应该最长
D正确，生成了Huffman树之后，我们就能看到，出现频率越高的节点越靠近根，深度越小即编码值尾数越短；出现频率越低的节点越远离根，深度越大即编码位数越长。

已知某个哈希表的n个关键字具有相同的哈希值，如果使用二次探测再散列法将这n个关键字存入哈希表，至少要进行____次探测。
二次探测再散列 
{   D = H(key);  
    ND = (D+di)%m;　　di 取 1*1,-1*1,2*2,-2*2,……,K*K,-K*K 　(K≤m/2)
　　 值得提醒的是，对利用开放地址法查了冲突所产生的哈希表中删除一个元素，不能简单地直接删除，因为这样将截断其它具有相同哈希地址的元素的查找地址，所以应设定一个特殊的标志以表明该元素已被删除。


