# [Understanding Stack Data Structure (LIFO)] 
## 💡 What I Learned
- **Concept of Stack**: A LIFO (Last In, First Out) data structure where the last element inserted is the first to be removed. (後入れ先出し形式のデータ構造であり、最後に保存したデータが最初に取り出される仕組み。)
- **Operations in Python**: Easy to implement using list methods: `append()` for "Push" and `pop()` for "Pop". (リストの `append()` をPushとして、`pop()` をPopとして利用することで簡単に実装可能であること。)
- **Application to Algorithms**: Effective when storing and referring to the latest state, such as in "Reverse String" or "Balanced Brackets" problems. (文字列の反転（Reverse String）や、括弧の整合性判定（Balanced Brackets）など、「直近の状態」を保持・参照する問題に有効。)

## 💻 Code Snippet
```python
class Stack:
    def __init__(self):
        self.items = []

    def push(self, item):
        """Add item to the top"""
        self.items.append(item)

    def pop(self):
        """Remove and return the top item"""
        if not self.is_empty():
            return self.items.pop()
        return None

    def is_empty(self):
        return len(self.items) == 0

    def peek(self):
        """Look at the top item without removing"""
        if not self.is_empty():
            return self.items[-1]
        return None

# Usage Example: Reverse a String
# "AI" -> "IA"
def reverse_string(s):
    stack = Stack()
    
    # Push each letter in s to Stack
    for letter in s:
        stack.push(letter)
    
    # Initialize an empty string to store the reversed string
    reverse_str = ""

    # Since Stack is LIFO, popping items retrieves them in reverse order
    while not stack.is_empty():
        # pop() returns the item, so we can append it directly
        reverse_str += stack.pop()

    return reverse_str

# Test
print(reverse_string("AI Engineer")) # Output: reenignE IA
```

## 🏥 Business Application
- **Logistics**: Truck Loading & Unloading is a typical example of LIFO operations. The last cargo loaded (Last In) is the first to be unloaded at the destination (First Out). It can also be applied to pallet stacking management. (トラックへの積載は典型的LIFO。最後に積んだ荷物（Last In）を、配送先で最初に取り出す（First Out）。倉庫でのパレット積み上げ管理にも適用可能。)