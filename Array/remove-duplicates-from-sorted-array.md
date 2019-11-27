### 题目描述
**26. 删除排序数组中的重复项**
给定一个排序数组，你需要在原地删除重复出现的元素，使得每个元素只出现一次，返回移除后数组的新长度。
不要使用额外的数组空间，你必须在原地修改输入数组并在使用 O(1) 额外空间的条件下完成。
[Leetcode 原题地址](https://leetcode-cn.com/problems/remove-duplicates-from-sorted-array/)

**示例 1:**
> 给定数组 nums = [1,1,2], 
> 函数应该返回新的长度 2, 并且原数组 nums 的前两个元素被修改为 1, 2。 
> 你不需要考虑数组中超出新长度后面的元素。

**示例 2:**
> 给定 nums = [0,0,1,1,1,2,2,3,3,4],
>函数应该返回新的长度 5, 并且原数组 nums 的前五个元素被修改为 0, 1, 2, 3, 4。
> 你不需要考虑数组中超出新长度后面的元素。


**说明:**
为什么返回数值是整数，但输出的答案是数组呢?
请注意，输入数组是以“引用”方式传递的，这意味着在函数里修改输入数组对于调用者是可见的。

**解法 1**

>  通过创建一个临时数组，记录原数组中已存在的数值，循环判断
>  时间复杂度 O(n)
>  在`duplicateVals.includes(num)`、`duplicateVals.push(num)`、`nums.splice(i, 1)` 有较大的性能消耗，所以leetcode检测效率不高

```
var removeDuplicates = function(nums) {
   if (nums.length <= 1) return nums.length
   let duplicateVals = []
   for (let i = 0; i < nums.length; i++) {
       let num = nums[i]
       if (!duplicateVals.includes(num)) {
           duplicateVals.push(num)
           continue
       }
       nums.splice(i, 1)
       i--
   }
   return nums.length
}
```

**解法 2**

>  由于题目描述中指明为`排序数组`,所以不可能出现`[0, 0, 1, 2, 1]`这种数据，可以在循环中比较`当前索引的值`和`前一个索引的值`来判断数字是否重复
>  时间复杂度 O(n)
>  循环里会多次执行`nums.splice(i, 1)` 有较大的性能消耗，所以leetcode检测效率也不高，比解法1略好

```
var removeDuplicates = function(nums) {
   if (nums.length <= 1) return nums.length
   for (let i = 1; i < nums.length; i++) {
       if (nums[i] === nums[i-1]) {
           nums.splice(i, 1)
           i--
       }
   }
   return nums.length
}
```

**解法 3——双指针法**（参考了官方题解）

>  
>  时间复杂度 O(n)
> 个人感觉，之所有效率大大提高了，是由于减少了对数组的插入和删除操作，
>  循环中都是进行赋值操作，并没有删除和插入操作
>  `nums.length = i + 1` 进行了一次尾部删除，时间复杂度应该是O(1)
```
var removeDuplicates = function(nums) {
   if (nums.length <= 1) return nums.length
   let i = 0
   for (let j = 1; j < nums.length; j++) {
       if (nums[i] !== nums[j]) {
           i++
           nums[i] = nums[j]
       }
   }
   nums.length = i + 1
   return i + 1
}
```




