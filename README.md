## 2020 Questions:

### [287.](https://leetcode.com/problems/find-the-duplicate-number/) Find the Duplicate Number  
```python
# goes through and makes the 
# Time: O(n)
# Space: O(1)
def findDuplicate(self, nums: List[int]) -> int:
  for i in range(len(nums)):
    if nums[abs(nums[i]) - 1] < 0:
      return abs(nums[i])
    else:
      nums[abs(nums[i])-1] = -nums[abs(nums[i])-1]

  return -1
```
### [347.](https://leetcode.com/problems/top-k-frequent-elements/) Top K Frequent Elements  
```python
# keep track of the elements in a minheap with their count in first index.
# Time: O(nlog(k))
# Space: O(k)

def topKFrequent(self, nums, k):
  if not nums:
    return []
  if len(nums) == 1:
    return [nums[0]]

  count = collections.Counter(nums)
  q = []

  for num in set(nums):
    if len(q) == k:
      heapq.heappushpop(q, (count[num], num))
    else:
      heapq.heappush(q, (count[num], num))
      
  return [num[1] for num in reversed(q)]
```
### [23.](https://leetcode.com/problems/merge-k-sorted-lists/) Merge k Sorted Lists  
```python
# create a helper method to merge individual lists
# this is the same method as merging one list
# cover edge cases
# calculate the mid and recursively call the main function on the left and right sides
# call merge to merge it together
# Time: O(nlog(l)) where there are there are n lists and list is length l
# Space: O(log(l))

def merge(l, r):
 dummy = cur = ListNode(0)
 while l and r:
     if l.val < r.val:
         cur.next = l
         l = l.next
     else:
         cur.next = r
         r = r.next
     cur = cur.next
 cur.next = l or r
 return dummy.next
        
if not lists:
    return
if len(lists) == 1:
    return lists[0]

mid = len(lists)//2
l = self.mergeKLists(lists[:mid])
r = self.mergeKLists(lists[mid:])

return merge(l, r)
```
### [2.](https://leetcode.com/problems/add-two-numbers/) Add Two Numbers
```python
# make a dummy and current node. make a carry value = 0
# go through while loop until carry or l1 or l2 is done
# and l1 or l2 vals to carry if they exist
# get val by modding carry
# get carry by // 10
# set next node val to val, increment current
# Time: O(n+m)
# Space: O(n+m)

def addTwoNumbers(self, l1: ListNode, l2: ListNode) -> ListNode:
  dummy = ListNode(0)
  curr = dummy
  carry = 0
  while l1 or l2 or carry:
    if l1:
      carry += l1.val
      l1 = l1.next
    if l2:
      carry += l2.val
      l2 = l2.next
    val = carry % 10
    carry = carry // 10
    curr.next = ListNode(val)
    curr = curr.next
  return dummy.next
```
### [138.](https://leetcode.com/problems/copy-list-with-random-pointer/) Copy List with Random Pointer . 
```python
# make a dictionary and current pointer
# add each node to dictionary referencing a new node
# go through and add each of dic[curr] neighbors if they exist
# return the dictionary referencing the head
# Time: O(n)
# Space: O(n)

def copyRandomList(self, head: 'Node') -> 'Node':
  if not head:
      return None

  dic = {}
  curr = head

  while curr:
    dic[curr] = Node(curr.val)
    curr = curr.next

  curr = head

  while curr:
    if curr.next:
      dic[curr].next = dic[curr.next]
    if curr.random:
      dic[curr].random = dic[curr.random]
    curr = curr.next

  return dic[head]
```

