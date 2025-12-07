# [Singly Linked Lists: Implementation & Operations]

## 💡 What I Learned
- **Concepts of Singly Linked Lists**: Unlike an Array, each node consists of a "value" and a "pointer to the next node". Data does not need to be stored consecutively in memory. (配列（Array）とは異なり、各データ（Node）が「値」と「次のデータへのポインタ」を持ち、数珠繋ぎになっている構造。メモリ上で連続している必要がない。)
- **Insertion**: To add a new Node at the end, only the last Node needs to update its pointer. Unlike arrays, no resizing or copying of the entire structure is necessary. (リストの末尾に新しいNodeを追加する場合、最後のNodeのポインタを新しいNodeに向けるだけで済む（配列のようなサイズ変更やコピーが不要）。)
- **Deletion by Value**: To delete a specific Node, connect the *previous* Node's pointer directly to the Node *following* the one being deleted. (特定の値を持つNodeを削除する場合、その「一つ前のNode」のポインタを「削除対象の次のNode」に繋ぎ変えることで実現する。)
- **Deletion by Position**: Deletion based on `Index` rather than `Value`. It requires handling two cases: deleting the Head (first node) and deleting any other node. (`Value` ではなく `Index`（何番目か）を指定して削除する操作。先頭（Head）を削除する場合と、それ以外で処理を分ける必要がある。)
- **Length Calculation**: Calculating the length requires traversing the list from Head to End. The time complexity is O(n). (リストの長さを知るには、Headから末尾まで next ポインタを辿ってカウントする必要がある（計算量は O(n)）。)
- **Node Swap**: Two ways to swap nodes: overwriting data vs. changing pointers. The latter approach is more crucial for understanding memory address manipulation. (2つのノードを入れ替える際、単に「中のデータ」を書き換える方法と、「ポインタ（接続）」を繋ぎ変える方法があるが、メモリ番地を扱う観点では後者がより重要。)
- **Reverse (Iterative)**: Reversing the list order by changing link directions. This requires maintaining three pointers: "Previous", "Current", and "Next". (リストの向きを逆転させる操作。「前のノード」「現在のノード」「次のノード」の3つのポインタを保持しながら、リンクの向きを次々と後ろへ向け変えていく。)

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

    def delete_at_position(self, pos):
        """Delete node at specific position (0-based index)"""
        if not self.head:
            return

        curr_node = self.head

        # Case 1: Delete head (position 0)
        if pos == 0:
            self.head = curr_node.next
            curr_node = None
            return

        # Case 2: Traverse to find the previous node of the position
        prev = None
        count = 0
        while curr_node and count != pos:
            prev = curr_node
            curr_node = curr_node.next
            count += 1

        # If position is out of range
        if curr_node is None:
            return

        # Unlink the node
        prev.next = curr_node.next
        curr_node = None

    def get_length(self):
        """Return the length of the list"""
        count = 0
        curr_node = self.head
        while curr_node:
            count += 1
            curr_node = curr_node.next
        return count

    def swap_nodes(self, key_1, key_2):
        """Swap two nodes by changing pointers (not just data)"""
        if key_1 == key_2:
            return

        # Search for key_1
        prev_1 = None
        curr_1 = self.head
        while curr_1 and curr_1.data != key_1:
            prev_1 = curr_1
            curr_1 = curr_1.next

        # Search for key_2
        prev_2 = None
        curr_2 = self.head
        while curr_2 and curr_2.data != key_2:
            prev_2 = curr_2
            curr_2 = curr_2.next

        # If either key is not found
        if not curr_1 or not curr_2:
            return

        # Update prev_1 to point to curr_2
        if prev_1:
            prev_1.next = curr_2
        else: # key_1 is head
            self.head = curr_2

        # Update prev_2 to point to curr_1
        if prev_2:
            prev_2.next = curr_1
        else: # key_2 is head
            self.head = curr_1

        # Swap next pointers
        curr_1.next, curr_2.next = curr_2.next, curr_1.next

    def reverse(self):
        """Reverse the linked list"""
        prev = None
        curr = self.head
        while curr:
            next_node = curr.next  # Store next node temporarily
            curr.next = prev       # Reverse the link
            prev = curr            # Move prev one step forward
            curr = next_node       # Move curr one step forward
        self.head = prev

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

    print("\n[Test] Delete 'Point B':")
    llist.delete_node("Point B")
    llist.print_list()
    
    print("\n[Test] Reverse Route (Returns Management):")
    llist.reverse()
    llist.print_list()
```

## 🏥 Business Application
- Logistics (Route Management): Managing a delivery route with a Linked List (e.g., "Warehouse -> Point A -> Point B -> Point C"). If a delivery to Point B is cancelled (Deletion), we only need to update Point A's destination to Point C without reconstructing the whole route. (配送ルートをLinked Listで管理する（倉庫 -> 地点A -> 地点B -> 地点C）。 もし「地点B」への配送がキャンセル（Deletion）になった場合、ルート全体を作り直す必要はなく、「地点A」の行き先を「地点C」に書き換えるだけで済む。)

- Logistics (Reverse Logistics): While a normal route (Warehouse -> A -> B) is for delivery, a return route operates in the opposite direction (B -> A -> Warehouse). The Linked List Reverse operation can be applied to simulate this route inversion efficiently. (通常の配送ルート（Warehouse -> A -> B）が「納品」なら、返品回収ルートはその逆（B -> A -> Warehouse）。 Linked Listの Reverse 操作は、この「順路の逆転」をシミュレーションするのに使える。)

## 🔮 Future Work
- Merging Two Sorted Linked Lists
- Remove Duplicates
- Nth-to-Last Node