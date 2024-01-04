---
author: Jens Petersen
title: LTS 22 release for ghc-9.6 and Nightly now on ghc-9.8
description: Stackage LTS 22 (ghc-9.6.3) has been released and Stackage Nightly moved to ghc-9.8.1.
timestamp: 2024-01-04T04:00:00Z
---

## Stackage LTS 22 has been released

The Stackage team is happy to announce that [Stackage LTS version 22](https://www.stackage.org/lts-22.0) was released last month, based on GHC stable version 9.6.3.

LTS 22 includes many [package changes](https://www.stackage.org/diff/lts-21.25/lts-22.0), and has over 3300 packages!
Thank you for all the nightly contributions that made this release possible: the release was made by Mihai Maruseac.
(The closest nightly snapshot to lts-22.0 is [nightly-2023-12-17](https://www.stackage.org/diff/lts-22.0/nightly-2023-12-17).)

If your package is missing from LTS 22 and builds there, you can easily request to have it added by (*new*) opening a PR in the [lts-haskell](https://github.com/commercialhaskell/lts-haskell/) project to the [build-constraints/lts-22-build-constraints.yaml](https://github.com/commercialhaskell/lts-haskell/blob/master/build-constraints/lts-22-build-constraints.yaml) file.
The new LTS workflow was implemented by Adam Bergmark and first appeared in [lts-22.1](https://www.stackage.org/lts-22.1):
we are in the process of updating our documentation to cover the new nightly-style workflow for LTS snapshots.

## Stackage Nightly updated to ghc-9.8.1

At the same time we are excited to have moved [Stackage Nightly](https://www.stackage.org/nightly) to GHC 9.8.1: the initial snapshot being [nightly-2023-12-27](https://www.stackage.org/nightly-2023-12-27).  Current nightly has over 2400 packages, but we expect that number to continue to grow over the coming days, weeks, and months: we very much welcome your contributions and help with this.
You can see all the [changes](https://www.stackage.org/diff/nightly-2023-12-26/nightly-2023-12-27) made relative to the preceding last 9.6 nightly snapshot.
The initial snapshot was done by Alexey Zabelin and Jens.

Thank you to all those who have already done work updating their packages to ghc-9.8.

Adding or enabling your package for Nightly is just a simple [pull request](https://github.com/commercialhaskell/stackage/blob/master/MAINTAINERS.md#adding-a-package) to the large [build-constraints.yaml](https://github.com/commercialhaskell/stackage/blob/master/build-constraints.yaml) file.

If you have questions you can also ask in the Slack [#stackage channel](https://haskell-foundation.slack.com/archives/C023DF5202X).

## New HF server

We would also like to take this opportunity to thank the Haskell Foundation for providing the new upgraded Stackage build-server (setup by Bryan Richter, along with other stackage.org migration), which has greatly helped our daily work with much increased performance and storage.