### [997.](https://leetcode.com/problems/find-the-town-judge/) Find the Town Judge  
```python
# make an array of size n+1 for zero indexing
# for each pair in the array
# decrement the value for the person trusting
# and increment for the person trusted
# Find the person with N-1 value in trusted
# Time: O(n), Space: O(n)

trusted = [0] * (N+1)
        
for a, b in trust:
  trusted[a] -= 1
  trusted[b] += 1
    
for i in range(1,N+1):
  if trusted[i] == N-1:
    return i
        
return -1
```
### [200.](https://leetcode.com/problems/number-of-islands/) Number of Islands  
```python
# Do two for loops then look for if i,j is marked as land.
# call recursive dfs, then count += 1.
# in dfs check if it is still in bounds and land.
# mark the spot as used
# call dfs on all other spots
# Time: O(n^2) where n is len and width, Space: O(n^2)

def helper(grid, i, j):
 if i < 0 or j < 0 or i >= len(grid) or j >= len(grid[0]) or grid[i][j] != '1':
     return
 grid[i][j] = '@'
 helper(grid, i+1, j)
 helper(grid, i-1, j)
 helper(grid, i, j+1)
 helper(grid, i, j-1)

if not grid:
    return 0
row = len(grid)
col = len(grid[0])
count = 0
for i in range(row):
    for j in range(col):
        if grid[i][j] == '1':
            helper(grid, i, j)
            count += 1
return count     
```
### [973.](https://leetcode.com/problems/k-closest-points-to-origin/) K Closest Points to Origin  
```
go through each point.
calculate distance as negative to make a maxheap.
if length of maxheap is equal to k, pushpop
else push onto heap
return the pair of points from maxheap
```
### [91.](https://leetcode.com/problems/decode-ways/) Decode Ways  
### [1060.](https://leetcode.com/problems/missing-element-in-sorted-array/) Missing Element in Sorted Array  
### [56.](https://leetcode.com/problems/merge-intervals/) Merge Intervals  
```python
# make output array
# sort the intervals by the first value and loop thru
# if output is not empty and the starting time <= ending time of prev interval
# make the ending time the max of current interval or previous interval
# else add interval to output
# Time: O(n)
# Space: O(n)

out = []
        
for i in sorted(intervals, key=lambda i: i[0]):
  if out and i[0]<=out[-1][-1]:
    out[-1][-1] = max(out[-1][-1], i[-1])
  else: 
    out+=[i]
return out
```
### [226.](https://leetcode.com/problems/invert-binary-tree/) Invert Binary Tree  
```python
# Time: O(n)
# Space: O(n)

# recursively
if root:
    root.left, root.right = self.invertTree(root.right), self.invertTree(root.left)
    return root

#iteratively
q = collections.deque([root])
while q:
  node = q.popleft()
  if node:
    node.left, node.right = node.right, node.left
    q.append(node.left)
    q.append(node.right)
return root
```
### [155.](https://leetcode.com/problems/min-stack/) Min Stack  
```python
# Whole point here is to use a stack to append the next value with the current min at all times
# Time: O(1) look up
# Space: O(n)

class MinStack:
  def __init__(self):
      self.q = []

  def push(self, x: int) -> None:
    curMin = self.getMin()
    if curMin is None or x < curMin:
      curMin = x
    self.q.append((x, curMin))

  def pop(self) -> None:
    self.q.pop()

  def top(self) -> int:
    if len(self.q) == 0:
      return None
    else:
      return self.q[-1][0]

  def getMin(self) -> int:
    if len(self.q) == 0:
      return None
    else:
      return self.q[-1][1]
```
### [472.](https://leetcode.com/problems/concatenated-words/) Concatenated Words  
### [121.](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/) Best Time to Buy and Sell Stock  
```
Keep track of the minimum value in array.
take difference of the day - minimum.
update maximum.
```
### [108.](https://leetcode.com/problems/convert-sorted-array-to-binary-search-tree/) Convert Sorted Array to Binary Search Tree  
```python
# Create a convert function to call recursively.
# Call convert function with beginning index and ending
# In convert set the parent node as the middle index
# recursively convert left side of array (mid-1) and right (mid+1)
# return the node
# Time: O(n), Space: O(n)

  def convert(left, right):
    if left > right:
      return None
    mid = (left + right) // 2
    node = TreeNode(nums[mid])
    node.left = convert(left, mid - 1)
    node.right = convert(mid + 1, right)
    return node
return convert(0, len(nums) - 1)
```
### [348.](https://leetcode.com/problems/design-tic-tac-toe/) Design Tic-Tac-Toe  
```python
# Instantiate a class by making a row array and col array of size n
# diagonal set to 0 and anti-diagonal set to zero, and the board size n
# everytime a player makes a move, calculate the offset, -1 or 1
# add this offset to diag, anti-diag, rows and cols
# if offset * n (a row is filled) return the player
# Time: O(1)
# Space: O(n)

class TicTacToe:
  def __init__(self, n):
    self.row, self.col, self.diag, self.anti_diag, self.n = [0] * n, [0] * n, 0, 0, n

  def move(self, row, col, player):
    offset = player * 2 - 3
    self.row[row] += offset
    self.col[col] += offset
    if row == col:
        self.diag += offset
    if row + col == self.n - 1:
        self.anti_diag += offset
    if offset * self.n in [self.row[row], self.col[col], self.diag, self.anti_diag]:
        return player
    return 0
```
### [767.](https://leetcode.com/problems/reorganize-string/) Reorganize String  
### [31.](https://leetcode.com/problems/next-permutation/) Next Permutation  
### [543.](https://leetcode.com/problems/diameter-of-binary-tree/) Diameter of Binary Tree  
```python
# Keep a global maximum value
# create a depth function which calculates the max depth.
# in the depth function calculate the max diameter of each subtree and compare to max.
# return the max value
# Time: O(n), Space: O(n)

self.ans = 0
        
  def depth(p):
    if not p: return 0
    left, right = depth(p.left), depth(p.right)
    self.ans = max(self.ans, left+right)
    return 1 + max(left, right)
            
depth(root)
return self.ans
```
### [48.](https://leetcode.com/problems/rotate-image/) Rotate Image  
### [49.](https://leetcode.com/problems/group-anagrams/) Group Anagrams  
```python
# make a dictionary
# go through each word in strings
# get the sorted tuple value of the word
# add the word to the dictionary key of the sorted tuple
# Time: O(n*mlog(m)) n = size of strs, m = size of word, Space: O(n)

d = {}
for word in strs:
  value = tuple(sorted(word))
  d[value] = d.get(value, []) + [word]
        
return list(d.values())
```
### [387.](https://leetcode.com/problems/first-unique-character-in-a-string/) First Unique Character in a String (then in stream)
```python
# Have a string of letters in the alphabet.
# For each letter in alphabet,
#  find the count of the letter in the string,
#    if the count == 1 add to your list of values.
# return the min of the values if values exist.
# Time: O(26*n), operations are called 26 times but only go thru loop once. Space: O(26 or 1)

letters='abcdefghijklmnopqrstuvwxyz'
index=[s.index(l) for l in letters if s.count(l) == 1]
return min(index) if len(index) > 0 else -1
```
### [232.](https://leetcode.com/problems/implement-queue-using-stacks/) Implement Queue using Stacks  
### [98.](https://leetcode.com/problems/validate-binary-search-tree/) Validate BST  
```python
# make a helper function that compares each node using DFS
# in each iteration u pass the lower bound value and upper bound value
# this could be parent or the original inf/-inf value
# call the function again on left and right node
# call the helper from the main
# Time: O(n)
# Space: O(n)

def helper(node, low, high):
  if not node:
      return True
  if not (low < node.val < high):
      return False
  return helper(node.left, low, node.val) and helper(node.right, node.val, high)

return helper(root, float("-inf"), float("inf"))
```
### [3.](https://leetcode.com/problems/longest-substring-without-repeating-characters/) Longest Substring Without Repeating Characters  
```python
# Keep a starting index, count index, and a dictionary
# Go thrugh the string and see if character in d and start is less than
# the index of the current character.
# if it passes both of these, then make the start 1 + the current character's index
# keep track of max count otherwise
# return count
# Time: O(n)
# Space: O(n)

def lengthOfLongestSubstring(self, s):
  start, count = 0, 0
  d = {}
  for i in range(len(s)):
    if s[i] in d and start <= d[s[i]]:
      start = d[s[i]] + 1
    else:
      count = max(i - start + 1, count)
    d[s[i]] = i

  return count
```
### [939.](https://leetcode.com/problems/minimum-area-rectangle/) Minimum Area Rectangle  

