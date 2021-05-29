---
author: Chris Dornan
title: Stackage nightly snapshots to switch to GHC 9.0.1
description: We will be releasing LST-18 and switching nightly to GHC 9
timestamp: 2021-05-29T16:07:00Z
---

We have been looking for an opportunity to switch to GHC-9 on our nightly builds and have decided
that GHC-9 has been out long enough and we need to get on with preparing the ecosystem for its
eventual deployment as the Haskell toolchain of choice. To that end, in the coming weeks we will be

  * releasing LTS 18 based on GHC 8.10.4 (or GHC 8.10.5, should it make
    an appearance) and

  * switching nightly to GHC 9.0.1 (or GHC 9.0.2 if it is released in time).

We can expect many packages to be removed from nightly due to build constraints being violated, or
even real API breakage, and we will need your help getting everything back into the new release.

We have prepared a [ghc-9 branch](https://github.com/commercialhaskell/stackage/pull/6047) which will become the first GHC 9 nightly and encourage you to check the diff to see if any of your packages are subject to removal. If you'd like them to be included in the initial GHC 9 nightly, please file a PR against that branch ([example](https://github.com/commercialhaskell/stackage/pull/6048))

Stand by!
