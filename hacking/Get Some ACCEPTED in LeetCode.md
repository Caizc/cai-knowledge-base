# Accepted Questiones in LeetCode.com

## 1. Two Sum

[Two Sum](https://leetcode.com/problems/two-sum/#/description)

* **My solution:**

Language: C#

```csharp
public class Solution {
    public int[] TwoSum(int[] nums, int target) {
        int[] result = new int[2];
        for(int i = 0; i < nums.Length-1; i++){
            for(int j = i+1; j < nums.Length; j++){
                if(nums[i] + nums[j] == target){
                    result[0] = i;
                    result[1] = j;
                    return result;
                }
            }
        }
        return null;
    }
}
```

Language: Lua

```lua
function TwoSum(nums, target)
    for i = 1, #nums do
        for j = i + 1, #nums do
            if nums[i] + nums[j] == target then
                return i - 1, j - 1
            end
        end     
    end
    return nil, nil
end
```

* **Impressive solution:**

Language: Java

```java
public int[] twoSum(int[] numbers, int target) {
    int[] result = new int[2];
    Map<Integer, Integer> map = new HashMap<Integer, Integer>();
    for (int i = 0; i < numbers.length; i++) {
        if (map.containsKey(target - numbers[i])) {
            result[1] = i + 1;
            result[0] = map.get(target - numbers[i]);
            return result;
        }
        map.put(numbers[i], i + 1);
    }
    return result;
}
```

## 461. Hamming Distance

[Hamming Distance](https://leetcode.com/problems/hamming-distance/#/description)

* **My solution:**

Language: Lua

```lua
function hammingDistance(a, b)
    local c = a ~ b
    local distance = 0
    for i = 31, 0, -1 do
        if c / 2^i >= 1 then
            c = c - 2^i
            distance = distance + 1
        end
    end
    return distance
end
```

* **Impressive solution:**

Language: Java

```java
public class Solution {
    public int hammingDistance(int x, int y) {
        return Integer.bitCount(x ^ y);
    }
}
```

## 561. Array Partition I

[Array Partition I](https://leetcode.com/problems/array-partition-i/#/description)

* **My solution:**

Language: C#

```csharp
public class Solution {
    public int ArrayPairSum(int[] nums) 
    {
        int sum = 0;
        Array.Sort(nums);
        for (int n = 0; n < nums.Length; n = n + 2)
        {
            sum += nums[n];
        }
        return sum;
    }
}
```

* **Impressive solution:**

Language: Java

```java
public class Solution {
    public int arrayPairSum(int[] nums) {
        Arrays.sort(nums);
        int result = 0;
        for (int i = 0; i < nums.length; i += 2) {
            result += nums[i];
        }
        return result;
    }
}
```

## 476. Number Complement

[Number Complement](https://leetcode.com/problems/number-complement/#/description)

* **My solution:**

Language: Lua

```lua
function findComplement(num)
    local result
    for i = 31, 0, -1 do
        if num / (2^i) >= 1 then
            result = num ~ (2^(i+1) - 1)
            break
        end
    end
    return result
end
```

* **Impressive solution:**

Language: Java

```java
public class Solution {
    public int findComplement(int num) {
        return ~num & (Integer.highestOneBit(num) - 1);
    }
}
```

## 557. Reverse Words in a String III

[Reverse Words in a String](https://leetcode.com/problems/reverse-words-in-a-string-iii/#/description)

* **My solution:**

Language: Lua

```lua
function reverseWords(s)
    i = i or 1
    result = result or ""
    local a, b = string.find(s, " ", i)
    if b == nil then
        result = result .. string.reverse(string.sub(s, i, #s))
        return
    end
    result = result .. string.reverse(string.sub(s, i, a - 1)) .. " "
    i = b + 1
    reverseWords(s)
    return result
end
```

* **Impressive solution:**

Language: Java

```java
public class Solution {
    public String reverseWords(String s) {
        char[] ca = s.toCharArray();
        for (int i = 0; i < ca.length; i++) {
            if (ca[i] != ' ') {   // when i is a non-space
                int j = i;
                while (j + 1 < ca.length && ca[j + 1] != ' ') { j++; } // move j to the end of the word
                reverse(ca, i, j);
                i = j;
            }
        }
        return new String(ca);
    }

    private void reverse(char[] ca, int i, int j) {
        for (; i < j; i++, j--) {
            char tmp = ca[i];
            ca[i] = ca[j];
            ca[j] = tmp;
        }
    }
}
```

## 566. Reshape the Matrix

[Reshape the Matrix](https://leetcode.com/problems/reshape-the-matrix/#/description)

* **My solution:**

Language: Lua

```lua
function matrixReshape(matrix, r, c)
    local result = {}
    local oRow = 0
    local oCol = 0
    local tempArray = {}
    local index = 0
    for k, v in pairs(matrix) do
        oRow = oRow + 1
        oCol = 0
        for k2, v2 in pairs(v) do
            index = index + 1
            oCol = oCol + 1
            tempArray[index] = v2
        end
    end
    print(oRow, oCol)
    if r * c == oRow * oCol then
        print(r, c)
        index = 0
        for i=1, r, 1 do
            local innerArray = {}
            for j=1, c, 1 do
                index = index + 1
                innerArray[j] = tempArray[index]
            end
            result[i] = innerArray
        end
    else
        result = matrix
    end
    return result
end

function printArray(array)
    local row = "["
    local firstRow = true
    for k, v in pairs(array) do
        if firstRow == true then
            firstRow = false
            row = row .. "["
        else
            row = row .. ",\n ["
        end
        local firstCol = true
        for k2, v2 in pairs(v) do
            if firstCol == true then
                row = row .. v2
                firstCol = false
            else
                row = row .. "," .. v2
            end
        end
        row = row .. "]"
    end
    row = row .. "]"
    print(row)
end

local matrix = {{7, 8, 9}, {10, 11, 12}, {13, 14, 15}, {16, 17, 18}}
local r = 2
local c = 6
local result = matrixReshape(matrix, r, c)
printArray(result)
```

* **Impressive solution:**

Language: Java

```java
public int[][] matrixReshape(int[][] nums, int r, int c) {
    int n = nums.length, m = nums[0].length;
    if (r*c != n*m) return nums;
    int[][] res = new int[r][c];
    for (int i=0;i<r*c;i++) 
        res[i/c][i%c] = nums[i/m][i%m];
    return res;
}
```

---

change log: 

	- 创建（2017-05-31）
	- 更新（2017-06-06）

---


