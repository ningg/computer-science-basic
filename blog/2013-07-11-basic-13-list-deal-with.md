---
layout: post
title: 链表--常见操作
description: 删除一个节点、输出倒数第k个节点、链表反转
published: true
category: CS basic
---

## 删除链表节点

Tips:

> 注意边界条件的判断，当删除的节点是head、或者尾节点时，类似临界条件需要单独考虑。


    /**
     * 删除指定节点
     *
     * @param pHead 链表的头节点
     * @param toBeRemoved 需要被删除的节点
     */
    public static void removeNode(Node pHead, Node toBeRemoved) {
        // 1. 边界判断
        if (null == pHead || null == toBeRemoved) {
            return;
        }

        // 2. 删除节点
        // a. 头部节点: 直接指向「下一个节点」
        // note: 需要借助「头节点」
        if (pHead == toBeRemoved) {
            pHead = pHead.next;
            return;
        }

        // b. 尾部节点: 从前遍历, 到倒数第二个节点, 然后, 删除最后一个
        // note: 需要借助「头节点」
        if (toBeRemoved.next == null) {
            Node pCurr = pHead;
            while (pCurr.next != toBeRemoved) {
                pCurr = pCurr.next;
            }
            pCurr.next = null;
            return;
        }

        // c. 中间节点: 非头部、非尾部节点
        // note: 不需要借助「头结点」
        toBeRemoved.value = toBeRemoved.next.value;
        toBeRemoved.next = toBeRemoved.next.next;
    }


重写一遍上述代码，两种场景：


### 场景1：被删除的节点，不为头结点、也不为尾节点

当被删除的节点，既不为`头结点`，也不为`尾节点`时，不需要知道链表的头部地址，代码如下：

void deleteNode(Node* pToBeDeleted)
{
	if(pToBeDeleted == null)
		return ;

	Node* pNext = pToBeDeleted->next;

	if(pNext == null)
		return ;

	pToBeDeleted->value = pNext->value;
	pToBeDeleted->next = pNext->next;

}

### 场景2：被删除的节点，可能为头结点、尾节点

若需要考虑，被删除的节点为`头结点`、`尾节点`的情况，则，需要借助链表的头部地址，代码如下：

    /**
     * 删除指定节点
     *
     * @param pHead 链表的头节点
     * @param toBeRemoved 需要被删除的节点
     */
    public static void removeNode(Node pHead, Node toBeRemoved) {
        // 1. 边界判断
        if (null == pHead || null == toBeRemoved) {
            return;
        }

        // 2. 删除节点
        // a. 头部节点: 直接指向「下一个节点」
        // note: 需要借助「头节点」
        if (pHead == toBeRemoved) {
            pHead = pHead.next;
            return;
        }

        // b. 尾部节点: 从前遍历, 到倒数第二个节点, 然后, 删除最后一个
        // note: 需要借助「头节点」
        if (toBeRemoved.next == null) {
            Node pCurr = pHead;
            while (pCurr.next != toBeRemoved) {
                pCurr = pCurr.next;
            }
            pCurr.next = null;
            return;
        }

        // c. 中间节点: 非头部、非尾部节点
        // note: 不需要借助「头结点」
        toBeRemoved.value = toBeRemoved.next.value;
        toBeRemoved.next = toBeRemoved.next.next;
    }





## 链表中倒数第k个节点


Tips:

> 注意边界条件的判断，链表为空，k小于等于0，链表长度小于k。

思路：设定两个指针，间隔为 k，当第一个指针到达链表末端 null 时，第二个指针即指向倒数第k个节点。


    /**
     * 找出链表中, 倒数第 k 个节点
     *
     * @param head 链表头指针
     * @param k 倒数第 k 个节点
     * @return 找到的目标节点
     */
    public static Node findKthToTail(Node head, int k) {
        // 1. 边界判断
        if (null == head || k <= 0) {
            return null;
        }

        // 2. 寻找 k-th 节点
        // a. 两个指针, 一个先走(相聚 k 个节点)
        Node former = head;
        Node latter = head;
        for (int i = 1; i <= k; i++) {
            if (null != former) {
                former = former.next;
            } else {
                return null;
            }
        }

        // b. 先走的节点, 走到 null, 则, 说明后走的节点,
        while (null != former) {
            former = former.next;
            latter = latter.next;
        }
        return latter;
    }



