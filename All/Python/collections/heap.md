# Heap

Builtin min heap, where you need efficient access to the minimum or maximum element like priority queue

```python
import heapq

# Create an empty heap
heap = []

# Insert elements
heapq.heappush(heap, 10)
heapq.heappush(heap, 15)
heapq.heappush(heap, 20)
heapq.heappush(heap, 5)

print("Heap:", heap)

# Peek (get the smallest element without removing it)
min_element = heap[0]
print("Min element:", min_element)

# Extract the smallest element
min_element = heapq.heappop(heap)
print("Extracted min element:", min_element)
print("Heap after extraction:", heap)

# Heapify an existing list
nums = [30, 10, 20, 5, 40, 25]
heapq.heapify(nums)
print("Heapified list:", nums)
```

