# Algorithem
## 算法通关村第一关 LinkedList Level1 —— 双向链表
双链表与单链表相比, 每个结点增加了前驱结点`prior`的引用, 结点结构如下图所示:

![](diagram/LinkedList/dblkNode.png)

### 1. 定义双链表

双向链表包含`数据域`**`val`**(以整型为例), `前驱引用`**`prior`**, `后继引用`**`next`**. 定义如下:

```java
static class Node {
        public int val;
        public Node prior;
        public Node next;

        public Node(int x) {
            val = x;
            prior = next = null;
        }
    }
```

### 2. 双链表插入

**(1) 表头插入**<br>
在双链表表头插入结点主要分为以下三步:<br>
① `newNode.next = head` <br>
② `head.prior = newNode`<br>
③ `head = newNode`<br>

**(2) 中间插入**<br>
在双链表的中间插入新结点的思路与单链表的插入相同, 首先遍历双链表, 找到要插入位置`position`的前一个结点 `pNode`, `pNode`为新结点`newNode`的前驱, `pNode.next`为`newNode`的后继. 一个可行步骤如下:<br>
① `newNode.next = pNode.next`<br>
② `pNode.next.prior = newNode`<br>
③ `newNode.prior = pNode`<br>
④ `pNode.next = newNode`<br>
双向链表的中间插入操作顺序不唯一, 但在上面这种情况下, 因为插入前我们持有的是前驱结点 **pNode** , 第 ④ 步一定要在第 ① 步之后, 不然链表的后半段就丢失了.

**(3) 结尾插入**<br>
在双链表的结尾插入新结点也简单, 假设 **tail** 指向尾结点, 插入步骤如下:<br>
① tail.next = newNode<br>
② newNode.prior = tail<br>

完整实现:

```java
    /**
     * 双链表插入
     *
     * @param head      头结点点
     * @param newNode   待插入结点
     * @param position  结点插入位置
     * @return          插入后的头结点
     */
    public static Node insert(Node head, Node newNode, int position) {
        // 判空
        if (head == null) {
            return newNode;
        }
        // 越界判断
        int size = getLength(head);
        if (position > size + 1 || position < 1) {
            System.err.println("IndexOutOfBound");
            return head;
        }
        // 表头位置插入
        if (position == 1) {
            newNode.next = head;
            head.prior = newNode;
            head = newNode;
            return head;
        }
        // 中间位置插入
        Node pNode = head;

        int index = 1;
        while (index < position - 1) {
            pNode = pNode.next;
            index++;
        }
        newNode.next = pNode.next;
        // 如果是尾插, pNode.next 为 null, 会报空指针
        if (pNode.next != null) {  // 因此需要判空
            pNode.next.prior = newNode;
        }
        newNode.prior = pNode;
        pNode.next = newNode;
        return head;
    }
```



### 3. 双链表删除

(1) 删除表头结点

(2) 删除最后一个结点

(3) 删除中间结点

```java

```

