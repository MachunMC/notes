#### 1. 对称二叉树

2021年6月6日 周日

<img src="https://note.youdao.com/yws/public/resource/a66685a4842f56c1ad2c2aaf50a39424/xmlnote/53D5100C80DF4197885F8BF6F42734EC/27051" style="zoom: 70%;" />

```C
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     struct TreeNode *left;
 *     struct TreeNode *right;
 * };
 */

/*
    解题思路：
    1. 将二叉树划分为左子树和右子树，将问题转换为判断左子树和右子树是否相等
    2. 将左右子树进一步划分为根节点、和左右两个子树
        - 左子树的左孩子节点和右子树的右孩子节点对称
        - 左子树的右孩子节点和右子树的左孩子节点对称
    3. 一步步转变为判断子节点是否对称
*/

bool ifEqual(struct TreeNode* pLeft, struct TreeNode* pRight);


bool isSymmetric(struct TreeNode* root){
    if (NULL == root)
    {
        return false;
    }
    else
    {
        if (NULL == root->left && NULL == root->right)
        {
            return true;
        }
        else if (NULL != root->left && NULL != root->right)
        {
            return ifEqual(root->left, root->right);
        }
        else
        {
            return false;
        }
    }
}

bool ifEqual(struct TreeNode* pLeft, struct TreeNode* pRight)
{
    // 异常判断
    if (NULL == pLeft || NULL == pRight)
    {
        return false;
    }

    // 4个子节点从左到右，编号分别为1,2,3,4
    if (pLeft->val == pRight->val)
    {
        // 4个子节点都没有
        if (pLeft->left == NULL && pRight->right == NULL && pLeft->right == NULL && pRight->left == NULL)
        {
            return true;
        }
        else if (pLeft->left == NULL && pRight->right == NULL) // 缺少1、4节点
        {
            if (pLeft->right != NULL && pRight->left != NULL)
            {
                return ifEqual(pLeft->right, pRight->left);
            }
            else
            {
                return false;
            }
        }
        else if (pLeft->right == NULL && pRight->left == NULL) // 缺少2、3节点
        {
            if (pLeft->left != NULL && pRight->right != NULL)
            {
                return ifEqual(pLeft->left, pRight->right);
            }
            else
            {
                return false;
            }
        }
        else // 都不缺
        {
            if (ifEqual(pLeft->left, pRight->right) && ifEqual(pLeft->right, pRight->left))
            {
                return true;
            }
            else
            {
                return false;
            }
        }
    }
    else
    {
        return false;
    }
}
```



#### 2. 环形链表

2021年6月10日 周四

<img src="https://note.youdao.com/yws/public/resource/a66685a4842f56c1ad2c2aaf50a39424/xmlnote/79B13AFF79A740169325B24E5A72E082/27053" style="zoom:67%;" />

<img src="https://note.youdao.com/yws/public/resource/a66685a4842f56c1ad2c2aaf50a39424/xmlnote/70E51215D9724A65ADEDD8D0A4CF6C9A/27055" style="zoom:67%;" />

```C
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     struct ListNode *next;
 * };
 */
 
 /*
    解题思路：
    1. 快慢指针：一个指针跑得快，一个指针跑的慢，如果有环，快的指针遍历所有结点后，会重新追上慢的
    2. 将所有访问过的结点保存到哈希表里（不推荐）
 */
bool hasCycle(struct ListNode *head) {
    struct ListNode *fast = head;
    struct ListNode *low  = head;

    // 有0个或1个结点
    if (NULL == head || NULL == head->next)
    {
        return false;
    }

    while(fast != NULL && fast->next != NULL)
    {
        fast = fast->next->next;
        low = low->next;

        if (low == fast)
        {
            return true;
        }
    }

    return false;
}
```



#### 3. 汉明距离

2021年6月10日 周四

<img src="https://note.youdao.com/yws/public/resource/a66685a4842f56c1ad2c2aaf50a39424/xmlnote/F9824E06DB6E4D568068E43A31DF91ED/27057" style="zoom:67%;" />

```C
int hammingDistance(int x, int y){
    int numx[32] = {0};  // 保存二进制对应的数值
    int numy[32] = {0};
    int len = 0;       // 二进制长度
    int diff = 0;

    // 求x的二进制对应的数值，“除二取余倒排列”
    while(x > 0)
    {
        numx[len] = x % 2;
        x = x / 2;
        len++;
    }

    len = 0;
    while(y > 0)
    {
        numy[len] = y % 2;
        y = y / 2;
        len++;
    }

    for (int i = 0; i < 32; i++)
    {
        if (numy[i] != numx[i])
        {
            diff++;
        }
    }

    return diff;
}
```

