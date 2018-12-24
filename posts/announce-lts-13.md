---
author: Dan Burton
title: "Announce: Stackage LTS 13 with ghc-8.6.3"
description: "Announce: Stackage LTS 13 with ghc-8.6.3"
timestamp: 2018-12-24T00:01:00Z
---

We are pleased to announce the release of
[lts-13.0](https://www.stackage.org/lts-13.0),
the first in a new
[LTS Haskell](https://github.com/commercialhaskell/lts-haskell#readme)
snapshot series, using ghc-8.6.3.
(See: [changes from lts-12.25](https://www.stackage.org/diff/lts-12.25/lts-13.0).)
'Tis always the season to be jolly around here, due to perpetual effort from
the many package maintainers involved in supporting the Haskell ecosystem.
LTS Haskell is made possible by your hard work. Thank you!

The LTS 13 series can add even more packages with each new snapshot (released weekly).
To add a package to future snapshots in the LTS 13 series,
please open a new issue on
[commercialhaskell/lts-haskell](https://github.com/commercialhaskell/lts-haskell).

As per our usual
[LTS release procedure](https://github.com/commercialhaskell/stackage/blob/master/CURATORS.md#new-lts-major-bump),
we have lifted many constraints from the Stackage nightly build plan.
Various packages may have been removed in order to accomplish this;
package authors should have been notified on the github issue justifying the removal.
However, we generally look at package removals as temporary.
To add (or restore) your package to the Stackage nightly builds,
see [MAINTAINERS.md](https://github.com/commercialhaskell/stackage/blob/master/MAINTAINERS.md#adding-a-package)
on the stackage repo for instructions and details.

We continue to encourage package authors to make use of ghc
alpha, beta, and rc releases. Thank you again for your efforts to keep
Haskell's library releases timely and relevant.
