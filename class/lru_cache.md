# LRU Cache

> Design and implement a data structure for Least Recently Used (LRU) cache. It should support the following operations: get and put.

> get(key) - Get the value (will always be positive) of the key if the key exists in the cache, otherwise return -1.

> put(key, value) - Set or insert the value if the key is not already present. When the cache reached its capacity, it should invalidate the least recently used item before inserting a new item.

> Follow up:

> Could you do both operations in O(1) time complexity?

> Example:

> ```
LRUCache cache = new LRUCache( 2 /* capacity */ );
cache.put(1, 1);
cache.put(2, 2);
cache.get(1);       // returns 1
cache.put(3, 3);    // evicts key 2
cache.get(2);       // returns -1 (not found)
cache.put(4, 4);    // evicts key 1
cache.get(1);       // returns -1 (not found)
cache.get(3);       // returns 3
cache.get(4);       // returns 4
```

dictionary and double linked list. maintain head and tail to do quick add and delete.

```Python
class Node(object):
    def __init__(self, key, val):
        self.key = key
        self.val = val
        self.next = None
        self.prev = None
        
class LRUCache(object):

    def __init__(self, capacity):
        """
        :type capacity: int
        """
        self.capacity = capacity
        self.dic = {}
        self.head = Node(0, 0)
        self.tail = Node(0, 0)
        self.head.next = self.tail
        self.tail.prev = self.head
        

    def get(self, key):
        """
        :type key: int
        :rtype: int
        """
        if key in self.dic:
            n = self.dic[key]
            self.listRemove(n)
            self.listAdd(n)
            return n.val
        return -1
        

    def put(self, key, value):
        """
        :type key: int
        :type value: int
        :rtype: void
        """
        if key in self.dic:
            self.listRemove(self.dic[key])
        n = Node(key, value)
        self.listAdd(n)
        self.dic[key] = n
        if len(self.dic) > self.capacity:
            n = self.head.next
            self.listRemove(n)
            del self.dic[n.key]
    
    
    def listRemove(self, node):
        node.prev.next, node.next.prev = node.next, node.prev
    
    def listAdd(self, node):
        self.tail.prev.next, self.tail.prev, node.prev, node.next = node, node, self.tail.prev, self.tail


# Your LRUCache object will be instantiated and called as such:
# obj = LRUCache(capacity)
# param_1 = obj.get(key)
# obj.put(key,value)
```
