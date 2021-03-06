### Top 100 Liked Questions
solved: 
+ 1~100: 1, 3, 19, 20, 49, 70, 94, 96, 
+ 101~200: 136, 169, 
+ 201~300:

1. Two Sum
```
Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
```
```
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        vector<int> ans(2);
        int stop = 0;
        for(int i=0; i<nums.size()-1; i++) {
            for(int j=i+1; j<nums.size(); j++) {
                if(nums[i]+nums[j]==target) {
                    ans[0]=i;
                    ans[1]=j;
                    stop=1;
                    break;
                }
            }
        if(stop==1) {
            break;
        }
        }
        return ans;
    }
};
```
3. Longest Substring Without Repeating Characters

Given a string, find the length of the longest substring without repeating characters.
```
Input: "abcabcbb"
Output: 3 
Explanation: The answer is "abc", with the length of 3.
```
+ hint: i<=j, the number of the char s[i] in the string s[i:j] is myMap[s[i]] and the number of the char s[j] in the string s[i:j] is myMap[s[j]].
+ example: s="abcabcbb"
  + "a"->"ab"->"abc"->"abca"->"bca"->"bcab"->"cab"->"cabc"->"abc"->"abcb"->"bcb"->"cb"->"cbb"->"bb"->"b"
```
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        int ans=0;
        unordered_map<char, int> myMap;
        for(int i=0, j=0; j<s.size(); j++) {
            myMap[s[j]]++;
            while(myMap[s[j]]>1) myMap[s[i++]]--;
            ans = max(ans, j-i+1);
        }
        return ans;
    }
};
```
19. Remove Nth Node From End of List
```
Given a linked list, remove the n-th node from the end of list and return its head.
Example: Given linked list: 1->2->3->4->5, and n = 2. After removing the second node from the end, the linked list becomes 1->2->3->5.
```
+ `fast` pointer points to the node which is N step away from the to_be_delete node. `slow` pointer points to the to_be_delete node.

The algorithms is described as below:
+ Firstly, move fast pointer N step forward.
+ Secondly,move fast and slow pointers simultaneously one step a time forward till the fast pointer reach the end, which will cause the slow pointer points to the previous node of the to_be_delete node.
+ Finally, slow->next = slow->next->next.
```
class Solution {
public:
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        if(!head) 
            return nullptr;
        ListNode new_head(-1);
        new_head.next = head;
        ListNode *slow = &new_head, *fast = &new_head;
        for(int i=0; i<n; i++) {
            fast = fast->next;
        }
        while(fast->next) {
            slow = slow->next;
            fast = fast->next;
        }
        ListNode *node_to_be_delete = slow->next;
        slow->next = slow->next->next;
        delete node_to_be_delete;
        return new_head.next;
    }
};
```
20. Valid Parentheses

Given a string containing just the characters '(', ')', '{', '}', '[', ']', determine if the input string is valid.
```
Input: "()[]{}"
Output: true

Input: "(]"
Output: false
```
```
class Solution {
public:
    bool isValid(string s) {
        stack<char> a;
        for(char &c:s) {
            switch(c) {
                case '(':
                case '[':
                case '{': a.push(c); break;
                case ')': if(a.empty() || a.top()!='(') return false; else a.pop(); break;
                case ']': if(a.empty() || a.top()!='[') return false; else a.pop(); break;
                case '}': if(a.empty() || a.top()!='{') return false; else a.pop(); break;
            }
        }
        return a.empty();
    }
};
```
49. Group Anagrams

Given an array of strings, group anagrams together.
```
Example: Input: ["eat", "tea", "tan", "ate", "nat", "bat"],
Output:
[ ["ate","eat","tea"],
  ["nat","tan"],
  ["bat"]]
```
```
algorithm:
str = "eat";
t = str;
sort(t.begin(), t.end()); // then t = "aet";
res["aet"] = "eat";
```
```
class Solution {
public:
    vector<vector<string>> groupAnagrams(vector<string>& strs) {
        unordered_map<string, vector<string>> res;
        for(string str:strs) {
            string t = str;
            sort(t.begin(), t.end());
            res[t].push_back(str);
        }
        
        vector<vector<string>> ans;
        for(auto tmp:res) {
            ans.push_back(tmp.second);
        }
        return ans;
    }
};
```
70. Climbing Stairs

You are climbing a stair case. It takes n steps to reach to the top. Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?

