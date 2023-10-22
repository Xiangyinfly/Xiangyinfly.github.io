## 二叉树
### 特点
1.如果该二叉树的所有叶子节点都在最后一层，并且结点总数=2^n-1,n为层数，则我们称为满二叉树。 

2.如果该二叉树的所有叶子节点都在最后一层或者倒数第二层，而且最后一层的叶子节点在左边连续，倒数第二层的叶子节点在右边连续，我们称为完全二叉树。

3.前序遍历：先输出父节点，再遍历左子树和右子树  
中序遍历：先遍历左子树，再输出父节点，再遍历右子树  
后序遍历：先遍历左子树，再遍历右子树，最后输出父节点

### 线索化二叉树
1）n个结点的二叉链表中含有n+1(2n-(n-1)=n+1)个空指针域。利用二叉链表中的空指针域，存放指向该结点在某种遍历次序下的前驱和后继结点的指针（这种附加的指针称为"线索"） 

2）这种加上了线索的二叉链表称为线索链表，相应的二叉树称为线索二叉树 (ThreadedBinaryTree)。根据线索性质的不同，线索二叉树可分为前序线索二叉树、中序线索二叉树和后序线索二叉树三种

3）一个结点的前一个结点，称为前驱结点;一个结点的后一个结点，称为后继结点

### 前序、中序、后序线索化比较
1. 前序线索化二叉树遍历相对最容易理解，实现起来也比较简单。由于前序遍历的顺序是：根左右，所以从根节点开始，沿着左子树进行处理，当子节点的left指针类型是线索时，说明到了最左子节点，然后处理子节点的right指针指向的节点，可能是右子树，也可能是后继节点，无论是哪种类型继续按照上面的方式（先沿着左子树处理，找到子树的最左子节点，然后处理right指针指向），以此类推，直到节点的right指针为空，说明是最后一个，遍历完成。

2. 中序线索化二叉树的网上相关介绍最多。中序遍历的顺序是：左根右，因此第一个节点一定是最左子节点，先找到最左子节点，依次沿着right指针指向进行处理（无论是指向子节点还是指向后继节点），直到节点的right指针为空，说明是最后一个，遍历完成。

3. 后序遍历线索化二叉树最为复杂，通用的二叉树数节点存储结构不能够满足后序线索化，因此我们扩展了节点的数据结构，增加了父节点的指针。后序的遍历顺序是：左右根，先找到最左子节点，沿着right后继指针处理，当right不是后继指针时，并且上一个处理节点是当前节点的右节点，则处理当前节点的右子树，遍历终止条件是：当前节点是root节点，并且上一个处理的节点是root的right节点。

## 哈夫曼树
### 基本介绍
1.给定n个权值作为n个叶子结点，构造一棵二叉树，若该树的带权路径长度 (wpl)达到最小，称这样的二叉树为最优二叉树，也称为哈夫曼树(Huffman Tree)，还有的书翻译为霍夫曼树。

2.赫夫曼树是带权路径长度最短的树，权值较大的结点离根较近。
### 重要概念
1）路径和路径长度：在一棵树中，从一个结点往下可以达到的孩子或孙子结点之间的通路，称为路径。通路中分支的数目称为路径长度。若规定根结点的层数为1，则从根结点到第L层结点的路径长度为L-1 

2)结点的权及带权路径长度：若将树中结点赋给一个有着某种含义的数值，则这个数值称为该结点的权。结点的带权路径长度为：从根结点到该结点之间的路径长度与该结点的权的乘积

### 创建
1）从小到大进行排序,将每一个数据，每个数据都是一个节点，每个节点可以看成是一颗最简单的二叉树

2）取出根节点权值最小的两颗二叉树

3）组成一颗新的二叉树，该新的二叉树的根节点的杈值是前面两颗二叉树根节点权值的和 

4）再将这颗新的二叉树，以根节点的权值大小再次排序，不断重复1-2-3-4的步骤，直到数列中，所有的数据都被处理，就得到一颗赫夫曼树

## 二叉排序树
### 删除节点
第一种情况：删除叶子节点  
(1)需要先去找到要删除的节点targetNode  
(2)找到targetNode的父结点parent  
(3)确定targetNode是parent的左子结点还是右子结点  
(4)根据前面的情况来对应删除
>左子结点parent.left=null  
>右子结点parent.right=null

第二种情況：删除只有一颗子树的节点  
(1)需要先去找到要删除的结点targetNode  
(2)找到targetNode的父结点parent  
(3)确定targetNode的子结点是左子结点还是右子结点  
(4)targetNode是parent的左子结点还是右子结点  
(5)如果targetNode有左子结点  
>5.1如果targetNode是parent的左子结点
>parent.left=targetNode.left;

>5.2如果targetNode是parent的右子结点
>parent.right = targetNode.left;

(6)如果targetNode有右子结点
>6.1如果targetNode是parent的左子结点
parent.left = targetNode.right;

>6.2如果targetNode是parent的右子结点
parent.right=targetNode.right;

第三种情况：删除有两颗子树的节点（由于二叉排序树中序遍历为从小到大顺序，这样替换可以保持仍是二叉排序树）  
(1)需求先去找到要删除的结点targetNode  
(2)找到targetNode的父結点parent  
(3)从targetNode的右子树找到最小的结点（或者左子树最大的结点）  
(4)用一个临时变量temp，将最小结点的值保存  
(5)删除该最小结点  
(6)targetNode.value = temp

## AVL树
### 特点
1.平衡二叉树也叫平衡二叉搜索树(self-balancing binary search tree)又被称为AVL树，可以保证查询效率较高。

2.具有以下特点：它是一棵空树或它的左右两个子树的高度差的绝对值不超过1，并且左右两个子树都是一棵平衡二叉树。平衡二叉树的常用实现方法有红黑树、AVL、替罪羊树、Treap、伸展树等。