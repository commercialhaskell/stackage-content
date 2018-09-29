---
author: Mihai Maruseac
title: Announcing stackage nightly snapshots with ghc-8.6.1
description: Announcing stackage nightly snapshots with ghc-8.6.1
timestamp: 2018-09-29T00:01:00Z
---

I am pleased to announce that Stackage nightly snapshots now use
ghc-8.6.1. Stack users can simply use `resolver: nightly-2018-09-29`
in a project's `stack.yaml` file in order to build and test with ghc-8.6.1.

As is usual when a new ghc is released, many packages were removed
from the nightly snapshot due to version constraints and build failures.
We expect many packages to return quickly to the build plan, and
we hope that the existing snapshots will help mainatainers get back in
by making it easy to build and test their packages.

Please check to see if your favorite packages are in
[the latest nightly snapshot](https://stackage.org/nightly),
and open up a PR or an issue on
[Stackage](https://github.com/commercialhaskell/stackage) if you find anything
missing which is known to work with ghc-8.6.1.

As ghc moves to its new 6-month release cycle, I'd like to encourage everyone
to be proactive in bumping bounds and testing packages you rely on
with the new ghc alphas and release candidates as they come out.
Haskell has a remarkable ecosystem; let's strive to make it even better!

