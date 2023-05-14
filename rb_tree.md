# rb_tree

红黑树是**平衡二叉搜索树**中的一种，AVL树也是一种平衡二叉搜索树。平衡二叉搜索树的特性：排列规则有利于插找和插入，并保持适度平衡（无任何节点过深）。

红黑树提供遍历操作及iterators，按正常规则(++iter)遍历能获得**排序状态**。

**不应**使用红黑树的迭代器改变元素值（因为元素有其严谨的排列规则），但编程层面**并未阻止此事**。这么设计是正确的，因为红黑树作为set和map的底层，map允许元素data被改变，只有元素的key是不可以改变的。

> 侯捷的课程中，**key和data合成value**：键值对中键是key，值是data，合成的键值对叫value。

红黑树提供两种insertion操作：insert_unique()和insert_equal()。前者表示节点的key一定在整个tree中独一无二，否则安插失败；后者表示节点的key可以重复。

Gnu2.9版本红黑树底层实现，模板类，有***5个模板参数***：

![image](https://github.com/babyblueling/MyLeetcode/assets/132556492/d632cdf1-3dd4-4371-a7bd-be27c8dad295)

第3个模板参数KeyOfValue表示怎样从Value中取出Key。

一颗红黑树的大小：size_type（也就是unsigned int）占4个字节，header是个指针占4个字节，key_compare是仿函数（函数对象）理论上是0字节，但在实现上对于大小为0的类，创造出的对象大小永远是1。所以一个红黑树的大小为9个字节。又由于内存对齐，红黑树的大小将被调整到12。

一个很好的**例子**：

![image](https://github.com/babyblueling/MyLeetcode/assets/132556492/74ce5c0b-2e0b-4026-92a0-0730a38bd5a9)

直接用rb_tree模板类，传入五个模板参数，实现一棵红黑树。对于其中的第三个参数`identity<int>`，只是在Gnu中独有，在VC中没有（旧版没有，新版不清楚）。identity继承自父类unary_function，但unary_function中没有任何函数和属性，继承它是为了**adaptable**。同理，less继承binary_function也是为了**adaptable**。

在Gnu4.9版以后的容器_Rb_tree实现采用了**handle-and-body**的手法，为了XXX目标，会在类中有一个指针或东西（图中的`_Rb_tree_impl<...>`）来表示它的实现手法。其中的handle就是`_Rb_tree<...>`，body就是`_Rb_tree_impl<...>`。如下图：

![image](https://github.com/babyblueling/MyLeetcode/assets/132556492/f447ce61-849f-4bde-9233-d237dc136b68)

---

红黑树必须满足下面几条性质：

- **每个节点不是红色就是黑色**
- **根节点为黑色**
- **红色节点的子节点必须为黑**
- **任一节点至NULL节点(空节点)的任何路径，所含黑色节点数必须相同**
- **NULL节点(空节点)都是黑色**

> NULL节点是指最底层的空节点（外部节点），也叫叶子节点

根据以上规则，**新增节点必须为红，且新增节点的父节点必须为黑，红色节点的子节点和父节点都为黑**。当新节点根据二叉搜索树的规则到达其插入点，却未能符合上述条件时，就必须调整颜色并旋转树形。

当插入节点却不能满足*新增节点必须为红，且新增节点的父节点必须为黑*时，分为以下三种情况（假设新增节点X，其父节点P，其祖父节点G，伯父节点S，曾祖父节点GG）：

1. S为黑且X为外侧插入。先对P、G进行一次单旋转，再改变P、G的颜色即可。
2. S为黑且X为内侧插入。先对P、X进行一次单旋转，再改变G、X的颜色，再将结果对G进行一次单旋转。
3. S为红且X为外侧插入。先对P、G做一次单旋转，再改变X的颜色。如果GG为黑，结束；GG为红，持续往上做，直到不再有两个连续的红色节点。

为避免上面情况三中的父子节点皆为红向上层结构发展，可以采用一个**由上往下**的程序：假设新增节点为A，沿着A的路径，只要看到有某节点X的两个子节点都为红，就把X改为红色，并把两个子节点改为黑色。如果还出现两个红色节点相连的情况，就执行情况1或情况2。

之后的插入要么直接插入，要么插入后再一次旋转即可。

---

红黑树保证最长路径不超过最短路径的两倍，因而近似平衡。红黑树是一种近似平衡的二叉树（说它近似平衡是因为它并没有像AVL树平衡条件的概念，只是靠着上面五条性质来维持一种接近平衡的结构）。红黑树的**查找，插入和删除操作，时间复杂度都是O(logN)**。
