### 题目描述
**11. 盛最多水的容器**
![avatar](https://aliyun-lc-upload.oss-cn-hangzhou.aliyuncs.com/aliyun-lc-upload/uploads/2018/07/25/question_11.jpg)
给定 n 个非负整数 a1，a2，...，an，每个数代表坐标中的一个点 (i, ai) 。在坐标内画 n 条垂直线，垂直线 i 的两个端点分别为 (i, ai) 和 (i, 0)。找出其中的两条线，使得它们与 x 轴共同构成的容器可以容纳最多的水。

> 说明：你不能倾斜容器，且 n 的值至少为 2。

[Leetcode 原题地址](https://leetcode-cn.com/problems/container-with-most-water/)

**示例 1:**
> 输入: [1,8,6,2,5,4,8,3,7]
> 输出: 49



**说明:**
为什么返回数值是整数，但输出的答案是数组呢?
请注意，输入数组是以“引用”方式传递的，这意味着在函数里修改输入数组对于调用者是可见的。

**暴力法**

>两重循环，比较获取最大值
>时间复杂度 O(n²)

```
var maxArea = function(height) {
    let max = 0
    let len = height.length
    for (let i = 0; i < len - 1; i++) {
        // 由于是计算2根柱子之间的空间，i 的取值范围 0 ~ len - 2
        // j 的取值范围 1 ~ len - 1    
        for (let j = i + 1; j < len; j++) {
            let w = j - i
            let h = Math.min(height[i], height[j])
            max = Math.max(max, w * h)
        }
    }
    return max
}
```

**双指针法（参考了官方题解）**

>通过比较最左侧柱子和最右侧柱子，不断向中间查找最大值
>时间复杂度 O(n)

```
var maxArea = function(height) {
   if (height.length < 2) return 0
    let end = height.length - 1 // 最右侧柱子索引
    let start = 0 // 最左侧柱子索引
    let max = 0 // 可容纳水的最大值
    while (start < end) {
        let w = end - start
        let h = Math.min(height[start], height[end])
        max = Math.max(max,  w * h)
        // 比较最左侧柱子的高度和最右侧柱子的高度
        // 哪一侧柱子高，表示该侧暂时为能够容纳足够多的水的柱子
        // 另一侧向中间查找更高的柱子，左侧+1，右侧-1
        if (height[start] < height[end]) {
            start++
        } else {
            end--
        }
    }
    return max
}
```




