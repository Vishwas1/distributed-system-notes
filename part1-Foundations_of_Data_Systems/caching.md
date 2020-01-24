# Caching

## Why
- Save Network calls
- Avoid redundant computations
- Reducde DB load

## When to load data on cache?

Loading or evicting data is called **caching policy**.

### caching policy

- LRU: Least Recently Used
- LFU: Least Frequently Used 
- Sliding window based policy


### Problem with poor eviction policy

- Extra call
- Tharashing
- Consistency problem


### Cache writing policies

- write-through 
  - Data is written to the cache and the backing store location at the same time. The significance here is not the order in which it happens or whether it happens in parallel. 
- write-back
  - Data is written to cache after its been written to store.
  


