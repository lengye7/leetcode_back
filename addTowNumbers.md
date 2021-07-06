# leetcode的第2题：两数相加 

> [题目](https://leetcode-cn.com/problems/add-two-numbers/):
> 给你两个 非空 的链表，表示两个非负的整数。它们每位数字都是按照 逆序 的方式存储的，
> 并且每个节点只能存储 一位 数字。请你将两个数相加，并以相同形式返回一个表示和的链表。
> 你可以假设除了数字 0 之外，这两个数都不会以 0 开头。 

    示例 1：
    输入：l1 = [2,4,3], l2 = [5,6,4]
    输出：[7,0,8]
    解释：342 + 465 = 807.  


    示例 2：
    输入：l1 = [0], l2 = [0]
    输出：[0]  


    示例 3：
    输入：l1 = [9,9,9,9,9,9,9], l2 = [9,9,9,9]
    输出：[8,9,9,9,0,0,0,1] 

## 代码：

### 普通版本
``` Javascript
/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */
/**
 * @param {ListNode} l1
 * @param {ListNode} l2
 * @return {ListNode}
 */

var addTwoNumbers = function(l1, l2) {

    //正常版本
    let ca = 0;
    let num = 0;
    let flag = 0;
    let first_node = 0;
    let current_node = 0;
    while(l1 !==null || l2 !== null){
        if(l1 !== null && l2 !==null){
            num = l1.val + l2.val + ca;
            ca = Math.floor(num/10);
            num = num % 10;
            l1 = l1.next;
            l2 = l2.next;
        }
        else if(l1 !== null){
            num = l1.val + ca;
            ca = Math.floor(num/10);
            num = num % 10;
            l1 = l1.next;
        }
        else if(l2 !== null){
            num = l2.val + ca;
            ca = Math.floor(num/10);
            num = num % 10;
            l2 = l2.next;
        }
        if(0 === flag){
            current_node = new ListNode(num,null);
            first_node = current_node;
            flag = -1;
        }
        else{
            current_node.next = new ListNode(num,null);
            current_node = current_node.next;
        }
    }
    if(ca > 0){
        current_node.next = new ListNode(ca,null)
        current_node = current_node.next;
    }
    return first_node;
};
```
### 优化版本

``` Javascript
/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */
/**
 * @param {ListNode} l1
 * @param {ListNode} l2
 * @return {ListNode}
 */
var addTwoNumbers = function(l1, l2) {

    //优化版本：优化了scope chain，减少了计算次数。
    let ca = 0;
    let first_node = null;
    let current_node = null;
    while(l1 || l2){
        let num1 = (l1)?l1.val:0;
        let num2 = (l2)?l2.val:0;
        num1 = num1 + num2 + ca;
        const node = new ListNode(num1%10);
        ca = Math.floor(num1/10);
        if(first_node){
            current_node.next = node;
            current_node = current_node.next;
        }
        else{
            current_node = node;
            first_node = node;
        }
        if(l1){
            l1 = l1.next;
        }
        if(l2){
            l2 = l2.next;
        }
    }
    if(ca > 0){
        current_node.next = new ListNode(ca);
        //优化版本，最后一次不移动current_node指针
    }
    return first_node;
};
```

