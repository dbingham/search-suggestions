[Algorithms Overview](./Algorithms.md)

### Initial Seed

```
ForEach article In articles //O(a)
  index := SHash.length //O(1)
  entry := { "phrase": article.title, "lastused": 0, "count", 0 }
  
  SHash.add(index, entry) //O(1)
  RHash.add(article.title, index) //O(1)
  
  ForEach word In article.title //O(n)
    If word NotIn stopWords AND word.length > 2 //O(1)
      For i From 3 To word.length //O(n)
        prefix := word.substring(0, i) //O(1)
        setAdd("qs:prefix:"+prefix, index) //O(1)
```

**Runtime Complexity: O(a*n^2)** where `a` is the number of articles being index and `n` is the length of the title. In practice `n` is expected to be quite small on average (on the order of 10s).