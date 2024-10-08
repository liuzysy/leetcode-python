# LeetCode 热题100

## 一、哈希表

### LeetCode49. 字母异位词分组

给你一个字符串数组，请你将 `字母异位词` 组合在一起。可以按任意顺序返回结果列表。

`字母异位词` 是由重新排列源单词的所有字母得到的一个新单词。

* 示例 1:
    > 输入: `strs = ["eat", "tea", "tan", "ate", "nat", "bat"]`
    > 输出: `[["bat"],["nat","tan"],["ate","eat","tea"]]`


* 示例 2:

    > 输入: `strs = [""]`
    > 输出: `[[""]]`


* 示例 3:

    > 输入: `strs = ["a"]`
    > 输出: `[["a"]]`

#### 解法：哈希表解法
**解题思路：** 
* 哈希表（字典）
  * 利用哈希表的特性，将字母异位词分组。通过排序字符串生成唯一键，将所有相同键的字符串放入同一个列表中。

**解题步骤：**
* 初始化哈希表：创建一个空字典 `anagrams`，用于存储字母异位词的组合。
* 遍历字符串数组：
    * 排序字符串：将字符串中的字母排序，生成一个新的字符串作为键。
    * 检查键是否存在：
      * 如果存在，将当前字符串添加到该键对应的列表中。
      * 如果不存在，创建新的键，并将当前字符串初始化为该键的值列表。
* 返回结果：提取字典中的所有值（异位词组合）并返回。
```python
def groupAnagrams(strs):
    anagrams = {}  # 创建哈希表
    print("初始哈希表:", anagrams)

    for s in strs:
        key = ''.join(sorted(s))  # 将字符串排序，作为键
        print(f"当前字符串: {s}, 排序后的键: {key}")

        if key in anagrams:
            print("找到已有键:", key)
            anagrams[key].append(s)  # 添加到对应的列表
        else:
            print("未找到键，创建新键:", key)
            anagrams[key] = [s]  # 创建新键并初始化列表

        print("当前哈希表状态:", anagrams)

    result = list(anagrams.values())
    print("最终结果:", result)
    return result
```
**代码运行流程：**
1. **初始哈希表**:` {}`

2. **当前字符串**: `eat`
- **排序后的键**: `aet`
- **未找到键，创建新键**: `aet`
- **当前哈希表状态**: `{'aet': ['eat']}`

3. **当前字符串**: `tea`
- **排序后的键**: `aet`
- **找到已有键**: `aet`
- **当前哈希表状态**: `{'aet': ['eat', 'tea']}`

4. **当前字符串**: `tan`
- **排序后的键**: `ant`
- **未找到键，创建新键**: `ant`
- **当前哈希表状态**: `{'aet': ['eat', 'tea'], 'ant': ['tan']}`

5. **当前字符串**: `ate`
- **排序后的键**: `aet`
- **找到已有键**: `aet`
- **当前哈希表状态**:` {'aet': ['eat', 'tea', 'ate'], 'ant': ['tan']}`

6. **当前字符串**: `nat`
- **排序后的键**: `ant`
- **找到已有键**: `ant`
- **当前哈希表状态**: `{'aet': ['eat', 'tea', 'ate'], 'ant': ['tan', 'nat']}`

7. **当前字符串**: `bat`
- **排序后的键**: `abt`
- **未找到键，创建新键**: `abt`
- **当前哈希表状态**: `{'aet': ['eat', 'tea', 'ate'], 'ant': ['tan', 'nat'], 'abt': ['bat']}`

8. **最终结果**: `[['eat', 'tea', 'ate'], ['tan', 'nat'], ['bat']]`






