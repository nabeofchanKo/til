# [Arrays & Hashing: Patterns and Problems]

## 💡 Key Concepts & Patterns
- **Hash Map (Dictionary)**: A Key-Value store allowing **O(1)** average time complexity for lookups. Essential for caching results (e.g., Two Sum) or counting frequencies. (キーと値のペアで管理するデータ構造。検索が平均O(1)で可能なため、計算結果のキャッシュや頻度カウントに必須。)
- **Two Pointers**: A technique to efficiently traverse arrays (often sorted) from different ends or directions to find pairs or intersections, reducing complexity from O(n²) to **O(n)**. (ソート済みの配列などで、始点と終点（または異なる位置）から2つのポインタを操作して探索する手法。二重ループを回避し計算量を落とせる。)
- **Python Sets**: Useful for **O(1)** lookups and removing duplicates instantly using set theory logic. (重複を許さない集合データ構造。高速な存在確認や、重複削除、積集合（Intersection）の計算に便利。)

## 📘 Educative: Array Logic
Fundamental logic for array manipulation.

### Array Advance (Greedy Algorithm)
Check if the last index is reachable by jumping from the current position.
```python
def array_advance(A):
    furthest_reached = 0
    last_idx = len(A) - 1
    i = 0
    while i <= furthest_reached and furthest_reached < last_idx:
        furthest_reached = max(furthest_reached, A[i] + i)
        i += 1
    return furthest_reached >= last_idx

```

## ⚔️ LeetCode Practice
Refined solutions focusing on Pythonic syntax and Time/Space Complexity.

1. Two Sum
- Approach: Use a Hash Map to store ```value -> index```. By checking if ```target - num``` exists in the map, we can find the pair in one pass.
- Complexity: Time O(n) | Space O(n)
```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        prev_map = {}  # val : index

        for i, n in enumerate(nums):
            diff = target - n
            if diff in prev_map:
                return [prev_map[diff], i]
            prev_map[n] = i
        return []
```
217. Contains Duplicate
- Approach: Use a Hash Set to check if the length of the unique set differs from the original list.
- Complexity: Time O(n) | Space O(n)
```python
class Solution:
    def containsDuplicate(self, nums: List[int]) -> bool:
        return len(set(nums)) != len(nums)
```
242. Valid Anagram
- Approach: Compare character frequency counts using ```collections.Counter```.
- Complexity: Time O(n) | Space O(1) (Since alphabet size is fixed at 26)
```python
from collections import Counter

class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        return Counter(s) == Counter(t)
```
349. Intersection of Two Arrays
- Approach: Use Set intersection (```&``` operator) to efficiently find common elements.
- Complexity: Time O(n+m) | Space O(n+m)
```python
class Solution:
    def intersection(self, nums1: List[int], nums2: List[int]) -> List[int]:
        return list(set(nums1) & set(nums2))
```
706. Design HashMap (Under the Hood)
- Concept: Implementing a Hash Map using Chaining to handle collisions.
- Structure: An array of buckets, where each bucket contains a list of (```key, value```) tuples.
```python
class MyHashMap:
    def __init__(self):
        self.size = 1000
        self.buckets = [[] for _ in range(self.size)]

    def put(self, key: int, value: int) -> None:
        index = key % self.size
        bucket = self.buckets[index]
        for i, (k, v) in enumerate(bucket):
            if k == key:
                bucket[i] = (key, value) # Update existing key
                return
        bucket.append((key, value)) # Insert new key

    def get(self, key: int) -> int:
        index = key % self.size
        bucket = self.buckets[index]
        for k, v in bucket:
            if k == key:
                return v
        return -1

    def remove(self, key: int) -> None:
        index = key % self.size
        bucket = self.buckets[index]
        for i, (k, v) in enumerate(bucket):
            if k == key:
                del bucket[i]
                return
```

## 🏥 Business Application
- Pharma (Drug Interaction Check): Instead of scanning a list of thousands of drugs (O(n)), use a Hash Map (O(1)) to instantly check if a prescribed drug interacts with a patient's existing medication list. (数千種類の薬剤リストをスキャンするのではなく、ハッシュマップを使ってO(1)で即座に飲み合わせ（相互作用）チェックを行う。)

- Logistics (Inventory Management): Managing SKU (Stock Keeping Unit) data using Hash Maps allows for instant retrieval of stock levels, location, and price given a product ID. (商品ID（SKU）をキーとしたハッシュマップで在庫管理を行うことで、在庫数や保管場所への即時アクセスを実現する。)

- Logistics (Route Planning): Arrays are fundamental for representing time-series GPS coordinates or delivery sequences where order matters. (時系列のGPS座標や配送順序など、順序が重要なデータには配列（リスト）が不可欠。)