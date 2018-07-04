# Performance

- Prefer Vector over List
- Use a set instead of filtering over everything if you plan on getting more than a couple elements out of a collection. e.g. just because list.filter achieves the same result as set.contains, use a set if appropriate.
- In concurrent programs with a write/read ratio less than 1/10, use an immutable collection and an atomic reference. You get better (and more consistent) performance out of an immutable hash set and an atomic reference for both reads and writes than a ConcurrentHashMap.

