---
description: 哈希表
---

# 1. 两数之和

### Question

[https://leetcode.cn/problems/two-sum/](https://leetcode.cn/problems/two-sum/)

给定一个整数数组 `nums` 和一个整数目标值 `target`，请你在该数组中找出 **和为目标值** _`target`_  的那 **两个** 整数，并返回它们的数组下标。

你可以假设每种输入只会对应一个答案。但是，数组中同一个元素在答案里不能重复出现。

你可以按任意顺序返回答案。

&#x20;

**示例 1：**

<pre><code>输入：nums = [2,7,11,15], target = 9
<strong>输出：
</strong>[0,1]
<strong>解释：
</strong>因为 nums[0] + nums[1] == 9 ，返回 [0, 1] 。
</code></pre>

**示例 2：**

<pre><code>输入：nums = [3,2,4], target = 6
<strong>输出：
</strong>[1,2]
</code></pre>

**示例 3：**

<pre><code>输入：nums = [3,3], target = 6
<strong>输出：
</strong>[0,1]
</code></pre>

&#x20;

**提示：**

* `2 <= nums.length <= 104`
* `-109 <= nums[i] <= 109`
* `-109 <= target <= 109`
* **只会存在一个有效答案**

**进阶：**你可以想出一个时间复杂度小于 `O(n2)` 的算法吗？

### Solution

#### 暴力法

可以使用嵌套循环查找满足条件的答案。

<pre class="language-java"><code class="lang-java"><strong>class Solution {
</strong>    public int[] twoSum(int[] nums, int target) {
        for(int i = 0; i &#x3C; nums.length; i++) {
            for(int j = 1; j &#x3C; nums.length; j++) {
                if(nums[i] + nums[j] == target) {
                    return new int[]{i,j};
                }
            }
        }
        return null;
    }
}
</code></pre>

**时间复杂度**

&#x20;$$O(n^2)$$, $$n$$是数组$$nums$$的长度。

**空间复杂度**

$$O(1)$$, 不需要使用额外空间。

#### 使用Map

我们声明一个Map，用来存储数字和该数字对应下标。

我们遍历数组，每次遍历时用`target`减去`nums[i]`得到**剩余数字**，然后查找**剩余数字**是否在Map中。如果在Map，则返回**剩余数字**的下标和**当前下标**；如果不在Map中，则将**当前数字**和**当前下标**写入Map。

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        var map = new HashMap<Integer, Integer>();
        for(var i = 0; i < nums.length; i++) {
            var remain = target - nums[i];
            if(map.containsKey(remain)) {
                return new int[] {map.get(remain), i};
            } 
            map.put(nums[i], i);
        }
        return null;
    }
}
```

**时间复杂度**

&#x20;$$O(n)$$, $$n$$是数组$$nums$$的长度。

**空间复杂度**

&#x20;$$O(n)$$, $$n$$是数组$$nums$$的长度。
