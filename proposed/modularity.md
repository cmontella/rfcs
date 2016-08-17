Discussion: https://github.com/witheve/rfcs/issues/9

# RFC - Data and code modularity through "collections"

## Summary

## Motivation

* Reuse of code
* Reuse of data
* Encapsulation

## Design

### Terminology

Collection
Alternatives: module, library, bag, bucket, batch, container, volume, dataset

### Design Goals

### Semantics

Collections are containers of facts and code.

Composition
  Creating collections that are compositions vs runtime composition
  Types
    Completely isolated loading of a collection
    Write isolated loading, including rebinding
    Completely merged
    Data only?
    Code only?
  Logs
  Integrity constraints

Built-in collections
  session
  global
  browser
  file

### Syntax

```
  // match against all bags in the default composition
  match
  // match against only galaga
  match @galaga
  // match against galaga and instance
  match (@galaga, @instance)
  // match against math and the default composition
  match (@math, @default)
```

```
  // bind into session, these are equivalent
  bind
  bind @session
  // bind into galaga
  bind @galaga
  // bind into both galaga and instance
  bind (@galaga, @instance)

  // commit into session, these are equivalent
  commit
  commit @session
  // commit into galaga
  commit @galaga
  // commit into galaga and instance
  commit (@galaga, @instance)
```

```
  bind
    [#collection @galaga url: ""]
```

### Changes to the runtime

* Match can optionally take a set of collections to search in. If none is given, we use the default composition.
* Bind/Commit can optionally take a set of collections to write to. If none is given, we use the default composition.
* We can load a collection by creating a `[#collection]` record.
* Collections can be added to the default composition through attributes on a collection record.
* Every collection internally has both bound and committed facts, which means each user-level collection is two internal collections.

