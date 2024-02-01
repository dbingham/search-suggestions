[Algorithms Overview](./Algorithms.md)

### Add Entry

```
//O(n*w*m*log(m) + n*w*m)
// Where:
//   n = length of phrase
//   w = length of a word
//   m = number of indexes in PSet
// Worst case n = w and complexity is:
// O(n^2*m*log(m) + n^2*m)
def UpdatePrefixes(entry: SHash, phrase: String):
  ForEach word In phrase //O(n)
    If word NotIn stopWords AND word.length > 2 //O(1)
      For i From 3 To word.length //O(w*(m*log(m) + m))
        prefix := word.substring(0, i) //O(1)
        key := "qs:prefix:"+prefix
        indexes := setGet(key) //O(1)
        (scored, unscored, missing) := ScoreRank(indexes) //O(m*log(m) + m)
        lowest := scored.tail.score //O(1)
        
        setRemoveAll(key, missing) //O(m)
        
        If scored.length EqualTo 100 AND count >= lowest
          setRemove(key, scored.tail.index) //O(1)
          setAdd(key, entry) //O(1)
        ElseIf scored.length EqualTo 99
          setRemoveAll(key, unscored) //O(m)
          setAdd(key, entry) //O(1)
        ElseIf scored.length < 99
          setAdd(key, entry) //O(1)

If phrase ExistsIn RHash
  index := RHash[phrase] //O(1)
  entry := SHash[index]  //O(1)
  
  entry.lastused := now()
  entry.count += 1
  SHash.update(index, entry) //O(1)
  
  UpdatePrefixes(entry, phrase) //O(n^2*m*log(m) + n^2*m)
Else
  entry := {"phrase": phrase, "lastused": now(), "count": 1}
  index := SHash.length //O(1)
  
  SHash.add(index, entry) //O(1)
  RHash.add(phrase, index) //O(1)
  
  UpdatePrefixes(entry, phrase) //O(n^2*m*log(m) + n^2*m)
        
```

**Runtime Complexity: O(n^2*m*log(m) + n^2*m)** where `n` is the length of the phrase being added and `m` is the number of indexes in each PSet. In practice, it is expected that both `n` and `m` will be quite small (`n` on the order of 10s, and `m` on the order of 100s).