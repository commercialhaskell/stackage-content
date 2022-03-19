---
author: Jens Petersen
title: LTS 19 release and Nightly on ghc-9.2
description: Stackage LTS 19 (ghc-9.0.2) has been released and Stackage Nightly moves to ghc-9.2.2.
timestamp: 2022-03-20T05:00:00Z
---

The Stackage team is very happy to announce the initial [Stackage LTS version 19](https://www.stackage.org/lts-19.0) snapshot release is now available, based on GHC version 9.0.2. This release is significant for several reasons:

- not only is it the first stable LTS release based on ghc9,
- it also includes many significant [upgrades](https://www.stackage.org/diff/lts-18.28/lts-19.0), including aeson-2.0 with improved security, and
- it is also the largest stable LTS release we have ever done: just 1 short of 2900 packages!

Of course it is still possible to get your package added to lts-19, if it builds with lts19 and you missed to get it into Nightly in time for the initial lts-19.0 build: using our straightforward process - just open a github issue in the [lts-haskell](https://github.com/commercialhaskell/lts-haskell/issues) project and following the template there.

Thank you to the great Haskell community for all the many contributions
you are making - do keep them coming!

At the same time we are also excited to [move Nightly now to GHC 9.2.2](https://www.stackage.org/nightly-2022-03-19) - enjoy!  Apparently there will be a 9.2.3 bugfix release coming, so we will update Nightly to that after it is released.

Quite a number of Nightly packages had to be [disabled](https://www.stackage.org/diff/nightly-2022-03-17/nightly-2022-03-19) as part of the upgrade to 9.2. This is being tracked in <https://github.com/commercialhaskell/stackage/issues/6486>: if you find your package listed there, you can help to update it to build with ghc-9.2 and Stackage Nightly, thank you!

Help us make the next LTS 20 an even bigger and better release!
