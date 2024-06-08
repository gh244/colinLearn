# 树

## **JZ55** **二叉树的深度**

​		输入一棵二叉树，求该树的深度。从根结点到叶结点依次经过的结点（含根、叶结点）形成树的一条路径，最长路径的长度为树的深度，根节点的深度视为 1 。

​		数据范围：节点的数量满足 0≤𝑛≤1000≤*n*≤100 ，节点上的值满足 0≤𝑣𝑎𝑙≤1000≤*v**a**l*≤100

​		进阶：空间复杂度 𝑂(1)*O*(1) ，时间复杂度 𝑂(𝑛)*O*(*n*)

​		假如输入的用例为{1,2,3,4,5,#,6,#,#,7}，那么如下图:

<img src="C:\Users\gengh\Desktop\科林\笔记\LeetCode笔记图片\DFDBE52B6C61F8021FC86EB0779848B1" alt="img" style="zoom:50%;" />

**方法一：**

​		使用递归的方式对二叉树进行遍历，每次递归深度加1，同时维护一个**最大深度**（depthMax），最终将最大深度返回。

```c++
class Solution {
public:
	int depthMax = 0;
	void search(TreeNode* pRoot, int depth) {
		if (pRoot == nullptr) return;
		depthMax = ::max(depthMax, depth);
		search(pRoot->left, depth + 1);
		search(pRoot->right, depth + 1);
	}
    int TreeDepth(TreeNode* pRoot) {
		search(pRoot, 1);
		return depthMax;
    }
};
```

**方法二：**

​		通过队列的大小可以知道二叉树某一层的节点数，只要记录每一层的节点数，就可以知道当前层是否已经处理完成。当前层处理完成后，此时再获取当前队列大小，又可以获得下一层节点数。也就是说，每一层处理完成后就可以将二叉树深度加1，直至所有节点处理完成，就可以得到整颗二叉树的深度。

```c++
class Solution {
public:
    int TreeDepth(TreeNode* pRoot) {
		if (pRoot == nullptr) return 0;
		queue<TreeNode*> que;
		que.push(pRoot);
		int size = 1;
		int depth = 0;

		while (!que.empty()) {
			pRoot = que.front();
			que.pop();
			size -= 1;
			if (pRoot->left) que.push(pRoot->left);
			if (pRoot->right) que.push(pRoot->right);

			if (size == 0) {
				depth++;
				size = que.size();
			}
		}

		return depth;
    }
};
```

