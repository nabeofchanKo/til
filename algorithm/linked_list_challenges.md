# [Singly Linked Lists: Algorithmic Challenges]

## 💡 What I Learned
- **Merge Two Sorted Lists**: An operation to merge two sorted lists into a single sorted list. It involves creating a dummy node and connecting pointers in ascending order by comparing the head nodes of both lists. (2つのソート済みリストをマージして1つのソート済みリストにする操作。新しいダミーノードを用意し、2つのリストの先頭を比較しながら小さい順にポインタを繋いでいく。)
- **Remove Duplicates**: When removing duplicates from a sorted list, if the current node's value matches the next node's, we simply skip (delete) the next node. This approach is memory-efficient as it does not require a hash map. (ソート済みリストから重複を削除する場合、現在のノードと次のノードの値が同じであれば、次のノードをスキップ（削除）するだけで済む（ハッシュマップ不要でメモリ効率が良い）。)
- **Nth-to-Last Node**: A technique to retrieve the Nth node from the end using the "Two Pointers" method. A "leading pointer" is moved forward by N steps first, then moved simultaneously with a "current pointer." When the leader reaches the end, the current pointer is at the target position. (「後ろからN番目」を取得するテクニック。「先行ポインタ」を先にN歩進め、その後「現在のポインタ」と同時に動かすことで、先行ポインタがゴールに着いた時に現在のポインタが正解の場所にいる（Two Pointers手法）。)
- **Count Occurrences**: Counts how many times a specific value appears in the list. This can be solved via simple traversal. (特定の値がリスト内に何回登場するかをカウントする。単純な探索（Traversal）で解決できる。)
- **Rotate List**: Rotates the list to the right by `k` places. This is efficiently achieved by forming a ring (connecting the tail to the head) and then breaking the link at the calculated new tail position. (指定した回数 k だけリストを回転させる。リストをリング状（末尾を先頭に接続）にしてから、適切な位置で切断することで効率的に実現できる。)
- **Is Palindrome**: Determines if the list is a palindrome (reads the same forward and backward). The most space-efficient method involves reversing the second half of the list and comparing it with the first half, avoiding additional memory usage. (リストが回文（前から読んでも後ろから読んでも同じ）か判定する。リストの後半を「反転（Reverse）」させてから前半と比較する方法が、追加メモリを使わず最も効率的。)

## 💻 Code Snippet
```python
    # Note: These methods are intended to be added to the LinkedList class

    def merge_sorted_lists(self, llist):
        """Merge another sorted linked list into this one"""
        p = self.head 
        q = llist.head
        s = None # Pointer to track the merged list
        
        # If one list is empty, return the other
        if not p: return q
        if not q: return p

        # Set the head of the merged list
        if p.data <= q.data:
            s = p
            p = s.next
        else:
            s = q
            q = s.next
        new_head = s 

        # Traverse and stitch
        while p and q:
            if p.data <= q.data:
                s.next = p
                s = p
                p = s.next
            else:
                s.next = q
                s = q
                q = s.next
        
        # Attach the remaining part
        if not p: s.next = q
        if not q: s.next = p
        
        self.head = new_head # Update head to the merged list

    def remove_duplicates(self):
        """Remove duplicates from a sorted linked list"""
        curr = self.head
        while curr and curr.next:
            if curr.data == curr.next.data:
                curr.next = curr.next.next # Skip the duplicate
            else:
                curr = curr.next

    def print_nth_from_last(self, n):
        """Find the n-th node from the end using Two Pointers"""
        # Method 1: Using Length (Simple)
        total_len = self.get_length()
        if n > total_len or n <= 0:
             return None
        
        curr = self.head
        count = 0
        while curr and count < total_len - n:
            curr = curr.next
            count += 1
        return curr.data
        
        # Note: Method 2 (Two Pointers) is more efficient as it needs only one pass

    def count_occurrences(self, data):
        """Count how many times a specific data occurs"""
        count = 0
        curr = self.head
        while curr:
            if curr.data == data:
                count += 1
            curr = curr.next
        return count

    def rotate(self, k):
        """Rotate the list to the right by k places"""
        if self.head and self.head.next:
            # 1. Calculate length
            length = 0
            curr = self.head
            while curr:
                length += 1
                curr = curr.next
            k = k % length 
            
            # 2. Find the pivot point (length - k - 1)
            p = self.head
            count = 1
            while count < length - k:
                p = p.next
                count += 1
            
            # 3. Rotate
            q = p.next # New head
            p.next = None # Break the link
            
            curr = q
            while curr.next: # Go to the end of new list
                curr = curr.next
            curr.next = self.head # Connect old tail to old head
            
            self.head = q

    def is_palindrome(self):
        """Check if the list is a palindrome (e.g., A -> B -> A)"""
        # String comparison approach (Simplest)
        s = ""
        curr = self.head
        while curr:
            s += str(curr.data)
            curr = curr.next
        return s == s[::-1]
```
## 🏥 Business Application
- Pharma (Genomic Sequence Analysis): In bioinformatics, detecting Palindromic sequences in DNA is crucial (e.g., restriction enzyme cutting sites). The "Is Palindrome" algorithm can be applied to sequence data stored in linked structures to identify these patterns. (バイオインフォマティクスにおいて、DNA配列内の回文構造（Palindrome）の検出は重要。Linked List上のシーケンスデータに対して回文判定アルゴリズムを適用できる。)

- Pharma (Patient Data Cleanup): When merging patient records from different hospital systems, duplicate entries (e.g., same Patient ID sorted by date) often occur. "Remove Duplicates" logic efficiently cleans this data without needing heavy hash maps. (異なる病院システムの患者データを統合する際、ソート済みのIDリストから重複エントリーを削除するのに利用できる。)

- Logistics (Tracking Logs Integration): Merging tracking logs from two different carriers (e.g., Land transport and Air transport) that are already sorted by timestamp. "Merge Two Sorted Lists" allows creating a single unified timeline of the package journey efficiently. (異なる配送業者（陸送と空輸など）からの、時刻順にソートされた追跡ログを1つのタイムラインに統合する際にマージ操作が利用できる。)