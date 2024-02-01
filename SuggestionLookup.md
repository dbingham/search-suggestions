[Algorithms Overview](./Algorithms.md)

### Suggestion Lookup

```
prefixes := []
ForEach word In typed //O(n)
  prefixes += word
indexes := setIntersect(prefixes) //O(n*m)
(scored, unscored, _) := ScoreRank(indexes) //O(m*log(m) + m)
return (scored ++ unscored).take(10) //O(m)
```

**Runtime Complexity: O(m*log(m) + n*m + n + m)** where `n` is the length of the typed phrase and `m` is the number of indexes in the smallest prefix set.  In practice, both `n` and `m` are expected to be quite small with `n` being on the order of 10s and `m` on the order of 100s in the typical case and 1000s in the worst case.