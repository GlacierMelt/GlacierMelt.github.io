---
title: "Alogrithm MAP"
date: 2020-04-12 17:05:18
featured_image: '/images/demo/sunlight_mountain.JPG'
excerpt: MAP
---

![image](/images/demo/sunlight_mountain.JPG)
<center>Photo by <a style="background-color:black;color:white;text-decoration:none;padding:4px 6px;font-family:-apple-system, BlinkMacSystemFont, &quot;San Francisco&quot;, &quot;Helvetica Neue&quot;, Helvetica, Ubuntu, Roboto, Noto, &quot;Segoe UI&quot;, Arial, sans-serif;font-size:12px;font-weight:bold;line-height:1.2;display:inline-block;border-radius:3px" href="https://unsplash.com/@josephyates_?utm_medium=referral&amp;utm_campaign=photographer-credit&amp;utm_content=creditBadge" target="_blank" rel="noopener noreferrer" title="Download free do whatever you want high-resolution photos from Joe Yates"><span style="display:inline-block;padding:2px 3px"><svg xmlns="http://www.w3.org/2000/svg" style="height:12px;width:auto;position:relative;vertical-align:middle;top:-2px;fill:white" viewBox="0 0 32 32"><title>unsplash-logo</title><path d="M10 9V0h12v9H10zm12 5h10v18H0V14h10v9h12v-9z"></path></svg></span><span style="display:inline-block;padding:2px 3px">Joe Yates</span></a></center>

## 链表

### 反转链表

#### 1. 反转一个单链表
**实例**<br>
输入: 1->2->3->4->5->NULL<br>
输出: 5->4->3->2->1->NULL

```cpp
ListNode* reverseList(ListNode* head){
    if(head->next == NULL) return head;
    ListNode* last = reverseList(head->next);
    head->next->next = head;
    head->next = NULL;
    return last;
}
```
---
#### 2. 反转链表前N个节点
**实例**<br>
**输入**: 1->2->3->4->5->NULL, n = 3<br>
**输出**: 3->2->1->4->5->NULL
```cpp
ListNode* reverseN(ListNode* head, int n, ListNode* successor){
    if(n==1){
        return head;
    }
    ListNode* last = reverseN(head->next, --n, successor);
    head->next->next = head;
    head->next = successor;
    return last;
}
```
---
#### 3. 反转链表的一部分
**实例**<br>
**输入**: 1->2->3->4->5->NULL, m = 2, n = 4<br>
**输出**: 1->4->3->2->5->NULL

```cpp
ListNode* reverseBetween(ListNode* head, int m, int n, ListNode* successor){
    if(m==1){
        return reverseN(head, n, successor);
    }
    head->next = reverseBetween(head->next, --m, --n, successor);
    return head;
}
```
### 合并链表

#### 1. 合并两个有序链表
**实例**<br>
**输入**：1->2->4, 1->3->4<br>
**输出**：1->1->2->3->4->4
```cpp
ListNode* merge2List(ListNode* head_0, ListNode* head_1){
    ListNode* temp = 0; ListNode* first=0;
    while(head_0!=0 && head_1!=0){
        if(head_0->val < head_1->val){
            if(temp==0) temp = first = head_0;
            else{
                temp->next = head_0;
                temp = head_0;
            }
            head_0 = head_0->next;
        }else{
            if(temp==0) temp = first = head_1;
            else{
                temp->next = head_1;
                temp = head_1;
            }
            head_1 = head_1->next;
        }
    }
    if(head_0==0) temp->next = head_1;
    else temp->next = head_0;
    return first;
}
```
### Remaining code
```cpp
#include <stdio.h>
#include <malloc.h>

typedef struct Node{
    int val;
    struct Node* next;
}ListNode;

ListNode* instance(int *nums, int length){
    ListNode* head = NULL;
    ListNode* H = (ListNode*)malloc(sizeof(ListNode));
    for(int i=0; i<length; i++){
        ListNode* temp = (ListNode*)malloc(sizeof(ListNode));
        temp->val = nums[i];
        temp->next = NULL;
        if(i==0){
            head = temp;
            H = head;
        }else{
            H->next = temp;
            H = H->next;
        }
    }
    return head;
}

void display(ListNode* ins){
    while(ins != NULL){
        printf("%d->", ins->val);
        ins = ins->next;
    }
    printf("NULL\n");
}

void printrear2head(ListNode* ins){
    if(ins == NULL) return;
    printrear2head(ins->next);
    printf("%d ", ins->val);
}

ListNode* location(ListNode* head, int n){
    ListNode* successor = NULL;
    ListNode* temp = head;
    for(int i=0; i<n; i++){
        successor = temp->next;
        temp = temp->next;
    }
    return successor;
}

int main()
{
    printf("Hello World\n");
    int array[] = {1,2,3,4,5};
    int array_1[] = {6,7,8,9,10};
    int length = sizeof(array)/sizeof(array[0]);
    ListNode* ins = instance(array, length);
    ListNode* ins_1 = instance(array_1, length);
    display(ins);
    display(ins_1);

    ListNode* ins_merge = merge2List(ins, ins_1);
    display(ins_merge);

    printrear2head(ins); printf("\n");

    ins = reverseList(ins);
    display(ins);

    int n = 3;
    ins = reverseN(ins, n, location(ins, n));
    display(ins);

    int m=5;
    ins = reverseBetween(ins, n, m, location(ins, m));
    display(ins);

    return 0;
}
```


[^1]: Image from <a style="background-color:black;color:white;text-decoration:none;padding:4px 6px;font-family:-apple-system, BlinkMacSystemFont, &quot;San Francisco&quot;, &quot;Helvetica Neue&quot;, Helvetica, Ubuntu, Roboto, Noto, &quot;Segoe UI&quot;, Arial, sans-serif;font-size:12px;font-weight:bold;line-height:1.2;display:inline-block;border-radius:3px" href="https://unsplash.com/@josephyates_?utm_medium=referral&amp;utm_campaign=photographer-credit&amp;utm_content=creditBadge" target="_blank" rel="noopener noreferrer" title="Download free do whatever you want high-resolution photos from Joe Yates"><span style="display:inline-block;padding:2px 3px"><svg xmlns="http://www.w3.org/2000/svg" style="height:12px;width:auto;position:relative;vertical-align:middle;top:-2px;fill:white" viewBox="0 0 32 32"><title>unsplash-logo</title><path d="M10 9V0h12v9H10zm12 5h10v18H0V14h10v9h12v-9z"></path></svg></span><span style="display:inline-block;padding:2px 3px">Joe Yates</span></a>
