---
author: Jens Petersen
title: LTS 20 release for ghc-9.2 and Nightly now on ghc-9.4
description: Stackage LTS 20 (ghc-9.2.5) has been released and Stackage Nightly moves to ghc-9.4.3.
timestamp: 2022-11-19T14:00:00Z
---

## Stackage LTS 20 has been released

The Stackage team is very happy to announce the first [Stackage LTS version 20](https://www.stackage.org/lts-20.0) snapshot has been released this week, based on GHC stable version 9.2.5.

LTS 20 includes many [package changes](https://www.stackage.org/diff/lts-19.32/lts-20.0), and is the first LTS release with over 3000 packages!! Thank you for all the nightly contributions that made this possible.

If your package is missing from LTS 20 and builds there, you can easily request to have it added using our straightforward process: just open a github issue in the [lts-haskell](https://github.com/commercialhaskell/lts-haskell/issues) project and following the steps in the template.

## Stackage Nightly updated to ghc-9.4.3

At the same time we are also excited to have moved Stackage [Nightly to GHC 9.4.3](https://www.stackage.org/nightly-2022-11-19) now!

Almost 500 Nightly packages had to be [disabled](https://www.stackage.org/diff/nightly-2022-11-17/nightly-2022-11-19) as part of the upgrade to 9.4. Please help us to update your packages to build with ghc-9.4 and get them back into Stackage Nightly, thank you!

Big thank you to the community for all your help and support, and do keep the contributions coming!

(_Note for Linux users of older glibc < 2.32_: at the time of writing stack setups for ghc-9.4 default to the fedora33 bindist which uses glibc-2.32. Some possible workarounds are mentioned in [this issue](https://github.com/commercialhaskell/stack/issues/5881) though the Stackage team has not verified the suggestions.)
