# Accepted Questions in LeetCode.com

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

## 463. Island Perimeter

[Island Perimeter](https://leetcode.com/problems/island-perimeter/#/description)

* **My solution:**

Language: Lua

```lua
function islandPerimeter(grid)
    local perimeter
    local islands = 0
    local neighbours = 0
    for i, row in pairs(grid) do
        for j, v in pairs(row) do
            if v == 1 then
                islands = islands + 1
            end
            if i > 1 then
                neighbours = neighbours + ((grid[i][j] | grid[i-1][j]) - (grid[i][j] ~ grid[i-1][j]))
            end
            if j > 1 then
                neighbours = neighbours + ((grid[i][j] | grid[i][j-1]) - (grid[i][j] ~ grid[i][j-1]))
            end
        end
    end
    print("islands: " .. islands)
    print("neighbours: " .. neighbours)
    perimeter = 4 * islands - 2 * neighbours
    return perimeter
end

local grid = {{
    0, 1, 0, 0
},{
    1, 1, 1, 0
},{
    0, 1, 0, 0
},{
    1, 1, 0, 0
}}
print(islandPerimeter(grid))
```

* **Impressive solution:**

> loop over the matrix and count the number of islands;
> if the current dot is an island, count if it has any right neighbour or down neighbour;
> the result is islands * 4 - neighbours * 2

```java
public class Solution {
    public int islandPerimeter(int[][] grid) {
        int islands = 0, neighbours = 0;
        for (int i = 0; i < grid.length; i++) {
            for (int j = 0; j < grid[i].length; j++) {
                if (grid[i][j] == 1) {
                    islands++; // count islands
                    if (i < grid.length - 1 && grid[i + 1][j] == 1) neighbours++; // count down neighbours
                    if (j < grid[i].length - 1 && grid[i][j + 1] == 1) neighbours++; // count right neighbours
                }
            }
        }
        return islands * 4 - neighbours * 2;
    }
}
```

## 292. Nim Game

[Nim Game](https://leetcode.com/problems/nim-game/#/description)

* **My solution:**

Language: Lua

```lua
function canWinNim(n)
    return n % 4 ~= 0
end

local n = 4
print(canWinNim(n))
```

* **Impressive solution:**

> The first one who got the number that is multiple of 4 (i.e. n % 4 == 0) will lost, otherwise he/she will win.

```java
public boolean canWinNim(int n) {    
    return n % 4 != 0 ;
}
```

## 485. Max Consecutive Ones

[Max Consecutive Ones](https://leetcode.com/problems/max-consecutive-ones/#/description)

* **My solution:**

Language: Lua

```lua
function findMaxConsecutiveOnes(nums)
    local maxCount = 0
    local temp = 0
    for i=1,#nums do
        if nums[i] == 1 then
            temp = temp + 1
        else
            temp = 0
        end
        if temp > maxCount then
            maxCount = temp
        end
    end
    return maxCount
end

local nums = {0, 1, 1, 0, 0, 1, 1, 1}
print(findMaxConsecutiveOnes(nums))
```

* **Impressive solution:**

> The idea is to reset maxHere to 0 if we see 0, otherwise increase maxHere by 1.

```java
public int findMaxConsecutiveOnes(int[] nums) {
    int maxHere = 0, max = 0;
    for (int n : nums)
        max = Math.max(max, maxHere = n == 0 ? 0 : maxHere + 1);
    return max; 
} 
```

## 136. Single Number

[Single Number](https://leetcode.com/problems/single-number/#/description)

* **My solution:**

Language: Lua

```lua
function singleNumber(nums)
    local result = 0
    for i=1,#nums do
        result = result ~ nums[i]
    end
    return result
end

local nums = {1, 2, 3, 3, 1, 5, 2}
print(singleNumber(nums))
```

* **Impressive solution:**

> Known that A XOR A = 0 and the XOR operator is commutative, the solution will be very straightforward.

```java
int singleNumber(int A[], int n) {
    int result = 0;
    for (int i = 0; i<n; i++)
    {
		result ^=A[i];
    }
	return result;
}
```

## 606. Construct String from Binary Tree

[Construct String from Binary Tree](https://leetcode.com/problems/construct-string-from-binary-tree/#/description)

* **My solution:**

Language: Lua

```lua
local treeNode = {
    val,
    left,
    right
}

function treeNode:new(val)
    t = t or {}
    setmetatable(t, self)
    self.__index = self
    self.val = val
    return t
end

function createBinaryTree(nums, i, str)
    if i > #nums then
        return nil, str
    end

    local node = treeNode:new(nums[i])

    if i == 1 then
        str = str .. node.val
    else
        if node.val ~= nil and node.val ~= -1 then
            str = str .. "(" .. node.val
        else
            str = str .. "()"
            return node, str
        end  
    end

    node.left, str = createBinaryTree(nums, 2 * i, str)
    node.right, str = createBinaryTree(nums, 2 * i + 1, str)

    if i ~= 1 then
        str = str .. ")"
    end

    return node, str
end

function tree2str(nums)
    local _, str = createBinaryTree(nums, 1, "")
    return str
end

local nums = {1, 2, 3, -1, 4}
print(tree2str(nums))
```

* **Impressive solution:**

> Java Solution, Tree Traversal

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
 public class Solution {
    public String tree2str(TreeNode t) {
        if (t == null) return "";
        String result = t.val + "";
        String left = tree2str(t.left);
        String right = tree2str(t.right);
        if (left == "" && right == "") return result;
        if (left == "") return result + "()" + "(" + right + ")";
        if (right == "") return result + "(" + left + ")";
        return result + "(" + left + ")" + "(" + right + ")";
    }
}
```

## 520. Detect Capital

[Detect Capital](https://leetcode.com/problems/detect-capital/#/description)

* **My solution:**

Language: Lua

```lua
function detectCapitalUse(word)
    local pattern1 = "%u+"
    local pattern2 = "%l+"
    local pattern3 = "%u%l+"
    local a1, b1 = string.find(word, pattern1)
    if a1 == 1 and b1 == #word then
        return true
    end
    local a2, b2 = string.find(word, pattern2)
    if a2 == 1 and b2 == #word then
        return true
    end
    local a3, b3 = string.find(word, pattern3)
    if a3 == 1 and b3 == #word then
        return true
    end
    return false
end

local word1 = "USA"
print(word1, detectCapitalUse(word1))
local word2 = "leetcode"
print(word2, detectCapitalUse(word2))
local word3 = "Google"
print(word3, detectCapitalUse(word3))
local word4 = "FlaG"
print(word4, detectCapitalUse(word4))
```

* **Impressive solution:**

> ASCII 码

```java
public class Solution {
    public boolean detectCapitalUse(String word) {
        int cnt = 0;
        for(char c: word.toCharArray()) if('Z' - c >= 0) cnt++;
        return ((cnt==0 || cnt==word.length()) || (cnt==1 && 'Z' - word.charAt(0)>=0));
    }
}
```

> 正则表达式

```java
public boolean detectCapitalUse(String word) {
    return word.matches("[A-Z]+|[a-z]+|[A-Z][a-z]+");
}
```

## 104. Maximum Depth of Binary Tree

[Maximum Depth of Binary Tree](https://leetcode.com/problems/maximum-depth-of-binary-tree/#/description)

* **My solution:**

Language: Lua

```lua
local treeNode = {
    val,
    left,
    right
}

function treeNode:new(val)
    t = t or {}
    setmetatable(t, self)
    self.__index = self
    self.val = val
    return t
end

function createBinaryTree(nums, i, count)
    if i > #nums then
        return nil, count
    end

    local node = treeNode:new(nums[i])

    if node.val ~= nil and node.val ~= -1 then
        count = count + 1
        local leftDepth
        local rightDepth
        node.left, leftDepth = createBinaryTree(nums, 2 * i, count)
        node.right, rightDepth = createBinaryTree(nums, 2 * i + 1, count)
        return node, math.max(leftDepth, rightDepth)
    else
        return nil, count
    end  
end

function maxDepth(nums)
    local _, count = createBinaryTree(nums, 1, 0)
    return count
end

local nums = {1, 2, 3, -1, 5, 6, -1, -1, -1, 10}
print(maxDepth(nums))
```

* **Impressive solution:**

> if the node does not exist, simply return 0. Otherwise, return the 1+the longer distance of its subtree.

```java
public int maxDepth(TreeNode root) {
    if(root==null){
        return 0;
    }
    return 1 + Math.max(maxDepth(root.left),maxDepth(root.right));
}
```

## 448. Find All Numbers Disappeared in an Array

[Find All Numbers Disappeared in an Array](https://leetcode.com/problems/find-all-numbers-disappeared-in-an-array/#/description)

* **My solution:**

Language: Lua

```lua
function findDisappearedNumbers(nums)
    local result = {}
    local temp = {}
    for i=1,#nums do
        temp[nums[i]] = 0
    end
    local j = 0
    for i=1,#nums do
        if temp[i] ~= 0 then
            j = j + 1
            result[j] = i
        end
    end
    return result
end

local nums = {4, 3, 2, 8, 8, 2, 3, 1}
local result = findDisappearedNumbers(nums)
for i=1,#result do
    print(result[i])
end
```

* **Impressive solution:**

> The basic idea is that we iterate through the input array and mark elements as negative using `nums[nums[i] -1] = -nums[nums[i]-1]`. In this way all the numbers that we have seen will be marked as negative. In the second iteration, if a value is not marked as negative, it implies we have never seen that index before, so just add it to the return list.

```java
public List<Integer> findDisappearedNumbers(int[] nums) {
    List<Integer> ret = new ArrayList<Integer>();
    for(int i = 0; i < nums.length; i++) {
        int val = Math.abs(nums[i]) - 1;
        if(nums[val] > 0) {
            nums[val] = -nums[val];
        }
    }
    for(int i = 0; i < nums.length; i++) {
        if(nums[i] > 0) {
            ret.add(i+1);
        }
    }
    return ret;
}
```

## 389. Find the Difference

[Find the Difference](https://leetcode.com/problems/find-the-difference/#/description)

* **My solution:**

Language: Lua

```lua
function findTheDifference(s, t)
    local result = 0
    local byte = string.byte
    for i=1,string.len(s) do
        result = result ~ byte(s, i, i)
    end    
    for i=1,string.len(t) do
        result = result ~ byte(t, i, i)
    end
    return string.char(result)
end

local s = "abcd"
local t = "cdeab"
print(findTheDifference(s, t))
```

* **Impressive solution:**

> Java solution using bit manipulation

```java
public char findTheDifference(String s, String t) {
	char c = 0;
	for (int i = 0; i < s.length(); ++i) {
		c ^= s.charAt(i);
	}
	for (int i = 0; i < t.length(); ++i) {
		c ^= t.charAt(i);
	}
	return c;
}
```

> maybe a more elegant version

```java
public char findTheDifference(String s, String t) {
	int n = t.length();
	char c = t.charAt(n - 1);
	for (int i = 0; i < n - 1; ++i) {
		c ^= s.charAt(i);
		c ^= t.charAt(i);
	}
	return c;
}
```

## 226. Invert Binary Tree

[Invert Binary Tree](https://leetcode.com/problems/invert-binary-tree/#/description)

* **My solution:**

Language: Lua

```lua
local treeNode = {
    val,
    left,
    right
}

function treeNode:new(val)
    t = t or {}
    setmetatable(t, self)
    self.__index = self
    self.val = val
    return t
end

function createBinaryTree(nums, i, str)
    if i > #nums then
        return nil, str
    end

    local node = treeNode:new(nums[i])

    if i == 1 then
        str = str .. node.val
    else
        if node.val ~= nil and node.val ~= -1 then
            str = str .. "(" .. node.val
        else
            str = str .. "()"
            return node, str
        end  
    end

    node.left, str = createBinaryTree(nums, 2 * i + 1, str)
    node.right, str = createBinaryTree(nums, 2 * i, str)

    if i ~= 1 then
        str = str .. ")"
    end

    return node, str
end

function invertTree(nums)
    local _, str = createBinaryTree(nums, 1, "")
    return str
end

local nums = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10}
print(invertTree(nums))
```

* **Impressive solution:**

> recursive DFS solution

```java
public class Solution {
    public TreeNode invertTree(TreeNode root) {
        if (root == null) {
            return null;
        }
        final TreeNode left = root.left,  right = root.right;
        root.left = invertTree(right);
        root.right = invertTree(left);
        return root;
    }
}
```

> The above solution is correct, but it is also bound to the application stack, which means that it's no so much scalable - (you can find the problem size that will overflow the stack and crash your application), so more robust solution would be to use stack data structure.

```java
public class Solution {
    public TreeNode invertTree(TreeNode root) {      
        if (root == null) {
            return null;
        }
        final Deque<TreeNode> stack = new LinkedList<>();
        stack.push(root);
        while(!stack.isEmpty()) {
            final TreeNode node = stack.pop();
            final TreeNode left = node.left;
            node.left = node.right;
            node.right = left;
            if(node.left != null) {
                stack.push(node.left);
            }
            if(node.right != null) {
                stack.push(node.right);
            }
        }
        return root;
    }
}
```

> we can easly convert the above solution to BFS - or so called level order traversal.

```java
public class Solution {
    public TreeNode invertTree(TreeNode root) {
        if (root == null) {
            return null;
        }
        final Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);
        while(!queue.isEmpty()) {
            final TreeNode node = queue.poll();
            final TreeNode left = node.left;
            node.left = node.right;
            node.right = left;
            if(node.left != null) {
                queue.offer(node.left);
            }
            if(node.right != null) {
                queue.offer(node.right);
            }
        }
        return root;
    }
}
```

## 371. Sum of Two Integers

[Sum of Two Integers](https://leetcode.com/problems/sum-of-two-integers/#/description)

* **My solution:**

Language: Lua

```lua
function getSum(a, b)
    if b == 0 then
        return a
    else
        return getSum(a ~ b, (a & b) << 1)
    end
end

local a = 1
local b = 3
print(getSum(a, b))
```

* **Impressive solution:**

[A summary: How to use bit manipulation to solve problems easily and efficiently - LeetCode.com](https://discuss.leetcode.com/topic/50315/a-summary-how-to-use-bit-manipulation-to-solve-problems-easily-and-efficiently)

[Java simple easy understand solution with explanation](https://discuss.leetcode.com/topic/49771/java-simple-easy-understand-solution-with-explanation)

```java
// Iterative
public int getSum(int a, int b) {
	if (a == 0) return b;
	if (b == 0) return a;
	while (b != 0) {
		int carry = a & b;
		a = a ^ b;
		b = carry << 1;
	}
	return a;
}

// Iterative
public int getSubtract(int a, int b) {
	while (b != 0) {
		int borrow = (~a) & b;
		a = a ^ b;
		b = borrow << 1;
	}
	return a;
}

// Recursive
public int getSum(int a, int b) {
	return (b == 0) ? a : getSum(a ^ b, (a & b) << 1);
}

// Recursive
public int getSubtract(int a, int b) {
	return (b == 0) ? a : getSubtract(a ^ b, (~a & b) << 1);
}

// Get negative number
public int negate(int x) {
	return ~x + 1;
}
```

---

change log: 

	- 创建（2017-05-31）
	- 更新（2017-06-20）

---


