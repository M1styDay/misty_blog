---
title: Association：Content(2)
author: "Misty"
tags: ["Association","HKU"]
categories: ["Data Mining"]
date: 2021-01-10
---

# Improvements to A-Priori

## PCY Algorithm

### Introdution

* Main observation: during pass 1 of A-priori, most memory is idle.
* Use that memory to keep additional info to improve storage during pass 2 of A-priori.
* Passes > 2 are the same as in A-Priori.

### Pass 1

* Use a hash function which "bucketizes" item pairs, that is, maps them to integers in $[1,k]$.
* Each "bucket" i in $[1,k]$ is associated with a counter $c_i$. 
* During pass 1, as we examine a basket (e.g. {m,b,d,o}):
    * update counters of single items;
    * Generate all item pairs for that basket, hash each of them and add 1 to the corr. counter.

### Obersvations(1)

* A bucket is frequent if its counter is at least the support threshold s.
* If a bucket is not frequent, no pair that hashes to that bucket could possibly be a frequent pair.
* Therefore, on pass 2 we only count pairs that hash to frequent buckets.

### Obersvations(2)

* A bucket that a frequent pair hashes to is surely frequent.
* Even without any frequent pair, a bucket can be frequent.
* But in the best case, the count for a bucket is less than the support s.
    * Now, all pairs that hash to this bucket can be eliminated as candidates, even if the pair consists of two frequent items.

### Pass 2

* Count all pairs {i, j } that meet the conditions for being a candidate pair:
    * Both i and j are frequent items.
    * The pair {i, j }, hashes to a frequent bucket.

* Ignore all pairs belonging to non-frequent buckets (do not use a counter for them).

### All (Or Most) Frequent Itemsets In < 2 Passes

* A-Priori, PCY, etc., take k passes to find frequent itemsets of size k.
* Other techniques use 2 or fewer passes for all sizes:
    * Simple algorithm.
    * SON (Savasere, Omiecinski, and Navathe).

## Sampling

### Introdution

* Take a random sample of the market baskets.
* Run A-priori or one of its improvements in main memory, so you don’t pay for disk I/O each time you give a pass on the data.
    * Be sure you leave enough space for counts.

* To sample: give a full pass on the data and keep a basket in main memory with probability p (depending on main memory and input size)
* Why do we need to give a full pass just to retain a fraction p of the data?
    * A random sample is the best representative of a dataset. Keeping only the first baskets might not contain iPhones for example.

* Adjust the support threshold s accordingly:
    * E.g., if p=1/100 of the baskets, use s /100 as your support threshold instead of s.

### Errors

* We might have:
    * False positives: items frequent in the sample but not in the dataset.
    * False negatives: items not frequent in the sample but frequent in the dataset.
* If the sample is large enough it is unlikely that we get either of them.

### Improvement

* If we cannot have a sample large enough then
    * Remove false positives with one more pass (count only frequent itemsets in the sample).
    * False negatives: decrease the support threshold (e.g. 0.9ps). This might increase false positives. We might not remove all false negatives.


## SON Algorithm

### Introdution

* Two passes
* No false positives or false negatives.
* Divide the dataset into chunks, where each chunk contains a subset of baskets.

### Pass 1

* Divide the dataset into chunks, where each chunk contains a subset of baskets.
* Let $p_i$ such that the ith chunk contains a fraction $p_i$ of the dataset.
* For each chunk i compute all frequent itemsets with support $p_i$ x s and store them on disk. This is the set of candidates for next pass.

### Pass 2

* Read all frequent itemsets found in the previous pass (candidates).
* For each of them count the number of occurrences and output only those with support at least s.

### Errors

* False positives? 
    * No, because we compute the correct support in the second pass.
* False negatives? 
    * No. Suppose $p_i$ = p for all i. If an itemset is not frequent in any chunk then its support is < ps(1/p)=s (there are 1/p chunks). So it is not frequent in the dataset.
* A similar argument applies for general case.
* The SON algorithm lends itself to a MapReduce implementation...