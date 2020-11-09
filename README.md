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
