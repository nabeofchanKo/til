# [Singly Linked Lists: Basics & Operations (Work in Progress)]

## 💡 What I Learned
- **Concepts of Singly Linked Lists**: Unlike an Array, each node consists of a "value" and a "pointer to the next node". Data does not need to be stored consecutively in memory. (配列（Array）とは異なり、各データ（Node）が「値」と「次のデータへのポインタ」を持ち、数珠繋ぎになっている構造。メモリ上で連続している必要がない。)
- **Insertion**: To add a new Node at the end, only the last Node needs to update its pointer. Unlike arrays, no resizing or copying of the entire structure is necessary. (リストの末尾に新しいNodeを追加する場合、最後のNodeのポインタを新しいNodeに向けるだけで済む（配列のようなサイズ変更やコピーが不要）。)
- **Deletion by Value**: To delete a specific Node, connect the *previous* Node's pointer directly to the Node *following* the one being deleted. (特定の値を持つNodeを削除する場合、その「一つ前のNode」のポインタを「削除対象の次のNode」に繋ぎ変えることで実現する。)

## 💻 Code Snippet
```python
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None

class LinkedList:
    def __init__(self):
        self.head = None

    def append(self, data):
        """Insert a new node at the end of the list"""
        new_node = Node(data)
        
        # Case 1: If list is empty
        if not self.head:
            self.head = new_node
            return
        
        # Case 2: Traverse to the last node
        last_node = self.head
        while last_node.next:
            last_node = last_node.next
        last_node.next = new_node

    def delete_node(self, key):
        """Delete the first occurrence of key in the list"""
        curr_node = self.head

        # Case 1: If head holds the key to be deleted
        if curr_node and curr_node.data == key:
            self.head = curr_node.next
            curr_node = None
            return

        # Case 2: Search for the key to be deleted
        prev = None
        while curr_node and curr_node.data != key:
            prev = curr_node
            curr_node = curr_node.next

        # If key was not present in linked list
        if curr_node is None:
            return

        # Unlink the node from linked list
        prev.next = curr_node.next

    def print_list(self):
        curr_node = self.head
        while curr_node:
            print(curr_node.data, end=" -> ")
            curr_node = curr_node.next
        print("None")

# Test Execution
if __name__ == "__main__":
    llist = LinkedList()
    llist.append("Warehouse")
    llist.append("Point A")
    llist.append("Point B")
    llist.append("Point C")

    print("Original Route:")
    llist.print_list()

    print("\nAfter cancelling delivery to Point B:")
    llist.delete_node("Point B")
    llist.print_list()
```

## 🏥 Business Application
- Logistics: Managing a delivery route with a Linked List (e.g., "Warehouse -> Point A -> Point B -> Point C"). If a delivery to Point B is cancelled (Deletion), we only need to update Point A's destination to Point C without reconstructing the whole route. This offers more flexibility than an Array. (配送ルートをLinked Listで管理する（倉庫 -> 地点A -> 地点B -> 地点C）。 もし「地点B」への配送がキャンセル（Deletion）になった場合、ルート全体を作り直す必要はなく、「地点A」の行き先を「地点C」に書き換えるだけで済む。これは配列（Array）で管理するよりも柔軟に変更に対応できる。)

## Future Work
- Length Calculation
- Node Swapping
- Reverse Linked List
- Merging Two Sorted Linked Lists