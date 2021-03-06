---
title: "leetcode 236. 二叉树的最近公共祖先"
date: 2018-12-30T22:05:09+08:00
draft: false
tags: ["算法","数据结构","LeetCode"]
categories: ["数据结构与算法之美"]
comment: true
url: /2018/12/30/leetcode 236. 二叉树的最近公共祖先.html
---

### 题目描述
给定一个二叉树, 找到该树中两个指定节点的最近公共祖先

百度百科中最近公共祖先的定义为：“对于有根树 T 的两个结点 p、q，最近公共祖先表示为一个结点 x，满足 x 是 p、q 的祖先且 x 的深度尽可能大（一个节点也可以是它自己的祖先）。”

例如，给定如下二叉搜索树:  root = [3,5,1,6,2,0,8,null,null,7,4]

![二叉树](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/12/15/binarytree.png)

示例1:
```
输入: root = root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 1
输出: 3 
解释: 节点 5 和节点 1 的最近公共祖先是节点 3。
```

示例2:
```
输入: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 4
输出: 5
解释: 节点 5 和节点 4 的最近公共祖先是节点 5。因为根据定义最近公共祖先节点可以为节点本身。
```

说明:
  * 所有节点的值都是唯一的
  * p、q 为不同节点且均存在于给定的二叉树中。

### 思路
- 两个不同节点，在树中存在4种状态，1：都在root的左子树中 2，都在root的右子树中 3，分别在root的左右子树中 4，其中一个节点为root节点

### 代码实现
```
//TreeNode Definition for TreeNode.
type TreeNode struct {
	Val   int
	Left  *TreeNode
	Right *TreeNode
}

func lowestCommonAncestor(root, p, q *TreeNode) *TreeNode {
	if root == nil {
		//未找到p和q
		return nil
	}

	if root.Val == p.Val || root.Val == q.Val {
		//找到p或q
		return root
	}

	left := lowestCommonAncestor(root.Left, p, q)
	right := lowestCommonAncestor(root.Right, p, q)
	if left == nil && right == nil {
		//p,q不存在
		return nil
	} else if left != nil && right != nil {
		//1， p,q分别在root的两边
		return root
	} else {
		//2, p,q在左子树或右子树
		if left != nil {
			//都在左子树
			return left
		}
		//都在右子树
		return right
	}
}
```

### 参考资料
- [leetcode 236. 二叉树的最近公共祖先](https://leetcode-cn.com/problems/lowest-common-ancestor-of-a-binary-tree/)

### GitHub
- [源码传送门](https://github.com/TomorrowWu/golang-algorithms/blob/masterleetcode/0236.lowest-common-ancestor-of-a-binary-tree/src/lowest-common-ancestor-of-a-binary-tree.go)
- 各种数据结构及算法实现, LeetCode解题思路及答案
- [大厂面试题汇总及答案解析](https://github.com/TomorrowWu/interview)

> 本文为原创文章，转载注明出处，欢迎扫码关注公众号 ```楼兰``` 或者网站[https://lovecoding.club](https://lovecoding.club),第一时间看后续精彩文章，觉得好的话，顺手分享到朋友圈吧，感谢支持。

![image](https://upload-images.jianshu.io/upload_images/5815624-4a8b49cfbaf037dd.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/200)
