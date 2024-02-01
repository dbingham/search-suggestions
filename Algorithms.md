## Algorithm Overview
While complexity is provided for each algorithm, see the algorithm's detail page for more information regarding expected behavior.

### Score & Rank
In various places in the algorithms below, it will be necessary to score and rank potential suggested search phrases.

[Score & Rank Algorithm](./ScoreRank.md)

_Complexity: O(n\*log(n) + n)_

### Document Addition
To improve efficiency, a distinction will be made between the initial seeding of the dataset and document additions after the system is entered into usage.

#### Initial Seed
When initially creating the dataset from the corpus of documents available, it is possible to optimize the insertion beyond what is possible in the general purpose addition of data.

[Initial Seed Algorithm](./InitialSeed.md)

_Complexity: O(a\*n^2)_

#### Add Entry
This algorithm would be used for adding data either due to the ingestion of a new document or the indexing of a search string.

[Add Entry Algorithm](./AddEntry.md)

_Complexity: O(n^2\*m\*log(m) + n^2\*m)_

### Document Removal
Removing a document is a simple operation.

[Document Removal Algorithm](./DocumentRemoval.md)

_Complexity: O(1)_

### Document Update
The only data that can change is article titles (historical queries are static). In this case, it is sufficient to remove the old title and add the new one.

[Document Removal Algorithm](./DocumentRemoval.md)
[Add Entry Algorithm](./AddEntry.md)

_Complexity: O(n^2\*m\*log(m) + n^2\*m) As described in Add Entry._

### Suggestion Lookup
This algorithm is performance critical and tradeoffs on performance of the algorithms above were made to improve performance of this algorithm.

[Suggestion Lookup Algorithm](./SuggestionLookup.md)

_Complexity: O(m\*log(m) + n\*m + n + m)_