# algLearning
算法学习及强化


## 1.LeetCode 101


[167. 两数之和 II - 输入有序数组](https://leetcode-cn.com/problems/two-sum-ii-input-array-is-sorted/)

```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& numbers, int target) {
        
        int l = 0, r = numbers.size()-1;
        while (l < r) {
            int sum = numbers[l] + numbers[r];
            if (sum == target) {
                return {l+1, r+1};
            } else if (sum > target) {
                r--;
            } else if (sum < target) {
                l++;
            }
        }
        return {};
    }
};
```
[88. 合并两个有序数组](https://leetcode-cn.com/problems/merge-sorted-array/)

```cpp
class Solution {
public:
    void merge(vector<int>& nums1, int m, vector<int>& nums2, int n) {
        int r1 = m - 1, r2 = n - 1;
        int t = m + n - 1;
        
        while (r1 >= 0 || r2 >= 0) {
            if (r1 < 0) {
                while (r2 >= 0) {
                    nums1[t--] = nums2[r2--];
                }
            } else if (r2 < 0) {
                while (r1 >= 0) {
                    nums1[t--] = nums1[r1--];
                }
            } else if (nums1[r1] > nums2[r2]){
                nums1[t--] = nums1[r1--];
            } else {
                nums1[t--] = nums2[r2--];
            }
        }

    }
};
```

[142. 环形链表 II](https://leetcode-cn.com/problems/linked-list-cycle-ii/)

```cpp
class Solution {
public:
    ListNode *detectCycle(ListNode *head) {
        ListNode* p = head, *q = head;
        while (q && q->next) {
            p = p->next;
            q = q->next->next;
            if (p == q) {
                while (head != p) {
                    p = p->next;
                    head = head->next;
                }
                return p;
            }
        }

        return NULL;
    }
};
```

[76. 最小覆盖子串](https://leetcode-cn.com/problems/minimum-window-substring/)


```cpp
class Solution {
public:
    string minWindow(string s, string t) {
        unordered_map<char,int> src;

        for (auto c : t) {
            src[c]++;
        }
        unordered_map<char,int> tg;
        int l = 0, r = 0, len = 0;

        int left = 0, minLen = s.size() + 1;
        while (r < s.size()) {
            char c = s[r++];
            if (src.count(c)) {
                tg[c]++;
                if (src[c] == tg[c]) {
                    len++;
                }
            }
            while (len == src.size()) {
                if (r-l<minLen) {
                    left = l;
                    minLen = r-l;
                }
                char c =  s[l++];
                if (src.count(c)) {
                    if (src[c] == tg[c]) len--;
                    tg[c]--;
                }
            }
        }
        return minLen == s.size()+1 ? "" : s.substr(left, minLen);
    }
};
```

[680. 验证回文字符串](https://leetcode-cn.com/problems/valid-palindrome-ii/)

解法1：双指针

```cpp
class Solution {
public:
    bool judgeSquareSum(int c) {
        int end = sqrt(c);

        int start = 0;
        while (start <= end) {
            if (start*start == c-end*end) {
                return true;
            } else if (start*start < c-end*end) {
                start++;
            } else if (start*start > c-end*end) {
                end--;
            }
        }
        return false;
    }
};
```
解法2：直接遍历

```cpp
class Solution {
public:
    bool judgeSquareSum(int c) {  
        for (long i = 0; i*i<=c && i <= c ; i++) {
            double target = sqrt(c-i*i);
            if (target == int(target)) return true;
        }
        return false;
    }
};
```

[680. 验证回文字符串 Ⅱ](https://leetcode-cn.com/problems/valid-palindrome-ii/)

```cpp
class Solution {
public:
    bool validPalindrome(string s) {
        int i=0, j = s.size()-1;
        for (; i < j && s[i] == s[j]; i++, j--); 
        return  dfs(s, i+1, j) || dfs(s, i, j-1);
    }

    bool dfs(const string& s, int i, int j) {
        for ( ; i < j && s[i] == s[j]; ++i, --j);
        return i >= j;
    }

    
};
```

[524. 通过删除字母匹配到字典里最长单词](https://leetcode-cn.com/problems/longest-word-in-dictionary-through-deleting/)

```cpp
class Solution {
public:
    string findLongestWord(string s, vector<string>& d) {

        vector<string> x;
        for (const auto& e : d) {
            int j = 0;
            for (int i = 0; i < s.size(); i++) {
                if (s[i] == e[j])
                    j++;
            }
            if (j == e.size()) {
                x.push_back(e);
            }
        }
        sort(x.begin(), x.end(), [](const auto& first, const auto& second) {
            return (first.size() > second.size()) || (first.size() == second.size() && first < second);
        });
        return x.size() == 0 ? "" : x[0];
    }
};
```

[386. 最多有k个不同字符的最长子字符串
](https://www.lintcode.com/problem/longest-substring-with-at-most-k-distinct-characters/description?utm_source=sc-bky-sz0904)

```cpp
class Solution {
public:
    /**
     * @param s: A string
     * @param k: An integer
     * @return: An integer
     */
    int lengthOfLongestSubstringKDistinct(string &s, int k) {
        // write your code here
        unordered_map<char, int> um;
        
        if (k == 0) return 0;
        
        int l = 0, r = 0, maxLen = 0, len = 0;
        
        while (r < s.size()) {
            int c = s[r++];
            if (um[c] == 0) len++;
            um[c]++;

            while (len > k) {
                int d = s[l++];
                um[d]--;
                if (!um[d]) {
                    len--;
                }
            }
            maxLen = max(maxLen, r - l);
        }
        
        return maxLen;
    }
};
```
