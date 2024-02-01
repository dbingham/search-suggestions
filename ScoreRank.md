[Algorithms Overview](./Algorithms.md)

### Score & Rank

```
def ScoreRank(indexes: List):
  ForEach index In indexes //O(n)
    If index ExistsIn SHash
      entry := SHash[ndex]
      If entry.count > 0
        score := entry.count / (now - entry.lastused)
        scored += (index, score)
      Else
        unscored += index
    Else
      missing += index
  return (scored.sort, unscored, missing) //O(n*log(n))
```

_syntax note: (one, two) represents a Tuple_

Where sorting is done first by score, then lexographically using the phrase from the SHash.

**Runtime Complexity: O(n*log(n) + n)** where `n` is the number of indexes provided to the function. In practice `n` is expected to be on the order of 100s on average, and 1000s in worst case.