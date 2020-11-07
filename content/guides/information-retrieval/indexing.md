---
date: "2020-10-10"
description: ""
draft: true
lastmod: "2020-10-11"
layout: section
title: "Information Retrieval: Indexing"
type: guide
url: /guides/information-retrieval/indexing/
---

At the core of information retrieval is the data structure that makes everything
possible: the inverted index. This section is about building and maintaining an
inverted index and how operations such as insertions and deletions work.

Through this section, we'll build a simple-but-not-conrived inverted index
implementation in Python.

## TL;DR

* An inverted index maps terms to the documents they occur in and the position
  in that document.
* Inverted index support two operations: insertion and deletion. Updates are
  support too, but they're compiled down to an insert-and-delete operation.
* Inverted indices tend to be large and need to be compressed.
* Because the indices are large, they're frequently stored partially in-memory
  and partially on-disk.
* Maintaining the on-disk indices efficiently is non-trivial.

## Outline

* Indexing
  * Inverted Index
    * Data Structures
      * API
      * Dictionary
        * Hash-Based
        * Sort-Based
      * Postings List
    * Storage Backend
      * In-Memory
      * On-Disk
    * Operations
      * Insertion
      * Deletion
      * Updates as Insert-and-Delete
    * Maintenance
      * Index Partitioning
      * Index Merging
    * Compression
      * Postings List
        * Huffman LLRUN Coding
        * Variable-Byte Coding
        * Document Reordering
      * Dictionary
        * Front Coding
        * Interleaving
    * Garbage Collection
    * Types of Indices
      * Filter Index
      * Frequency Index
      * Positions Index

## Source Code

In many ways, an inverted index is basically a specialization of Python's `dict`
type. The `dict` type forms the base of our `InvertedIndex` class:

```py3
class InvertedIndex:
    def __init__(self) -> None:
        self._mapping = {}
```

As mentioned, the index will support both `.insert()` and `.delete()`, so we can
go ahead and stub those too:

```py3
class InvertedIndex:
    # def __init__(self) -> None: ...
    
    def delete(self, document: Document) -> None:
        pass
 
    def insert(self, document: Document) -> None:
        pass
```

{{< trusted >}}
<p style="display: flex;">
  <span>
    <a href="/guides/information-retrieval/text-analysis/">
      &larr; Previous: Text Analysis
    </a>
  </span>

  <span style="margin-left: auto;">
    <a href="/guides/information-retrieval/retrieval/">
      Next: Retrieval &rarr;
    </a>
  </span>
</p>
{{< /trusted >}}