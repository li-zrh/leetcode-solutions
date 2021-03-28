以下是文章模板，以 Leetcode 的《两数之和》问题为例：

# 两数之和

## 题目描述

题目：**两数之和**             难度：**简单**

给定一个整数数组 `nums` 和一个整数目标值 `target`，请你在该数组中找出 **和为目标值** 的那 **两个** 整数，并返回它们的数组下标。

你可以假设每种输入只会对应一个答案。但是，数组中同一个元素在答案里不能重复出现。

你可以按任意顺序返回答案。

**示例 1：**

输入：nums = [2,7,11,15], target = 9
输出：[0,1]
解释：因为 nums[0] + nums[1] == 9 ，返回 [0, 1] 。
**示例 2：**

输入：nums = [3,2,4], target = 6
输出：[1,2]
**示例 3：**

输入：nums = [3,3], target = 6
输出：[0,1]

**提示：**

- 2 <= nums.length <= 103
- -109 <= nums[i] <= 109
- -109 <= target <= 109
- **只会存在一个有效答案**

## 解题思路

本题虽然只是在搜索给定数组内是否存在唯一两个数字之和为给定数字，但是如果按照普通的两个循环搜索的话，时间复杂度会是 O(n<sup>2</sup>)。当数组的规模变大时，其所需的运行时间也会变得很大。所以需要使用 Hashmap 或者双指针这样的时间复杂度较低的方法。

### Hashmap 算法

HashMap （哈希表）是一个用于存储 Key-Value 键值对的集合，有点类似于 Redis 数据库的键值对。其中，每一个键值对称为 Entry，而这些 Entry 分散于一个数组当中，这个数组也就是 Hashmap 的主干。在 C++ 中，哈希表这种数据结构通过把关键码映射到表中一个位置来访问记录，以加快查找的速度，通常这个映射函数称为散列函数。哈希表中存在一个重要问题，即如何解决映射过程中发生的映射冲突问题。常用的方法有 **开放地址法** 和 **链地址法** 两种。在这道题中因为只存在一个答案，则不存在两个数字的映射地址相同，可以放心使用哈希表。如下图所示，初始化一个空的哈希表结构，然后开始遍历输入数组 nums，将 target-nums[i] 的值存储为哈希表对应序号的值。当遍历发现哈希表中所期待的值与当前遍历的数组值 nums[i] 相等时，输出包含哈希表的序号 j 和遍历的数组序号 i 的结果 result 数组。

