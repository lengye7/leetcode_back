### leetcode第7题：整数反转

> [题目](https://leetcode-cn.com/problems/reverse-integer/submissions/):给你一个 32 位的有符号整数 x ，返回将 x 中的数字部分反转后的结果。如果反转后整数超> 过 32 位的有符号整数的范围 [−231,  231 − 1] ，就返回 0。假设环境不允许存储 64 位整数（有符号或无符号）。


    示例 1：
    输入：x = 123
    输出：321

    示例 2：
    输入：x = -123
    输出：-321


    示例 3：
    输入：x = 120
    输出：21


    示例 4：
    输入：x = 0
    输出：0

    提示：
    -2^31 <= x <= 2^31 - 1


``` Javascript
/**
 * @param {number} x
 * @return {number}
 */
var reverse = function(x) {
    let str = x.toString();
    if(x>=0){
        x = Number(str.split("").reverse().join(""));
    }
    else{
        x = -Number(str.split("-")[1].split("").reverse().join(""));
    }
    if( x >= -Math.pow(2,31) && x <= (Math.pow(2,31) - 1) ){
        return x;
    }
    else{
        return 0;
    }
};
```