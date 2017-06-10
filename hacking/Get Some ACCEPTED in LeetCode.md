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

## 575. Distribute Candies

[Distribute Candies](https://leetcode.com/problems/distribute-candies/#/description)

* **My solution:**

Language: Lua

```lua
function distributeCandies(candies)
    local count = 0
    local sister = {}
    for i=1,#candies,1 do
        if sister[candies[i]] == nil and count < #candies/2 then
            count = count + 1
            sister[candies[i]] = i
        end
    end
    return count
end

local candies = {3, 3, 3, 3, 2, 4, 0, 0, 0, -3, 9, 7}
print(distributeCandies(candies))
```

* **Impressive solution:**

Language: Java

```java
public class Solution {
    public int distributeCandies(int[] candies) {
        Set<Integer> kinds = new HashSet<>();
        for (int candy : candies) kinds.add(candy);
        return kinds.size() >= candies.length / 2 ? candies.length / 2 : kinds.size();
    }
}
```

## 412. Fizz Buzz

[Fizz Buzz](https://leetcode.com/problems/fizz-buzz/#/description)

* **My solution:**

Language: Lua

```lua
function fizzBuzz(n)
    local list = {}
    for i=1,n do
        local str = ""
        if i % 3 == 0 then
            str = "Fizz"
        end
        if i % 5 == 0 then
            str = str .. "Buzz"
        end
        if str == "" then
            str = i
        end
        list[i] = str
    end
    return list
end

local n = 15
local list = fizzBuzz(n)
for i=1,#list do
    print(list[i])
end
```

* **Impressive solution:**

> Java 4ms solution , Not using "%" operation

```java
public class Solution {
    public List<String> fizzBuzz(int n) {
        List<String> ret = new ArrayList<String>(n);
        for(int i=1,fizz=0,buzz=0;i<=n ;i++){
            fizz++;
            buzz++;
            if(fizz==3 && buzz==5){
                ret.add("FizzBuzz");
                fizz=0;
                buzz=0;
            }else if(fizz==3){
                ret.add("Fizz");
                fizz=0;
            }else if(buzz==5){
                ret.add("Buzz");
                buzz=0;
            }else{
                ret.add(String.valueOf(i));
            }
        } 
        return ret;
    }
}
```

> C++ solution, 3ms

```c++
class Solution {
public:
    vector<string> fizzBuzz(int n) {
        vector<string> ret_vec(n);
        for(int i=1; i<=n; ++i)
        {
            if(i%3 == 0)
            {
                ret_vec[i-1] += string("Fizz");
            }
            if(i%5 == 0)
            {
                ret_vec[i-1] += string("Buzz");
            }
            if(ret_vec[i-1] == "")
            {
                ret_vec[i-1] += to_string(i);
            }
        }
        return ret_vec;
    }
};
```

## 344. Reverse String

[Reverse String](https://leetcode.com/problems/reverse-string/#/description)

* **My solution:**

Language: Lua

```lua
function reverseString(s)
    return string.reverse(s)
end

local s = "abcdefg"
print(reverseString(s))
```

* **Impressive solution:**

> Complexity Analysis

> Time Complexity: `O(n)` (Average Case) and `O(n)` (Worst Case) where `n` is the total number character in the input string. The algorithm need to reverse the whole string.

> Auxiliary Space: `O(n)` space is used where `n` is the total number character in the input string. Space is needed to transform string to character array.

```java
public class Solution {
    public String reverseString(String s) {
        char[] word = s.toCharArray();
        int i = 0;
        int j = s.length() - 1;
        while (i < j) {
            char temp = word[i];
            word[i] = word[j];
            word[j] = temp;
            i++;
            j--;
        }
        return new String(word);
    }
}
```

## 496. Next Greater Element I

[Next Greater Element I](https://leetcode.com/problems/next-greater-element-i/#/description)

* **My solution:**

Language: Lua

```lua
function nextGreaterElement(findNums, nums)
    local results = {}
    for i=1,#findNums do
        local hasFound = false
        for j=1,#nums do
            if hasFound == false and findNums[i] == nums[j] then
                hasFound = true
            else
                if hasFound == true and findNums[i] < nums[j] then
                    results[i] = nums[j]
                    break
                else
                    results[i] = -1
                end
            end
        end
    end
    return results
end

local findNums = {4, 1, 2}
local nums = {1, 3, 4, 2}
local results = nextGreaterElement(findNums, nums)
for i=1,#results do
    print(results[i])
end
```

* **Impressive solution:**

> Java 10 lines linear time complexity O(n) with explanation
> 
> Key observation:
> Suppose we have a decreasing sequence followed by a greater number
> For example [5, 4, 3, 2, 1, 6] then the greater number 6 is the next greater element for all previous numbers in the sequence
> We use a stack to keep a decreasing sub-sequence, whenever we see a number x greater than stack.peek() we pop all elements less than x and for all the popped ones, their next greater element is x
> For example [9, 8, 7, 3, 2, 1, 6]
> The stack will first contain [9, 8, 7, 3, 2, 1] and then we see 6 which is greater than 1 so we pop 1 2 3 whose next greater element should be 6

```java
public int[] nextGreaterElement(int[] findNums, int[] nums) {
    Map<Integer, Integer> map = new HashMap<>(); // map from x to next greater element of x
    Stack<Integer> stack = new Stack<>();
    for (int num : nums) {
        while (!stack.isEmpty() && stack.peek() < num)
            map.put(stack.pop(), num);
        stack.push(num);
    }   
    for (int i = 0; i < findNums.length; i++)
        findNums[i] = map.getOrDefault(findNums[i], -1);
    return findNums;
}
```

---

change log: 

	- 创建（2017-05-31）
	- 更新（2017-06-10）

---


