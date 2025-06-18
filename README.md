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
