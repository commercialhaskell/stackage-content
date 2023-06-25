---
author: Jens Petersen and Andreas Ländle
title: LTS 21 release for ghc-9.4 and Nightly now on ghc-9.6
description: Stackage LTS 21 (ghc-9.4.5) has been released and Stackage Nightly moves to ghc-9.6.2.
timestamp: 2023-06-25T06:00:00Z
---

## Stackage LTS 21 has been released

The Stackage team is very happy to announce the first [Stackage LTS version 21](https://www.stackage.org/lts-21.0) snapshot has been released this week, based on GHC stable version 9.4.5.

LTS 21 includes many [package changes](https://www.stackage.org/diff/lts-20.26/lts-21.0), and again has over 3000 packages!
Thank you for all the nightly contributions that made this possible.
(By the way lts-21.0 is basically identical to [nightly-2023-06-20](https://www.stackage.org/nightly-2023-06-20).)

If your package is missing from LTS 21 and builds there, you can easily request to have it added using our straightforward process: just open a github issue in the [lts-haskell](https://github.com/commercialhaskell/lts-haskell/issues) project and following the simple steps in the template.

## Stackage Nightly updated to ghc-9.6.2

At the same time we are also excited to have moved [Stackage Nightly](https://www.stackage.org/nightly) to GHC 9.6.2: the initial snapshot being [nightly-2023-06-22](https://www.stackage.org/nightly-2023-06-22).  Current nightly has over 2470 packages, but we expect that number to continue to grow over the coming days, weeks, and months: we very much welcome your contributions and help with that.

Apart from the usual bounds issues (we [dropped](https://github.com/commercialhaskell/stackage/pull/7010/files) nearly all our blocking upperbounds on packages), the main breakage reasons for disabling packages relative to lts-21 were:

- mtl-2.3 no longer re-exporting from Control.Monad etc
- optparse-applicative-0.18 changes to help prettyprinting exports
- unix-2.8 changing the API of openFd.

Thank you to all those who have already done work updating their packages to ghc-9.6.

Adding or enabling your package for Nightly is just a simple [pull request](https://github.com/commercialhaskell/stackage/blob/master/MAINTAINERS.md#adding-a-package) to a large yaml file.

Happy Stackage building!
