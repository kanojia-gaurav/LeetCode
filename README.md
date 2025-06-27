## LeetCode


- **valid-palindrome** [link](https://leetcode.com/problems/valid-palindrome/description/)
```
#please note this solution is done using the two pointer approach.
import re
def isPalindrome(s: str) -> bool:
    str = s.lower()
    str = re.sub(r'[^a-zA-Z0-9\s]', '', str)
    str = str.replace(" ", "")
    left, right = 0, len(str)-1
    while left < right:
        if str[left] !=  str[right]:
            return False
        left += 1
        right -=1
    return True
    

print(isPalindrome("0P")) 
print(isPalindrome("A man, a plan, a canal: Panama"))
```


- **palindrome-number** [link](https://leetcode.com/problems/palindrome-number/)
```#please note this solution is done using the two pointer approach.

def isPalindrome(x: int) -> bool:
    x = list(str(x))

    left, right = 0, len(x)-1
    while left < right:
        if x[left] != x[right]:
            return False
        left +=1
        right -=1

    return True
    
print(isPalindrome(121))
```

- **longest palindrome in a string**
```
# longest palindrome in a string
s = "abccccdd"
c = []
longest = ""
n= len(s)
for i in range(n):
    for j in range(i + 1, n + 1):
        substring = s[i:j]
        if substring == substring[::-1]:
            if len(substring) > len(longest):
                longest = substring
print(longest)
```


- **Two Sum - unsorted array** [link](https://leetcode.com/problems/two-sum/description/)
```
        hash_map = {}
        res = []

        for i, num in enumerate(nums):
            sum = target - num
            if sum in hash_map:
                res.append(hash_map[sum])
                res.append(i)
                return res
            hash_map[num] = i
```


```			
finding the duplicates in an array:
    def hasDuplicate(self, nums: List[int]) -> bool:
        d={}
        for i, value in enumerate(nums):
            if value in d:
                d[value] +=1
                if d[value] > 1:
                    return True
            else:
                d[value] =1
        return False
```

- **valid-anagram** [link](https://leetcode.com/problems/valid-anagram/)
```
    def isAnagram(self, s: str, t: str) -> bool:
        s1 = [0]*26
        s2 = [0]*26

        for char in s:
            s1[ord(char) - 97] +=1
        for char in t:
            s2[ord(char) - 97] +=1
        
        if s1 == s2:
            return True
        else:
            return False
```

- **two-integer-sum** [link](https://neetcode.io/problems/two-integer-sum?list=neetcode150)
```
    def twoSum(self, nums: List[int], target: int) -> List[int]:

        hash_map = {}
        res = []

        for i, value in enumerate(nums):
            sum = target - value
            if sum in hash_map:
                res.append(hash_map[sum])
                res.append(i)
                return res
            hash_map[value] = i
```

- ** group-anagrams ** [link](https://leetcode.com/problems/group-anagrams/description/)
```

class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        res = defaultdict(list)

        for s in strs:
            count = [0] * 26
            for c in s:
                count[ord(c) - ord("a")] +=1

            res[tuple(count)].append(s)
        return list(res.values())
```		
- ** top-k-frequent-elements ** [link](https://leetcode.com/problems/top-k-frequent-elements/description/)
```
class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        count = Counter(nums).items()
        bucket = [[] for i in range(len(nums) + 1) ]
        # print(bucket)

        for num, freq  in count:
            bucket[freq].append(num)

        # print(bucket)

        l = [j for i in bucket for j in i ]
        # print(l)

        return l[::-1][:k]

```

- **string-encode-and-decode** [link](https://neetcode.io/problems/string-encode-and-decode?list=neetcode150)
```
class Solution:

    def encode(self, strs: List[str]) -> str:
        res = ""
        for i in strs:
            res +=  str(len(i)) + "#" + i
        return res

    def decode(self, s: str) -> List[str]:
        # pass
        res, i = [], 0

        while i<len(s):
            j = i
            while s[j] != "#":
                j +=1
            length = int(s[i:j])
            res.append(s[j+1: j+1+length])
            i =  j +1+ length
        return res
```

- **products-of-array-discluding-self**  [link](https://neetcode.io/problems/products-of-array-discluding-self?list=neetcode150)
```
#note this will give us TLE because its a brute force approach
class Solution:
    def productExceptSelf(self, nums: List[int]) -> List[int]:

        res1, res2 = [], []
        for i in range(len(nums)):
            res1.append(nums[i+1:])
            res2.append(nums[:i])
        # print(res1)
        # print(res2)

        l = []
        for i in range(len(res1)):
            k = 1
            for j in res1[i]:
                k = k * j
            l.append(k)
            # print(l)
        l1 = []
        for i in range(len(res2)):
            k = 1
            for j in res2[i]:
                k = k * j
            l1.append(k)
            # print(l1)
        result = [ int(a) * int(b) for a, b in zip(l, l1)]
        return result


efficient result
class Solution:
    def productExceptSelf(self, nums: List[int]) -> List[int]:

        res = [1] * (len(nums))

        prefex = 1
        for i in range(len(nums)):
            res[i] = prefex
            prefex *= nums[i]
            # print(res)

        postfix = 1
        for i in range(len(nums) -1, -1, -1):
            res[i] *= postfix
            postfix *=nums[i]
            # print(res)

        return res

```
- **happy number** [link](https://leetcode.com/problems/happy-number/description/)
```
class Solution:
    def isHappy(self, n: int) -> bool:
        seen = set()
        s = str(n)

        while s not in seen:
            seen.add(s)
            sum = 0
            for i in s:
                sum += int(i) **2

            if sum == 1: 
                return True
            s = str(sum)
        return False
```

- ** Valid Parentheisis ** [link](https://leetcode.com/problems/valid-parentheses/)
```
class Solution:
    def isValid(self, s: str) -> bool:
        stack = []
        open_b = "({["

        for char in s:
            if char in open_b:
                stack.append(char)
            else:
                if stack:
                    open = stack.pop()
                else:
                    return False
                
                if char ==')':
                    if open == '(':
                        continue
                    else:
                        return False
                elif char == '}':
                    if open == '{':
                        continue
                    else:
                        return False
                elif char == ']':
                    if open == '[':
                        continue
                    else:
                        return False
        if stack:
            return False
        else:
            return True
```

- ** longest-consecutive-sequence ** [link](https://leetcode.com/problems/longest-consecutive-sequence/description/)
```
class Solution:
    def longestConsecutive(self, nums: List[int]) -> int:
        numset = set(nums)
        longest = 0
        for n in numset:
            if (n - 1) not in numset:
                length = 0
                while(n + length) in numset:
                    length +=1
                longest = max(length, longest)
        return longest


```
- ** twoSum **
```
class Solution:
    def twoSum(self, numbers: List[int], target: int) -> List[int]:

        i, j = 0, len(numbers)-1

        while i < j:
            total_sum = numbers[i] + numbers[j]
            if total_sum > target:
                j -=1
            elif total_sum < target:
                i +=1
            else:
                return [i+1, j+1]
        return []
```	

## Sliding Window	

- ** /maximum-average-subarray-i ** [link](https://leetcode.com/problems/maximum-average-subarray-i/description/)
```
#### fixed length
class Solution:
    def findMaxAverage(self, nums: List[int], k: int) -> float:

        n = len(nums)
        cur_sum = 0
        for i in range(k):
            cur_sum +=nums[i]
        
        max_avg = cur_sum / k
        
        for i in range(k, n):
            cur_sum += nums[i]
            cur_sum -= nums[i-k]

            avg = cur_sum / k

            max_avg = max(avg, max_avg)

        return max_avg
```

- ** longest-substring-without-repeating-characters ** [link](https://leetcode.com/problems/longest-substring-without-repeating-characters/description/?envType=problem-list-v2&envId=sliding-window)
```
#### Variable leagth
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:

        sett = set()
        longest = 0
        l = 0
        for r in range(len(s)):

            while s[r] in sett:
                sett.remove(s[l])
                l +=1
            
            w = (r-l) + 1
            longest = max(longest, w)
            sett.add(s[r])
        return longest
```
- ** contains-duplicate-ii ** [link](https://leetcode.com/problems/contains-duplicate-ii/description/?envType=problem-list-v2&envId=sliding-window)
```
class Solution:
    def containsNearbyDuplicate(self, nums: List[int], k: int) -> bool:
        hashmap = {}

        for i in range(len(nums)):
            if nums[i] in hashmap and i - hashmap[nums[i]] <=k:
                return True
            hashmap[nums[i]] = i
        return False
```
- ** longest-harmonious-subsequence ** [link](https://leetcode.com/problems/longest-harmonious-subsequence/description/?envType=problem-list-v2&envId=sliding-window)
        
```
#hashmap 

class Solution:
    def findLHS(self, nums: List[int]) -> int:
        freq = defaultdict(int)
        res = 0
        for num in nums:
            freq[num] += 1
        # print(freq)

        for num in freq:
            if num + 1 in freq:
                res = max(res, freq[num] + freq[num + 1])
        return res

```
