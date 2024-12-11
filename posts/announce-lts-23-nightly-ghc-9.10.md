---
author: Jens Petersen
title: LTS 23 release for ghc-9.8 and Nightly now on ghc-9.10
description: Stackage LTS 23 (ghc-9.8.4) has been released and Stackage Nightly moved to ghc-9.10.1.
timestamp: 2024-12-12T07:00:00Z
---

## Stackage LTS 23 has been released

The Stackage team is happy to announce that [Stackage LTS version 23](https://www.stackage.org/lts-23.0) has finally been released a couple of days ago, based on GHC stable version 9.8.4. It follows on from the LTS 22 series which was the longest lived LTS major release to date (with probable final snapshot lts-22.43).

LTS 23 includes many [package changes](https://www.stackage.org/diff/lts-22.43/lts-23.0), and almost 3200 packages!
Thank you for all your nightly contributions that made this release possible: the initial release was prepared by Jens Petersen.
(The closest nightly snapshot to lts-23.0 is [nightly-2024-12-09](https://www.stackage.org/diff/nightly-2024-12-09/lts-23.0), but lts-23 is just ahead of it with pandoc-3.6.)

***Dedication**: We are dedicating the LTS 23 release to the memory of Chris Dornan, who left this world suddenly and unexceptedly around the end of May. We are indebted to Christopher for his many years of wide Haskell community service, including also being one of the Stackage Curators up until the time he passed away. He is warmly remembered.*

If your package is missing from LTS 23 and can build there, you can easily have it added by opening a PR in [lts-haskell](https://github.com/commercialhaskell/lts-haskell/) to the [build-constraints/lts-23-build-constraints.yaml](https://github.com/commercialhaskell/lts-haskell/blob/master/build-constraints/lts-23-build-constraints.yaml) file.

## Stackage Nightly updated to ghc-9.10.1

At the same time we are excited to move [Stackage Nightly](https://www.stackage.org/nightly) to GHC 9.10.1: the initial snapshot release is [nightly-2024-12-11](https://www.stackage.org/nightly-2024-12-11).  Current nightly has over 2800 packages, and we expect that number to grow over the coming weeks and months: we welcome your contributions and help with this.
This initial release build was made by Jens Petersen (64 commits).

Most of our upperbounds were dropped for this rebase so quite a lot of packages had to be disabled.
You can see all the [changes](https://www.stackage.org/diff/nightly-2024-12-09/nightly-2024-12-11) made relative to the preceding last 9.8 nightly snapshot.
Apart from trying to build yourself, the easiest way to understand why particular packages are disabled is to look for their `< 0` lines in [build-constraints.yaml](https://github.com/commercialhaskell/stackage/blob/master/build-constraints.yaml), particularly under the `"Library and exe bounds failures"` section.
We also have some [tracking issues](https://github.com/commercialhaskell/stackage/issues?q=is%3Aissue+is%3Aopen+label%3Aghc-9.10) still open related to 9.10 core boot libraries.

Thank you to all those who have already done work updating their packages for ghc-9.10.

Adding or enabling your package for Nightly is just a simple [pull request](https://github.com/commercialhaskell/stackage/blob/master/MAINTAINERS.md#adding-a-package) to the large [build-constraints.yaml](https://github.com/commercialhaskell/stackage/blob/master/build-constraints.yaml) file.

If you have questions, you can ask in Stack and Stackage Matrix room (`#haskell-stack:matrix.org`) or Slack [channel](https://haskell-foundation.slack.com/archives/C023DF5202X).