Note: Given n will be a positive integer.
```
Example 1: Input: 2, Output: 2
```
```
class Solution {
public:
    int climbStairs(int n) {
        vector<int> dp(2, 1);
        dp[1] = 2;
        for(int i=2; i<n; i++) {
            dp.push_back(dp[i-2]+dp[i-1]);
        }
        return dp[n-1];
    }
};
```
94. Binary Tree Inorder Traversal

Given a binary tree, return the inorder traversal of its nodes' values.
```
class Solution {
public:
    vector<int> inorderTraversal(TreeNode* root) {
        stack<TreeNode *> todo;
        vector<int> ans;
        while(root || !todo.empty()) {
            while(root) {
                todo.push(root);
                root = root->left;
            }
            root = todo.top();
            todo.pop();
            ans.push_back(root->val);
            root = root->right;
        }
        return ans;
    }
};
```
96. Unique Binary Search Trees

Given n, how many structurally unique BST's (binary search trees) that store values 1 ... n?
```
class Solution {
public:
    int numTrees(int n) {
        vector<int> dp(3, 1);
        dp[2] = 2;
        for(int i=3; i<=n; i++) {
            int tmp = 0;
            for(int j=0; j<i; j++) {
                tmp += dp[j]*dp[i-1-j];
            }
            dp.push_back(tmp);
        }
        return dp[n];
    }
};
```
136. Single Number

Given a non-empty array of integers, every element appears twice except for one. Find that single one.
```
Example: Input: [4,1,2,1,2], Output: 4
```
```
class Solution {
public:
    int singleNumber(vector<int>& nums) {
        int ans;
        unordered_map<int, int> mp;
        for(int tmp: nums) {
            mp[tmp] += 1;
        }
        for(auto tmp: mp) {
            if(tmp.second==1) ans = tmp.first;
        }
        return ans;
    }
};
```
169. Majority Element

Given an array of size n, find the majority element. The majority element is the element that appears more than ⌊ n/2 ⌋ times. You may assume that the array is non-empty and the majority element always exist in the array.
```
Example 1: Input: [3,2,3], Output: 3
```
```
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        unordered_map<int, int> mp;
        vector<int> ans;
        for(auto t: nums) {
            mp[t]++;
        }
        
        for(auto s: mp) {
            if(s.second>nums.size()/2) ans.push_back(s.first);
        }
        return ans[0];
    }
};
```
416. Partition Equal Subset Sum
```
Given a non-empty array containing only positive integers, find if the array can be partitioned into two subsets such that the sum of elements in both subsets is equal.

Note: Each of the array element will not exceed 100. The array size will not exceed 200. 

Example 1: Input: [1, 5, 11, 5], Output: true
Explanation: The array can be partitioned as [1, 5, 5] and [11].

Example 2: Input: [1, 2, 3, 5], Output: false
Explanation: The array cannot be partitioned into equal sum subsets.
```
+ This problem is equavelent to finding a subset of nums, denoted as U, such that `sum(U)=sum(nums)/2`
  + Proof: Suppose the set nums is divided into two disjoint sets, denoted as U and V, then the union of U and V equals to nums. In addition, `sum(U)=sum(V)`, according to the description of the problem. Therefore, `sum(U)=sum(V)=sum(nums)/2`.
```
class Solution {
public:
    bool canPartition(vector<int>& nums) {
        int target = accumulate(nums.begin(), nums.end(), 0);
        if(target%2==1) return false;
        else target = target/2;
        
        vector<int> vec(target+1);
        vec[0] = 1;
        for(int i=0; i<nums.size(); i++) {
            for(int j=target; j>=nums[i]; j--) {
                vec[j] = vec[j] || vec[j-nums[i]];
            }
        }
        
        return vec[target];
    }
};
```
494. Target Sum

```
You are given a list of non-negative integers, a1, a2, ..., an, and a target, S. Now you have 2 symbols + and -. For each integer, you should choose one from + and - as its new symbol.

Find out how many ways to assign symbols to make sum of integers equal to target S.
Example 1:Input: nums is [1, 1, 1, 1, 1], S is 3. Output: 5 
Explanation: 
-1+1+1+1+1 = 3
+1-1+1+1+1 = 3
+1+1-1+1+1 = 3
+1+1+1-1+1 = 3
+1+1+1+1-1 = 3

There are 5 ways to assign symbols to make the sum of nums be target 3.
```
+ Suppose the set `nums=[a1, a2, ..., an]` is divided into two disjoint subsets P (for positive sysmbol) and N (for negtive sysmbol). For example, if `nums = [1, 2, 3, 4]` and `target=2`, then P and N could be `P = [2, 4]` and `N = [1, 3]`.
+ The problem is equavelent to answering how many subsets, denoted as `P`, do we have such that `sum(P)=(sum(nums)+target)/2`?
  + Proof: Since `sum(P)-sum(N) = target` and `sum(P)+sum(N) = sum(nums)`, then we have `sum(P)=(sum(nums)+target)/2`.
