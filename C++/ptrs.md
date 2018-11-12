# Ptrs

### Advanced

Smart ptrs are meant to solve many ptr problems like leaky mem and dangling ptrs by introducing the concept of ownership

Unique_ptrs are ptrs that can't be copied and delete the underlying mem when the ptr itself is deleted

Shared ptrs keep track of how many ptrs have access to the underlying object and delete the underlying object when there are no more references 

