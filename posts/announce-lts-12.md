---
author: Dan Burton
title: "Announce: Stackage LTS 12 with ghc-8.4.3"
description: "Announce: Stackage LTS 12 with ghc-8.4.3"
timestamp: 2018-07-09T00:01:00Z
---

We are pleased to announce the release of
[lts-12.0](https://www.stackage.org/lts-12.0),
the first in a new
[LTS Haskell](https://github.com/commercialhaskell/lts-haskell#readme)
snapshot series, using ghc-8.4.3.
(See: [changes from lts-11.17](https://www.stackage.org/diff/lts-11.17/lts-12.0).)
We thank all of the package authors involved in supporting
the Haskell ecosystem. LTS Haskell would not be possible without you!

To add your package to future snapshots in the LTS 12 series,
please open a new issue on
[commercialhaskell/lts-haskell](https://github.com/commercialhaskell/lts-haskell).

As per our usual
[LTS release procedure](https://github.com/commercialhaskell/stackage/blob/master/CURATORS.md#new-lts-major-bump),
we have lifted many constraints from the Stackage nightly build plan.
Various packages were removed in order to accomplish this,
and package authors should have been
notified on the corresponding github issues.
To add (or restore) your package to the Stackage nightly builds,
see [MAINTAINERS.md](https://github.com/commercialhaskell/stackage/blob/master/MAINTAINERS.md#adding-a-package) on the stackage repo.

It is uncertain at this time whether LTS 13
(anticipated to release in 3 to 5 months)
will use ghc-8.4 or ghc 8.6.
We encourage package authors to make use of the ghc
alpha and rc releases in order to test their packages
and speed up the adoption of new ghc versions.