![vgy.me](https://i.vgy.me/jz8vrD.png)

### Hashmap 算法复杂度分析

- 时间复杂度 O(n)，n 为数组的大小
- 空间复杂度 O(n)，n 为数组的大小

### 双指针算法

双指针利用的也是本题输入数组的一个特性：只存在一个有效答案。如下图所示，首先对输入数组进行拷贝，然后将数组排序为有序数组，这样就可以用一个指针指在开头、另一个指针指在末尾，在有序数组中利用双指针从左右向中间寻找，但两个指针重合时如若仍未找到答案，即证明不存在一个有效答案。如果存在一个有效答案，则会在两个指针重合之前找到符合要求的解。判断指针移动的依据是 **nums[i] + nums[j]** 和 **target** 的大小，当前者较大时，右指针左移，向更小的方向移动；当前者较小时，左指针右移，向更大的方向移动；当两者相等时，找到答案。需要注意的是，此时的答案并非是最终的答案，因为经过了排序现在的序号与输入数组的序号可能有所不同，需要到拷贝数组中找到对应 nums[i] 和 nums[j] 的下标，并对这两个下标进行排序（也可不排，题目说可以按照任何顺序返回答案）作为数组结果输出。

![vgy.me](https://i.vgy.me/SO7hBe.png)

### 双指针算法复杂度分析

- 时间复杂度 O(nlogn)，n 为数组的大小
- 空间复杂度 O(n)，n 为数组的大小

## 代码实现

### Hashmap C++ 实现

```cpp
// Leetcode0001_hashmap.cpp

class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        unordered_map<int, int> hash;
        vector<int> result(2,0);
        for (int i = 0; i < nums.size(); i++) {
            // 查找是否存在满足一个数 + nums[i] == target
            if (hash.count(nums[i]) > 0) {
                result[0] = hash[nums[i]];
                result[1] = i;
                return result;
            }
            hash[target - nums[i]] = i;
        }
        return result;
    }
};
```


### 双指针 C++ 实现

```cpp
//  Leetcode0001_dpointer.cpp

class Solution {
public:
    /**
     * @param numbers: An array of Integer
     * @param target: target = numbers[index1] + numbers[index2]
     * @return: [index1, index2] (index1 < index2)
     */
    vector<int> twoSum(vector<int> &numbers, int target) {
        vector<int> backUp = numbers;
        sort(numbers.begin(), numbers.end());
        int i = 0,j = numbers.size()-1;
        while (i < j) {
            // 找到答案
            if (numbers[i] + numbers [j] == target){
                break;
            }
            // 左指针右移
            else if (numbers[i] + numbers [j] < target){
                i += 1;
            }
            // 右指针左移
            else {
                j -= 1;
            }
        }
        int a = 0,b = 0;      // 标记是否找到，避免i，j值相同的情况
        for (int k = 0; k < numbers.size(); k++) {
            // 查找对应下标
            if (backUp[k] == numbers[i] && a == 0) {
                i = k;
                a = 1;
            }
            else if (backUp[k] == numbers[j] && b == 0) {
                j = k;
                b = 1;
            }
            else if (a == 1 && b == 1) {
                break;
            }
        }
        vector<int> ans;
        ans.push_back(i);
        ans.push_back(j);
        sort(ans.begin(), ans.end());
        return ans;
    }
};
```

### Hashmap Python 实现

```python
# Leetcode0001_hashmap.py

class Solution:
    """
    @param numbers: An array of Integer
    @param target: target = numbers[index1] + numbers[index2]
    @return: [index1, index2] (index1 < index2)
    """
    def twoSum(self, nums, target):
        um = dict()
        for i in range(len(nums)):
        # 查找是否存在满足一个数 + nums[i] == target
            if nums[i] in um:
                result=[]
                result.append(um[nums[i]])
                result.append(i)
                return result
            um[target-nums[i]] = i;
        return [0,0]
```

### 双指针 Python 实现

```python
# Leetcode0001_dpointer.py

class Solution:
    """
    @param numbers : An array of Integer
    @param target : target = numbers[index1] + numbers[index2]
    @return : [index1 + 1, index2 + 1] (index1 < index2)
    """
    def twoSum(self, numbers, target):
        backUp = numbers[:]
        numbers = sorted(numbers)
        i,j = 0,len(numbers) - 1
        while i < j:
            # 找到答案
            if numbers[i] + numbers [j] == target:
                break
            # 左指针右移
            elif numbers[i] + numbers [j] < target:
                i += 1
            # 右指针左移
            else:
                j -= 1
        a,b = 0,0    #   标记是否找到，避免i，j值相同的情况
        for k in range(len(backUp)):
            #查找对应下标
            if backUp[k] == numbers[i] and a == 0:
                i = k
                a = 1
            elif backUp[k] == numbers[j] and b == 0:
                j = k
                b = 1
            elif a == 1 and b == 1:
                break
        return sorted([i,j])
```

### Hashmap Java 实现

```java
// Leetcode0001_hashmap.java

public class Solution {
    /*
     * @param numbers : An array of Integer
     * @param target : target = numbers[index1] + numbers[index2]
     * @return : [index1 + 1, index2 + 1] (index1 < index2)
         numbers=[2, 7, 11, 15],  target=9
         return [1, 2]
     */
    public int[] twoSum(int[] numbers, int target) {
        HashMap<Integer,Integer> map = new HashMap<Integer,Integer>();
        int[] result = {0,0};
        for(int i=0;i<numbers.length;i++){
            // 查找是否存在满足一个数 + nums[i] == target
            if(map.get(numbers[i])!=null){
                int[] res = {map.get(numbers[i]),i};
                return res;
            }
            map.put(target-numbers[i],i);
        }
        return result;
    }
}
```

### 双指针 Java 实现

```java
// Leetcode0001_dpointer.java

public class Solution {
    /**
     * @param numbers: An array of Integer
     * @param target: target = numbers[index1] + numbers[index2]
     * @return: [index1, index2] (index1 < index2)
     */
    public int[] twoSum(int[] numbers, int target) {
        int[] backUp = new int[numbers.length];
        System.arraycopy(numbers, 0, backUp, 0, numbers.length);
        Arrays.sort(numbers);
        int i = 0,j = numbers.length-1;
        while (i < j) {
            // 找到答案
            if (numbers[i] + numbers [j] == target){
                break;
            }
            // 左指针右移
            else if (numbers[i] + numbers [j] < target){
                i += 1;
            }
            // 右指针左移
            else {
                j -= 1;
            }
        }
        int a = 0,b = 0;      // 标记是否找到，避免i，j值相同的情况
        for (int k = 0; k < numbers.length; k++) {
            // 查找对应下标
            if (backUp[k] == numbers[i] && a == 0) {
                i = k;
                a = 1;
            }
            else if (backUp[k] == numbers[j] && b == 0) {
                j = k;
                b = 1;
            }
            else if (a == 1 && b == 1) {
                break;
            }
        }
        int[] ans = new int[2];
        ans[0] = i;
        ans[1] = j;
        Arrays.sort(ans);
        return ans;

    }
}
```

## 参考资料

- [九章-小原 Leetcode 题解](https://www.jiuzhang.com/solution/two-sum/)
- [算法收集：HashMap的原理理解一](https://www.jianshu.com/p/cf253c8673a0)
- [C++ STL 之哈希表 | unordered_map](https://www.sczyh30.com/posts/C-C/cpp-stl-hashmap/)
- [C++ vector 容器浅析](https://www.runoob.com/w3cnote/cpp-vector-container-analysis.html)