## 反转链表


画图理清思路，直接使用4个节点来看，注意边界条件，输入链表为null的判断；示例代码如下：

	Node* ReversedList(Node* pHead)
	{
		if(pHead == null || pHead->next == null)
			return pHead;

		Node* pPre = null;
		Node* pCur = pHead;
		Node* pNext = pHead->next;

		while(pNext != null)
		{
			pCur->next = pPre;
			pPre = pCur;
			pCur = pNext;
			pNext = pNext->next;

		}

		pCur->next = pPre;
		return pCur;
	}

## 合并两个排序的链表


非递归方法：


	//合并两个有序链表,非递归方法  
	ListNode* MergeTwoList(ListNode* pHead1, ListNode* pHead2)  
	{  
		if (pHead1 == NULL)  
			return pHead2;  
		else if (pHead2 == NULL)  
			return pHead1;  
	  
		ListNode * pNode1 = pHead1;  
		ListNode * pNode2 = pHead2;  
		ListNode * pMergeListHead = NULL;  
		ListNode * pCurLastNode = NULL;  
	  
		if (pNode1->m_nValue < pNode2->m_nValue)  
		{             
			pMergeListHead = pHead1;  
			pNode1 = pNode1->m_pNext;  
			pCurLastNode = pMergeListHead;  
		}  
		else  
		{  
			pMergeListHead = pHead2;  
			pNode2 = pNode2->m_pNext;  
			pCurLastNode = pMergeListHead;  
		}  
	  
		while (pNode1 != NULL && pNode2 != NULL)  
		{  
			if (pNode1->m_nValue < pNode2->m_nValue)  
			{     
				pCurLastNode->m_pNext = pNode1;  
				pCurLastNode = pNode1;  
				pNode1 = pNode1->m_pNext;              
			}  
			else  
			{  
				pCurLastNode->m_pNext = pNode2;  
				pCurLastNode = pNode2;  
				pNode2 = pNode2->m_pNext;              
			}  
	  
			if (pNode1 == NULL)  
			{  
				pCurLastNode->m_pNext = pNode2;                
			}  
			  
			if (pNode2 == NULL)  
			{  
				pCurLastNode->m_pNext = pNode1;            
			}  
		}  
	  
		return pMergeListHead;  
	}  

递归方式：

	//合并两个有序链表,递归方法  
	ListNode *MergeTwoList(ListNode *pListOneHead, ListNode *pListTwoHead)  
	{  
		if (pListOneHead == NULL)  
			return pListTwoHead;  
		else if (pListTwoHead == NULL)  
			return pListOneHead;  
	  
		ListNode *pMergeListHead = NULL;  
	  
		if (pListOneHead->m_nValue < pListTwoHead->m_nValue)  
		{  
			pMergeListHead = pListOneHead;  
			pMergeListHead->m_pNext = MergeTwoList(pMergeListHead->m_pNext, pListTwoHead);  
		}  
		else  
		{  
			pMergeListHead = pListTwoHead;  
			pMergeListHead->m_pNext = MergeTwoList(pListOneHead, pMergeListHead->m_pNext);  
		}  
	  
		return pMergeListHead;  
	}  



参考：[面试题15：合并两个排序的链表][面试题15：合并两个排序的链表]


## 链表排序

本质: 归并方法, 进行链表排序

1. 拆分: 拆分出 2 个链表(找出中间节点, 拆分链表)
2. 排序: 递归对 2 个链表排序
3. 合并: 2 个有序链表, 排序








[NingG]:    http://ningg.github.com  "NingG"


[面试题15：合并两个排序的链表]:			http://blog.csdn.net/htyurencaotang/article/details/9396733






