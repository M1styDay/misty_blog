---
title: Curriculum Overview
author: "Misty"
tags: ["HKU","COMP 7801"]
categories: ["Advanced Topics in Data Management"]
date: 2021-01-08
---

* Course Information 1-27
* Lecture 1 Database Review 28-128
    * Database design and queries
        * Structure of Relational Databases
        * Reduction of an E-R Schema to Tables 
        * Relational Algebra and SQL
        * Storage of relations 
	* Database indexing
    	* Why indexing?
    	* What are the types of indexes that we have in a DBMS?
    	* How does the B+-tree index a relation based on a search key? How are B+-trees updated?
    	* How do hash-based indexes operate?
 
* Lecture 2 Spatial Data Management 129-245
    * Spatial Data
        * Vector representation/raster representation
    * Spatial Relationships
        * Topological relationships
        * Distance relationships
        * Directional relationships
    * Spatial Queries
        * Range query (spatial selection, window query) => SAMs
        * Nearest neighbor query
        * Spatial join
    * Issues in Query Processing 
        * SAMs
        * Two steps (Filter/Refinement)
        * Better: Have the minimum overlap
    * The R-tree
        * How to build (Parameters)
        * Range searching using an R-tree (window query)
        * How to construct/maintain (insert/delete) (similar to B+ tree)
        * R*-tree (differ in the insertion algorithm) (small MBRs/overlap/squares/as full as possible)
        * Node splitting (split axis)
        * Insertion heuristics: Forced Reinsert
        * Bulk-loading R-trees(iteratively/x-sorting/Hilbert sorting/sort-tile-recursive)
    * Spatial Query Processing 
        * Spatial Selections
        * Nearest Neighbor Queries (DF/BF)(incremental NN search
        * Spatial Joins (Three categories: synchronized tree traversal/indexed nested loops/spatial hash join)(multi-step join)(Plane Sweep)
 
* Lecture 3 Spatial Networks 246-290
    * Modeling and storing spatial networks 
    * Shortest path search (Dijkstra’s algorithm/A*/Bi-directional search)
    * Spatial queries over spatial networks (Selections/NN search/Joins)
    * Advanced indexing techniques for spatial networks 

* Lecture 4 Top-k Queries 291-341
    * Background
    * Top-k search methods (Rank aggregation/Index-based methods)
 
* Lecture 5 Uncertain Databases: An Overview 342-394
    * Uncertainty in Applications
    * Problems on Managing Uncertain Data 
        * Model: attribute/tuple uncertainty
        * Probabilistic Queries
        * Data quality and clear
    * Uncertainty Models

* Lecture 6 Probabilistic Queries 395-507
    * Query Classification
        * A review of traditional database queries 
        * Classification of probabilistic queries 
        * Basics of the ORION system 
    * Query Evaluation 
        * Queries that can be evaluated easily
        * Entity-based dependent queries
        * Nearest neighbor queries for 2D objects 
        * Joins 

* Lecture 7 Top-k Queries on Uncertain Data 508-543
    * Top-k queries for exact data
    * Top-k queries for uncertain data
        * U-topk
        * U-kRanks
        * PT-k
        * Global-topk
        * State-Expand (for U-Topk)
  
* Lecture 8 Text Databases 544-581
    * Document databases
    * Containment and similarity queries
    * Indexing for containment and similarity 

* Lecture 9 Uncertainty in Data Integration 582-647
    * Basic
    * Q-sharing
    * O-sharing




&nbsp; 

---

&nbsp; 

## Documents
Name|Link|Password
:---:|:---:|:---:
课程资料|[百度网盘](https://pan.baidu.com/s/1r8PxE-AaebyOeJjH6osl1Q)|550h