```
class Solution {
public:
    int findTargetSumWays(vector<int>& nums, int S) {
        int sum = 0;
        for (auto n : nums) sum += n;
        if(abs(S)>sum || (sum+S)%2==1) return 0;
        int target = (sum+S)/2;
        
        vector<int> vec(target+1);
        vec[0] = 1;
        for(int i=0; i<nums.size(); i++) {
            for(int j=target; j>=nums[i]; j--) {
                vec[j] = vec[j] + vec[j-nums[i]];
            }
        }
        
        return vec[target];
    }
};
```
560. Subarray Sum Equals K

```
Given an array of integers and an integer k, you need to find the total number of continuous subarrays whose sum equals to k.
Example 1: Input:nums = [1,1,1], k = 2, Output: 2
```
+ Time Limit Exceeded
```
class Solution {
public:
    int subarraySum(vector<int>& nums, int k) {
        for(int i=1; i<nums.size(); i++) nums[i] += nums[i-1];
        nums.insert(nums.begin(), 0);
        
        int ans=0;
        for(int i=1; i<nums.size(); i++) {
            for(int j=0; j<i; j++) {
                if(nums[i]-nums[j]==k) ans++;
            }
        }
        
        return ans;
    }
};
```
560. Subarray Sum Equals K
```
Given an array of integers and an integer k, you need to find the total number of continuous subarrays whose sum equals to k.
Example 1: Input:nums = [1,1,1], k = 2 Output: 2
```
```
class Solution {
public:
    int subarraySum(vector<int>& nums, int k) {
        int ans=0, sum=0;
        unordered_map<int, int> mp;
        mp[0] = 1;
        
        for(int i=0; i<nums.size(); i++) {
            sum += nums[i];
            ans += mp[sum-k];
            mp[sum] ++;
        }
        
        return ans;
    }
};
```
240. Search a 2D Matrix II

```
Write an efficient algorithm that searches for a value in an m x n matrix. This matrix has the following properties: Integers in each row are sorted in ascending from left to right. Integers in each column are sorted in ascending from top to bottom.
Example:
Consider the following matrix:
[ [1,   4,  7, 11, 15],
  [2,   5,  8, 12, 19],
  [3,   6,  9, 16, 22],
  [10, 13, 14, 17, 24],
  [18, 21, 23, 26, 30]]

Given target = 5, return true. Given target = 20, return false.
```
+ 每次都同右上角的元素相比。
```
class Solution {
public:
    bool searchMatrix(vector<vector<int>>& matrix, int target) {
        if(matrix.size()==0 or matrix[0].size()==0) return false;
        int i=0, j=matrix[0].size()-1;
        while(i<matrix.size() and j>=0) {
            if(matrix[i][j]==target) return true;
            else if(matrix[i][j]>target) j--;
            else i++;
        }
        
        return false;
    }
};
```
207. Course Schedule
```
Example 1: Input: numCourses = 2, prerequisites = [[1,0]], Output: true
Explanation: There are a total of 2 courses to take. 
             To take course 1 you should have finished course 0. So it is possible.

Example 2: Input: numCourses = 2, prerequisites = [[1,0],[0,1]], Output: false
Explanation: There are a total of 2 courses to take. 
             To take course 1 you should have finished course 0, and to take course 0 you should
             also have finished course 1. So it is impossible.
```
```
class Solution {
public:
    bool canFinish(int numCourses, vector<vector<int>>& prerequisites) {
        vector<vector<int>> G(numCourses);
        unordered_map<int, int> degree;
        vector<int> history;
        
        for(auto &t: prerequisites) G[t[1]].push_back(t[0]), degree[t[0]]++;
        for(int i=0; i<numCourses; i++) {
            if(degree[i]==0) history.push_back(i);
        }
        for(int i=0; i<history.size(); i++) {
            for(auto j: G[history[i]]) {
                if(--degree[j]==0) history.push_back(j);
            }
        }
        
        return history.size()==numCourses;
    }
};
```
215. Kth Largest Element in an Array