sort a list based on order in the second list  
implement stack using arrays  
Given a binary tree, print its immediate right neighbor (level wise)  
First occurence of an element in an array  
First occurence of an element in a sorted array  
but given a scrambled string, return a valid English dictionary word that can be returned with the string  
Delete alternate nodes from a circular linked list.   
Median of BST  


## Someone else's final list
LRU cachue using Doubly Linked List and dictionary  
Roman <-> Integer  
Dial keypad (Backtrack+DFS)  
BST verification  
Width/Diameter of BT  
Path Sum Leetcode (root to node)  
Reversing a Linked List (LL)  
Create copy of LL using random pointer  
LL as number and add those.  
Merge k sorted LL  
BFS/DFS  
Level order traversal  
Zig zag traversal    
 BFS search between a start and an end in a graph  


## Behavioral Questions:  
#### Why amazon?  
- I am helpful from past internships, working with full stack technologies.
- It will be a place that i can grow as a software engineer
- I have had experience with customers working from my first internships, i know how valuable the customer is
#### Tell me about yourself  
Sacrifice for larger rewards related question !?  
Things you did out of your daily job responsiblity ?  
Tell me a time when you had to decide on 2 differnt approaches  
When did you deliver more than you were asked?  
When did you make a mistake?  
Tell me about a time you faced an obstacle and how you overcame it.  
Tell me about a time you took help from senior  
#### deadline  
- S: At iridium i failed to do one of my tasks before the meeting due to wanting to learn other parts of the stack
- A: Decided to take more ownership of the tasks i was assigned and made sure to be prepared for the meeting.
- R: from then on i had decided to give follow up of notes for the meeting and updates on the project
- (another time could be workign on a school project and not getting all the requirements done) resulting in me focusing on
#### failures
- meeting deadline at iridium with dashboard based on reports and how i used follow up emails, after meeting notes
- engineering project for hovercraft. how our project failed final run, ownership of project, lead team for meetings

Tell me a situation where you had to take a tough decision  
Tell me a situation where you helped someone, even though its not your part  
Tell me a situation when you don't have enough time to evaluate all the options before doing something.
When was a time when you went over and above for the customer?   
Have you ever had to make a tough decision without consulting anybody? (bias for action)  
Have you ever helped a peer who was struggling to understand technology? (ownership)  
setbacks on projects  
Tell me about a time you made a mistake.  


https://www.amazon.jobs/en/principles
https://interviewgenie.com/blog-1/category/Amazon+interviews
https://leetcode.com/discuss/interview-question/437082/Amazon-Behavioral-questions-or-Leadership-Principles-or-LP
https://medium.com/@scarletinked/are-you-the-leader-were-looking-for-interviewing-at-amazon-8301d787815d
[SDE1 Final Interview Questions](https://leetcode.com/discuss/interview-question/488887/amazon-final-interview-questions-sde1)
