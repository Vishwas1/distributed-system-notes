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

- **write-through**
  - Data is written to the cache and the backing store location at the same time. The significance here is not the order in which it happens or whether it happens in parallel. 
  - I/O completion is only confirmed once the data has been written to both places.
- **write-back**
  - Data is written to the cache and Then I/O completion is confirmed. 
  - The data is then typically also written to the backing store in the background but the completion confirmation is not blocked on that.
- **write-around**
  - data is written only to the backing store without writing to the cache.
  - I/O completion is confirmed as soon as the data is written to the backing store.
  

https://shahriar.svbtle.com/Understanding-writethrough-writearound-and-writeback-caching-with-python