```
Find the kth largest element in an unsorted array. Note that it is the kth largest element in the sorted order, not the kth distinct element.
Example 1: Input: [3,2,1,5,6,4] and k = 2, Output: 5
Example 2: Input: [3,2,3,1,2,4,5,5,6] and k = 4, Output: 4
```
```
class Solution {
public:
    int findKthLargest(vector<int>& nums, int k) {
        int newNums[nums.size()];
        for(int i=0; i<nums.size(); i++) newNums[i]=nums[i];
        quickSort(newNums, 0, sizeof(newNums)/sizeof(newNums[0])-1);
        return newNums[sizeof(newNums)/sizeof(newNums[0])-k];
    }
    
    void quickSort(int nums[], int left, int right) {
    if(left>right) return;

    int base = nums[right]; // choose the right-most element as base
    int l=left;
    int r=right;

    while(l!=r) {
        while(nums[l]<=base && l<r) l++;

        while(nums[r]>=base && l<r) r--;

        if(l<r) {
            int tmp=nums[l];
            nums[l] = nums[r];
            nums[r] = tmp;
        }
    }

    nums[right] = nums[l];
    nums[l] = base;

    quickSort(nums, left, l-1);
    quickSort(nums, l+1, right);
}
    
};
```
238. Product of Array Except Self
```
Given an array nums of n integers where n > 1,  return an array output such that output[i] is equal to the product of all the elements of nums except nums[i].

Example: Input:  [1,2,3,4], Output: [24,12,8,6]
```
```
class Solution {
public:
    vector<int> productExceptSelf(vector<int>& nums) {
        int n = nums.size();
        vector<int> prefix(n, 1), suffix(n, 1);
        
        for(int i=1; i<n; i++) {
            prefix[i] = prefix[i-1]*nums[i-1];
        }
        
        for(int i=n-2; i>=0; i--) {
            suffix[i] = suffix[i+1]*nums[i+1];
        }
        
        for(int i=0; i<n; i++) {
            prefix[i] *= suffix[i];
        }
        
        return prefix;
        
    }
};
```
283. Move Zeroes
```
Given an array nums, write a function to move all 0's to the end of it while maintaining the relative order of the non-zero elements.

Example: Input: [0,1,0,3,12], Output: [1,3,12,0,0]
Note: You must do this in-place without making a copy of the array. Minimize the total number of operations.
```
```
class Solution {
public:
    void moveZeroes(vector<int>& nums) {
        int n = nums.size();
        for(int i=0; i<n; i++) {
            if(nums[i]==0) {
                int j = i+1;
                while(j<n and nums[j]==0) j++;
                if(j<n) nums[i] = nums[j], nums[j] = 0;
            }
        }
    }
};
```
621. Task Scheduler
```
Input: tasks = ["A","A","A","B","B","B"], n = 2, Output: 8
Explanation: A -> B -> idle -> A -> B -> idle -> A -> B.
```
```
class Solution {
public:
    int leastInterval(vector<char>& tasks, int n) {
        int count=0, ans=0;
        unordered_map<char, int> mp;
        
        for(auto t: tasks) mp[t]++, count = max(count, mp[t]);
        ans = (count-1)*(n+1);
        for(auto t: mp) if(t.second==count) ans++;
        
        return max(ans, (int)tasks.size());
    }
};
```
647. Palindromic Substrings
```
Given a string, your task is to count how many palindromic substrings in this string.
The substrings with different start indexes or end indexes are counted as different substrings even they consist of same characters.
Example 1: Input: "abc", Output: 3, Explanation: Three palindromic strings: "a", "b", "c".
Example 2: Input: "aaa", Output: 6, Explanation: Six palindromic strings: "a", "a", "a", "aa", "aa", "aaa".
```
```
class Solution {
public:
    int countSubstrings(string s) {
        int ans = 0, n = s.size();
        
        for(int i=0; i<n; i++) {
            for(int j=0; i-j>=0 and i+j<n and s[i-j]==s[i+j]; j++) ans++;
            for(int j=0; i-j-1>=0 and i+j<n and s[i-j-1]==s[i+j]; j++) ans++;
        }
        return ans;
    }
};
```
739. Daily Temperatures
```
Given a list of daily temperatures T, return a list such that, for each day in the input, tells you how many days you would have to wait until a warmer temperature. If there is no future day for which this is possible, put 0 instead.
For example, given the list of temperatures T = [73, 74, 75, 71, 69, 72, 76, 73], your output should be [1, 1, 4, 2, 1, 1, 0, 0].
```
```
class Solution {
public:
    vector<int> dailyTemperatures(vector<int>& T) {
        int n = T.size();
        vector<int> ans(n, 0);
        
        for(int i=0; i<n-1; i++) {
            if(i>0 and T[i]==T[i-1]) {
                if(ans[i-1]>0) ans[i] = ans[i-1] - 1;
                else ans[i] = 0;
            }
            else {
                for(int j=i+1; j<n; j++) {
                    if(T[j]>T[i]) {
                    ans[i] = j-i;
                    break;
                }
            }

            }
        }
        return ans;
    }
};
```
438. Find All Anagrams in a String
```
Example 1: Input: s: "cbaebabacd" p: "abc", Output: [0, 6]
Explanation:
The substring with start index = 0 is "cba", which is an anagram of "abc".
The substring with start index = 6 is "bac", which is an anagram of "abc".

Example 2: Input: s: "abab" p: "ab", Output: [0, 1, 2]
Explanation:
The substring with start index = 0 is "ab", which is an anagram of "ab".
The substring with start index = 1 is "ba", which is an anagram of "ab".
The substring with start index = 2 is "ab", which is an anagram of "ab".
```
```
class Solution {
public:
    vector<int> findAnagrams(string s, string p) {
        int ns = s.size(), np = p.size();
        vector<int> ans, mp(26, 0), tmp(26, 0);
        if(np>ns) return ans;
        
        for(int i=0; i<np; i++) tmp[s[i]-'a']++, mp[p[i]-'a']++;
        if(tmp==mp) ans.push_back(0);
        
        for(int i=np; i<ns; i++) {
            tmp[s[i-np]-'a']--;
            tmp[s[i]-'a']++;
            if(tmp==mp) ans.push_back(i-np+1);
        }
        return ans;
    }
};
```
347. Top K Frequent Elements
```
Given a non-empty array of integers, return the k most frequent elements.
Example 1: Input: nums = [1,1,1,2,2,3], k = 2, Output: [1,2]
Example 2: Input: nums = [1], k = 1, Output: [1]
```
```
class Solution {
public:
    vector<int> topKFrequent(vector<int>& nums, int k) {
        unordered_map<int, int> mp;
        vector<int> ans;
        vector<vector<int>> freq2num(nums.size()+1);
        
        for(int t: nums) mp[t]++;
        for(auto t: mp) freq2num[t.second].push_back(t.first);
        for(int i=nums.size(); i>=0 and ans.size()<k; i--) {
            for(auto t: freq2num[i]) ans.push_back(t);
        }
        return ans;
    }
};
```
394. 
```
Given an encoded string, return its decoded string. The encoding rule is: k[encoded_string], where the encoded_string inside the square brackets is being repeated exactly k times. Note that k is guaranteed to be a positive integer. You may assume that the input string is always valid; No extra white spaces, square brackets are well-formed, etc. Furthermore, you may assume that the original data does not contain any digits and that digits are only for those repeat numbers, k. For example, there won't be input like 3a or 2[4].

Input: s = "3[a2[c]]", Output: "accaccacc"
```
```
class Solution {
public:
    string decodeString(string s, int & i) {
        string ans;
        while(i<s.length() and s[i]!=']') {
            if(!isdigit(s[i])) 
                ans += s[i++];
            else {
                int n=0;
                while(i<s.length() and isdigit(s[i])) {
                    n = n*10 + s[i++] - '0';
                }

                i++; // '['
                string t = decodeString(s, i);
                i++; // ']'

                while(n>0) {
                    ans += t;
                    n--;
                }
            }            
        }
        return ans;
    }
    string decodeString(string s) {
        int i=0;
        return decodeString(s, i);
    }
};
```
200. Number of Islands
```
Input: grid = [
  ["1","1","0","0","0"],
  ["1","1","0","0","0"],
  ["0","0","1","0","0"],
  ["0","0","0","1","1"]
]
Output: 3
```
```
class Solution {
public:
    int numIslands(vector<vector<char>>& grid) {
        int ans=0;
        if(grid.size()==0 or grid[0].size()==0) return 0;
        for(int i=0; i<grid.size(); i++) {
            for(int j=0; j<grid[0].size(); j++) {
                if(grid[i][j]=='1') {
                    ans++;
                    dfs(grid, i, j);
                }
            }
        }
        return ans;
    }

private:
    void dfs(vector<vector<char>> &grid, int x, int y) {
        grid[x][y] = '0';
        if(x>0 and grid[x-1][y]=='1') dfs(grid, x-1, y);
        if(x<grid.size()-1 and grid[x+1][y]=='1') dfs(grid, x+1, y);
        if(y>0 and grid[x][y-1]=='1') dfs(grid, x, y-1);
        if(y<grid[0].size()-1 and grid[x][y+1]=='1') dfs(grid, x, y+1);
    }
};
```
