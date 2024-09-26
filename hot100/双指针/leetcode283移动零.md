# LeetCode 热题100

## 二、双指针

### LeetCode283. 移动零

给定一个数组 `nums`，编写一个函数将所有 `0` 移动到数组的末尾，同时保持非零元素的相对顺序。

* 示例 1:
    > 输入: `nums = [0,1,0,3,12]`
    > 输出: `[1,3,12,0,0]`


* 示例 2:

    > 输入: `nums = [0]`
    > 输出: `[0]`

#### 解法：使用双指针

**解题思路：** 
可以用`双指针`或`快慢指针`的方法在 `O(n)` 时间内解决这个问题。关键是要通过一次遍历，将非零元素移动到数组前面，并把多余的位置补上`0`。

**双指针（快慢指针）法：**
* 使用两个指针：一个指针用于遍历数组，另一个指针用于记录非零元素应该放置的位置。
* 遍历数组时，如果遇到非零元素，将其移动到慢指针的位置，同时慢指针向前移动一位。遍历完数组后，慢指针之后的所有位置都用 0 填充。
```python
def moveZeroes(nums):
    noneZero = 0
    for current_point in range(len(nums)):
        if nums[current_point] != 0:
            nums[noneZero], nums[current_point] = nums[current_point], nums[noneZero]
            noneZero += 1
```

**详细解释：**
1. 初始化 noneZero 指针：
    * noneZero 变量用于记录当前非零元素应该放置的位置。
    * 初始值为 0，表示从数组的最左边开始。
2. 遍历整个数组：
    * for current_point in range(len(nums)): 这里的 current_point 是快指针，用于遍历数组中的每个元素。
3. 判断是否为非零元素：
    * if nums[current_point] != 0: 如果当前元素不是零，则需要把它移动到 noneZero 指针所指的位置。
4. 交换操作：
    * nums[noneZero], nums[current_point] = nums[current_point], nums[noneZero]: 如果当前元素是非零，则将其与 noneZero 指针所在的元素进行交换。即使 noneZero 和 current_point 指向同一个位置，交换操作也不会出错。
5. 移动 noneZero 指针：
    * noneZero += 1: 每次处理一个非零元素后，noneZero 向右移动一位，为下一个非零元素留出位置。

**核心思想：**
* `交换思想`：当找到非零元素时，将其与当前 noneZero 指针位置的元素进行交换。由于 noneZero 是递增的，所以交换后，noneZero 之前的所有元素都是非零元素。
* `一次遍历`：通过一次遍历即可完成非零元素的移动，整个过程没有多余的空间开销。

**例子解析：**
假设输入数组为 [0, 1, 0, 3, 12]，执行过程如下：

1. 初始状态：noneZero = 0，current_point = 0

    * nums[0] = 0，跳过，noneZero 不动。
2. 第二次循环：noneZero = 0，current_point = 1

    * nums[1] = 1，与 nums[0] 交换，数组变为 [1, 0, 0, 3, 12]，noneZero 增加到 1。
3. 第三次循环：noneZero = 1，current_point = 2

    * nums[2] = 0，跳过，noneZero 不动。
4. 第四次循环：noneZero = 1，current_point = 3

    * nums[3] = 3，与 nums[1] 交换，数组变为 [1, 3, 0, 0, 12]，noneZero 增加到 2。
5. 第五次循环：noneZero = 2，current_point = 4

    * nums[4] = 12，与 nums[2] 交换，数组变为 [1, 3, 12, 0, 0]，noneZero 增加到 3。

最终数组为 [1, 3, 12, 0, 0]，达到了移动零的效果。

**复杂度分析：**
* 时间复杂度：`O(n)`，因为我们只遍历了一次数组。
* 空间复杂度：`O(1)`，我们只用了常数空间，没有额外的数组存储数据。