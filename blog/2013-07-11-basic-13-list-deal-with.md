---
layout: post
title: 链表--常见操作
description: 删除一个节点、输出倒数第k个节点、链表反转
published: true
category: CS basic
---

##删除链表节点

Tips:

> 注意边界条件的判断，当删除的节点是head、或者尾节点时，类似临界条件需要单独考虑。


	
	void DeleteNode(ListNode **pListHead,ListNode * pToBeDeleted)  
	{  
		if(!pListHead || !pToBeDeleted)  
			return;  
		//要删除的结点不是尾结点  
		if(pToBeDeleted->m_pNext!=NULL)  
		{  
			ListNode * pNext=pToBeDeleted->m_pNext;  
			pToBeDeleted->m_nValue=pNext->m_nValue;  
			pToBeDeleted->m_pNext=pNext->m_pNext;  
			delete pNext;  
			pNext=NULL;  
		}  
		//链表只有一个结点，删除头结点，也是尾结点  
		else if(*pListHead == pToBeDeleted)  
		{  
			delete pToBeDeleted;  
			pToBeDeleted=NULL;  
			*pListHead=NULL;  
		}  
		//链表中有多个结点，删除尾结点  
		else  
		{  
			ListNode *pNode=*pListHead;  
			while(pNode->m_pNext!=pToBeDeleted)  
				pNode=pNode->m_pNext;  
			pNode->m_pNext=NULL;  
			delete pToBeDeleted;  
			pToBeDeleted=NULL;  
		}  
	}  
	/**/


重写一遍上述代码，两种场景：


###场景1：被删除的节点，不为头结点、也不为尾节点

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

###场景2：被删除的节点，可能为头结点、尾节点

若需要考虑，被删除的节点为`头结点`、`尾节点`的情况，则，需要借助链表的头部地址，代码如下：

	void deleteNode(Node* pHead, Node* pToBeDeleted)
	{
		if(pHead == null || pToBeDeleted == null)
			return ;

		if(pHead == pToBeDeleted)	// 头节点
			pHead = pHead->next;

		if(pToBeDeleted->next == null)	// 尾节点
		{
			Node* pCur = pHead;
			while(pCur->next != pToBeDeleted)
			{
				pCur = pCur->next;
			}
			pCur->next = null;
			pToBeDeleted = null;
		}

		// 既非头结点，也非尾节点
		Node* pNext = pToBeDeleted->next;
		pToBeDeleted->value = pNext->value;
		pToBeDeleted->next = pNext->next;

	}










##链表中倒数第k个节点


Tips:

> 注意边界条件的判断，链表为空，k小于等于0，链表长度小于k。

思路：设定两个指针，间隔为k-1，当第一个指针到达链表末端时，第二个指针即指向倒数第k个节点。


	Node* FindKthTotail(Node *head, int k)
	{
		if(head == NULL || k <= 0)  // 边界条件
			return NULL;

		Node *pAhead = head;
		Node *pAfter = head;

		for(int i=0;i<k-1;i++)
		{
			pAhead = pAhead->next;
			if(pAhead->next == NULL)  // 边界条件
				return NULL;
		   
		}

		while(pAhead->next != NULL)	// 结束条件
		{
			pAfter = pAfter->next;
			pAhead = pAhead->next;
			
		}

		return pAfter;
	}



##反转链表


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

##合并两个排序的链表


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


##链表排序

直接使用冒泡排序即可，哈哈；










[NingG]:    http://ningg.github.com  "NingG"


[面试题15：合并两个排序的链表]:			http://blog.csdn.net/htyurencaotang/article/details/9396733






