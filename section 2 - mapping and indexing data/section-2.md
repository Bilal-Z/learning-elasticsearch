# Mapping and Indexing Data

## Mapping

Only need to define mapping if something needs to be specifically set to a certain type.  
Or else type inference is used.

**Schema Definition**

- **Feild Types**
- **Feild Index**  
  do you want this feild indexed for full text search?  
  analyzed/ not analyzed.
- **Feild Analyzers**
  - **tokenizer**  
    how to split stringswhitespace, punctuation etc
  - **token filter**  
    lowercase, uppercase, remove stop words ("a", "the", "is", etc.), add tokens (eg synonyms), stemming etc
  - **character filter**  
    remove html encoding etc.

## Choices for analyzers

- **Standard**  
  Split on word boundaries, remove punctuation, lowecases, good choice if language is unknown.
- **Simple**  
  Splits on anything that isnt a letter and lowercases.
- **whitespace**  
  Split on whitespace but doesnt lowercase.
- **language**
- accounts for language specific stop words and does stemming.

## Versions

Every document has a version feild.

Elasticsearch documents are immutable

When you update an existing document:

- new doc created with incremented_version
- old doc marked for deletion

## Dealing with Concurrency

Optimistic concurrency control

- sequence number
- primary shard that owns sequence

use `retry_on_conflicts = N` to auto retry

## Cotrolling full text search

**Using Analyzers**

- Sometimes text feilds should be exact-match
  - Use `keyword` mapping instead of `text`
- Search on analyzed `text` feilds will return anything remotely relevant.
  - Depending on the analyzer results will be case insensitive, stemmed, stopwords removed. synonyms applied etc.
  - Searches with multiple terms need not match them all.
