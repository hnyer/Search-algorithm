
###[查阅更多](http://note.youdao.com/share/?id=867201174273b78841581d48ff796d11&type=note) 
```java
/**
 * 顺序查找
 * @param sz
 * @param key
 * @return 下标
 */
public static int SequenceSearch(int[] sz, int key) {
    for (int i = 0; i < sz.length; i++) {
        if (sz[i] == key) {
            return i;
        }
    }
    return -1;
}

 
/**
 * 折半查找、二分查找 。前提：数组是 按升序排列 的。
 * @param sz
 * @param key
 * @return 下标
 */
public static int BinarySearch(int[] sz, int key) {
    int low = 0;
    int high = sz.length - 1;
    while (low <= high) {
        int middle = (low + high) / 2;
        if (sz[middle] == key) {
            return middle;
        } else if (sz[middle] > key) {
            high = middle - 1;
        } else {
            low = middle + 1;
        }
    }
    return -1;
}
/**
 * 哈希查找。通过计算数据元素的存储地址进行查找。
 * 哈希查找的操作步骤：⑴用给定的哈希函数构造哈希表⑵根据选择的冲突处理方法解决地址冲突⑶在哈希表的基础上执行哈希查找。 
 * 建立哈希表操作步骤：
 * ①取数据元素的关键字key，计算其哈希 函数值。若该地址对应的存储 空间还没有被占用，则将该元素存入；否则执行step2解决冲突。
 * ②根据选择的冲突处理方法，计算关键字 key的下一个存储地址。若下一个存储地 址仍被占用，则继续执行step2，直到找 到能用的存储地址为止。
 * @param sz
 * @param key
 */
public static int HashSearch(int[] sz, int key) {
    int mod = 15;// 大于或等于数组长度
    int[] hash = new int[mod];
    BuildHash(sz, hash);
    int hashAddress = key % mod;
    while (hash[hashAddress] != 0 && hash[hashAddress] != key) {
        hashAddress = (++hashAddress) % mod;
    }
    if (hash[hashAddress] == 0) {
        return -1;
    }
    return hashAddress;
}
 
public static void BuildHash(int[] sz, int[] hash) {
    int mod = hash.length;
    for (int i = 0; i < sz.length; i++) {
        int hashAddress = sz[i] % mod;
        while (hash[hashAddress] != 0) {// 如果对应的地址已经有值，则使用开放地址法解决
            hashAddress = (++hashAddress) % mod;
        }
        hash[hashAddress] = sz[i];
    }
}
/**
 * 二叉树查找。二叉排序树左节点的所有节点都比根节点小，右节点的所有节点都比根节点大。
 * @param sz
 * @param key
 * @return
 */
public static int BinaryTreeSearch(int[] sz, int key) {
    BinaryTree bt = CreateBinaryTree(sz);
    return find(bt, key);
}
 
public static BinaryTree CreateBinaryTree(int[] sz) {
    BinaryTree bt = new BinaryTree(sz[0], 0);
    for (int i = 1; i < sz.length; i++) {
        InsertNode(bt, sz[i], i);
    }
    return bt;
}
 
private static void InsertNode(BinaryTree bt, int key, int index) {
    BinaryTree parent = null;
    while (bt != null) {
        parent = bt;
        if (bt.data > key) {
            bt = bt.left;
        } else {
            bt = bt.right;
        }
    }
 
    bt = new BinaryTree(key, index);
    bt.setParent(parent);
}
 
public static int find(BinaryTree bt, int key) {
    while (bt != null) {
        if (bt.data == key) {
            return bt.index;
        } else if (bt.data > key) {
            bt = bt.left;
        } else {
            bt = bt.right;
        }
    }
    return -1;
 
}
 
public static void LDR_BT(BinaryTree bt) {
    if (bt != null) {
        LDR_BT(bt.left);
        System.out.print(bt.data + " ");
        LDR_BT(bt.right);
    }
}
 
static class BinaryTree {
    int data;
    int index;
    BinaryTree left;
    BinaryTree right;
 
    public BinaryTree(int data, int index, BinaryTree left, BinaryTree right) {
        this.data = data;
        this.index = index;
        this.left = left;
        this.right = right;
    }
 
    public BinaryTree(int data, int index) {
        this.data = data;
        this.index = index;
    }
 
    public void setParent(BinaryTree parent) {
        if (this.data < parent.data) {
            parent.left = this;
        } else {
            parent.right = this;
        }
    }
 
}


```
