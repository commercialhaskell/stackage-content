---
author: Michael Snoyman
title: New Stackage snapshot format
description: "We've been making some changes to how we build Stackage snapshots, and the file format used. This post covers those changes, and what's coming next."
timestamp: 2019-07-04T13:00:00Z
---

I've been blogging off-and-on about [Pantry](https://www.stackage.org/package/pantry-tmp) and how it affects both Stack and Stackage. There have been a number of Github issues lying around about changes to how we'll build Stackage snapshots. Most of those changes have landed, and it's worth recapping the problems we were trying to solve, how things used to work, how they work now, and what's left.

## Old build process overview

The [`stackage`](https://github.com/commercialhaskell/stackage/) repo has a [`build-constraints.yaml`](https://github.com/commercialhaskell/stackage/blob/master/build-constraints.yaml) file, which specifies which packages should be included in the next nightly, which tests are expected to fail, upper bounds, etc. The file is where most people interact with the Stackage project, where pull requests land, and where the Stackage Curator team applies changes.

The [`stackage-curator`](https://github.com/fpco/stackage-curator/) tool is used on Travis CI to put together the constraints file with the current state of Hackage to come up with a snapshot, and then check to make sure all of the bounds on that snapshot are valid. When you get an issue from someone on the Curator team reporting bounds failures, it's a report from `stackage-curator`.

We run a build server that rebuilds nightly snapshots on a regular basis. It uses the `stackage-curator` tool as well to create the snapshot definition, perform the build, run tests, upload Haddocks to Amazon S3, and commit the new snapshot file to the [`stackage-nightly`](https://github.com/commercialhaskell/stackage-nightly/) repo. If there are build failures, the Stackage Curator team reports on them and adds more constraints to work around them.

LTS snapshots are basically the same thing, except for an LTS minor version bump, the constraints come from the previous snapshot (e.g., `lts-13.22` is based on the constraints implicit in `lts-13.21`), and the snapshots are committed to the [`lts-haskell`](https://github.com/commercialhaskell/lts-haskell/) repo.

Finally, [Stackage Server](https://github.com/fpco/stackage-server/) (a.k.a. [stackage.org](https://www.stackage.org/)) takes information from `stackage-nightly`, `lts-haskell`, and the uploaded docs on S3 to provide everything it does: lists of snapshots, packages, Haddocks, and Hoogle search.

## Problems

* `stackage-curator` implements its own Cabal package building logic by working directly with Cabal-the-library. There's a lot of feature overlap with Stack, and different behavior in some corner cases.
* The original Stackage file format used in `stackage-nightly` and `lts-haskell` is unique from the "custom snapshot" format that Stack supports, for only historical reasons.
* The snapshot format is _big_. It contains a lot of information about module names, constraints, users, etc, that build tools don't need.
* While there is cryptographic hash information on cabal files to deal with Hackage Revisions, there is no cryptographic hash information on the package tarball contents themselves.

## Changes

* We're scrapping the previous `stackage-curator` tool entirely.
* There's a brand new `curator` tool, which uses the same snapshot format as Stack 2, Pantry, and what was previously known as custom snapshots.
* This curator tool still does bounds checking, and is now included in Travis CI. However, this tool does _not_ build packages. It shells out to Stack to do that instead. That makes this tool _much_ simpler.
* __Important end user consideration__: the old tool would automatically add dependencies of packages to a snapshot. After some discussion and lots of requests around this, __all packages to be included in a snapshot must appear explicitly in `build-constraints.yaml`__. Some people have already gotten reports about this, which is what initially spurred this blog post.
* New snapshots are landing in the [`stackage-snapshots`](https://github.com/commercialhaskell/stackage-snapshots/) repo.
* For backwards compatibility, we currently convert snapshots to the original format in the original repos, so `stackage-nightly` and `lts-haskell` are still being populated. This will not continue indefinitely, we do not have a timeframe on when we will discontinue this.

## Current status

We've moved over Nightly builds completely to the new tool. We have not yet moved LTS Haskell over. Due to differences in how constraints are tracked, we're going to make the switchover when we release LTS 14. We'll put out a separate post about LTS 14 fairly soon.

## Takeaways

The two most important takeaways for most people are:

1. If you depend on a package that's not present in Stackage, you'll need to add that package to Stackage to get your package included.
2. If you're writing tooling that uses the snapshot files, you should check out `stackage-snapshots` and the `pantry` library.
