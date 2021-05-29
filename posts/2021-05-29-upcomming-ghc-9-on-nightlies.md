---
author: Chris Dornan
title: Stackage nightly snapshots to switch to GHC 9.0.1
description: We will be releasing LST-18 and switching nightly to GHC 9
timestamp: 2021-06-29T16:07:00Z
---

We have been looking for an opportunity to switch to GHC-9 on our nightly builds and have decided
that GHC-9 has been out long enough and we need to get on with preparing the ecosystem for its
eventual deployment as the Haskell toolchain of choice. To that end, in the coming weeks we will be

  * releasing LTS 18 based on GHC 8.10.4 (or GHC 8.10.5, should it make
    an appearance) and

  * switching nightly to GHC 9.0.1 (or GHC 9.0.2 if it is released in time).

We can expect many packages to be removed from nightly due to build constraints being violated, or
even real API breakage, and we will need your help getting everything back into the new release.

Stand by!
