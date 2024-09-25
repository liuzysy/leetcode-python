# LeetCode 热题100

## 一、哈希表

### LeetCode1. 两数之和

给定一个整数数组 `nums` 和一个整数目标值 `target`，请你在该数组中找出和为目标值 `target` 的那两个整数，并返回它们的数组下标。

你可以假设每种输入只会对应一个答案，并且你不能使用两次相同的元素。

你可以按任意顺序返回答案。

* 示例 1:
    > 输入: nums = [2,7,11,15], target = 9  
    > 输出: [0,1]  
    > 解释: 因为 nums[0] + nums[1] == 9，返回 [0,1]。


* 示例 2:

    > 输入: nums = [3,2,4], target = 6  
    > 输出: [1,2]  


* 示例 3:

    > 输入: nums = [3,3], target = 6  
    > 输出: [0,1]

#### 解法1：暴力解法
思路：使用两个嵌套循环遍历所有可能的数对，检查它们的和是否等于目标值。
```python
def twoSum(nums, target):
    # 定义一个函数，接受一个整数数组 nums 和一个整数 target
    for i in range(len(nums)):
        # 外层循环遍历数组中的每个元素 i
        for j in range(i + 1, len(nums)):
            # 内层循环从 i + 1 开始，遍历数组中剩余的元素 j
            if nums[i] + nums[j] == target:
                # 检查 nums[i] 和 nums[j] 的和是否等于 target
                return [i, j]
                # 如果找到符合条件的两个数，返回它们的下标 [i, j]
```

- **时间复杂度**：O(n²)
- **空间复杂度**：O(1)
  
**解法**：

- 外层循环遍历每个元素 `i`，内层循环从 `i + 1` 开始遍历每个元素 `j`。
- 对于每一对 `nums[i]` 和 `nums[j]`，我们检查它们的和是否等于 `target`。
- 如果找到了，返回它们的下标 `[i, j]`。


#### 解法2：哈希表解法
**进阶：** 你可以想出一个时间复杂度小于 `O(n²)` 的算法吗？
**思路：** 利用哈希表存储每个元素及其下标，以便在遍历过程中快速查找补数。

```python
def twoSum(nums, target):
    # 初始化一个空的哈希表，用于存储每个元素及其对应的下标
    num_to_index = {}
    # 使用 enumerate 遍历数组 nums，i 是下标，num 是当前元素
    for i, num in enumerate(nums):
        # 计算当前元素的补数
        complement = target - num
        # 检查补数是否已经存在于哈希表中
        if complement in num_to_index:
            # 如果存在，返回补数的下标和当前元素的下标
            return [num_to_index[complement], i]
        # 如果补数不在哈希表中，将当前元素及其下标存入哈希表
        num_to_index[num] = i
```

- **时间复杂度**：O(n)
- **空间复杂度**：O(n)

**解法**：

1. **创建哈希表**：`num_to_index = {}`
   - 初始化一个空的哈希表，用于存储每个元素及其对应的下标。

2. **遍历数组**：`for i, num in enumerate(nums):`
   - 使用 `enumerate` 遍历数组 `nums`，`i` 是下标，`num` 是当前元素。

3. **计算补数**：`complement = target - num`
   - 计算当前元素的补数，即需要的另一个数，使得二者之和等于 `target`。

4. **检查补数**：`if complement in num_to_index:`
   - 检查补数是否已经存在于哈希表中。如果存在，说明找到了符合条件的数对。

5. **返回结果**：`return [num_to_index[complement], i]`
   - 如果找到，返回补数的下标和当前元素的下标。

6. **更新哈希表**：`num_to_index[num] = i`
   - 如果补数不在哈希表中，将当前元素及其下标存入哈希表，供后续查找。
