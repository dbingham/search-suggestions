[Algorithms Overview](./Algorithms.md)

### Document Removal

```
If phrase ExistsIn RHash
  index := RHash[phrase]
  SHash.remove(index) //O(1)
  RHash.remove(phrase) //O(1)
```

**Runtime Complexity: O(1)**

_Note: The corresponding index is not removed from prefixes as finding them could be quite slow and the penalty for leaving them in-place until the next prefix update is very low._