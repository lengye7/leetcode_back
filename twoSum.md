# leetcode第1题：两数之和

> [题目](https://leetcode-cn.com/problems/two-sum/):给定一个整数数组 nums 和一个整数目标值 target，
> 请你在该数组中找出 和为目标值 target  的那 两个 整数，并返回它们的数组下标。你可以假设每种输入只会对
> 应一个答案。但是，数组中同一个元素在答案里不能重复出现。你可以按任意顺序返回答案。

    示例 1：
    输入：nums = [2,7,11,15], target = 9
    输出：[0,1]
    解释：因为 nums[0] + nums[1] == 9 ，返回 [0, 1] 。


    示例 2：
    输入：nums = [3,2,4], target = 6
    输出：[1,2]


    示例 3：
    输入：nums = [3,3], target = 6
    输出：[0,1]


    提示：
    2 <= nums.length <= 104
    -109 <= nums[i] <= 109
    -109 <= target <= 109
    只会存在一个有效答案
    进阶：你可以想出一个时间复杂度小于 O(n2) 的算法吗？


## 代码

### 版本一

``` Javascript
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[]}
 */
var twoSum = function(nums, target) {

    //暴力法
    let len = nums.length -1;
    for(let index=0;index < len;index++){
        for(let j_index = index+1;j_index < nums.length;j_index++){
            if(target === nums[index] +nums[j_index] ){
                return [index,j_index];
            }
        }
    }
};
```

### 版本二

``` Javascript
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[]}
 */
var twoSum = function(nums, target) {
       
    //利用Array的indexof方法，一次遍历完成,一次遍历比暴力法还差，我了个乖乖。
    let len = nums.length -1;
    let num_index = -1;
    let buffer = 0.3;
    for(let index = 0;index < len; index++){
        buffer = target - nums[index];
        num_index = nums.indexOf(buffer,index+1)
        if( num_index > index){
            return [index,num_index]
        }
    }
};

```

### 版本三

``` Javascript
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[]}
 */
var twoSum = function(nums, target) {

    //利用map存储配对数，在后续的遍历过程中直接进行配对
    //速度还是不理想，map查看难道不是基于hash映射的？我直接数组随机访问试试？
    let map_buffer = new Map();
    let buffer = 0.3;
    for(let index = 0; index < nums.length; index++){
        if(map_buffer.has(nums[index])){
            return [map_buffer.get(nums[index]),index];
        }
        else{//本题中明确说明只对应一个答案，因此不用处理重复的数字。
            buffer = target - nums[index];
            map_buffer.set(buffer,index);
        }
    }
};
```

### 版本四

``` Javascript
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[]}
 */
var twoSum = function(nums, target) {
    //利用数组随机访问来代替map，尝试较快执行速度，但是肯定极大的提高内存消耗。
    let map = [];
    let buffer = 0.3;
    for(let index = 0; index < nums.length; index++){
        if(map[nums[index]] !== undefined){
            return [map[nums[index]],index];
        }
        else{
            buffer = target - nums[index];
            map[buffer] = index;
        }
    }
};
```

### 版本五

``` Javascript
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[]}
 */
var twoSum = function(nums, target) {

    //我使用了map以及array的映射之后，发现自己的代码效率仍然很差，我一度怀疑这俩数据结构的映射的真实性。
    //参考了一下别人的代码实现，我发现我的代码似乎是没有考虑scope chain的问题？下面是尝试改进的版本。
    //改进之后果然效率提升了不少。
    let map_buffer = new Map();
    for(let index = 0; index < nums.length; index++){
        let num1 = nums[index];
        let buffer = target - num1;
        if(map_buffer.has(num1)){
            return [map_buffer.get(num1),index];
        }
        //本题中明确说明只对应一个答案，因此不用处理重复的数字。
        map_buffer.set(buffer,index);
    }
};
```

