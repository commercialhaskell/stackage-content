---
author: Michael Snoyman
title: Discontinuing legacy snapshots
description: "We are no longer going to be producing the legacy, pre-Pantry snapshot files."
timestamp: 2020-02-04T08:24:47Z
---
Seven months ago, we [announced a new Stackage snapshot format](https://www.stackage.org/blog/2019/07/new-snapshot-format) based on the work in Pantry. This snapshot format provides a number of advantages over the previous format:

* It's smaller, leading to less bandwidth usage
* It provides for more download checks by including pantry trees
* With the advent of Casa, it allows for even more help with download caching, mirroring, and behind-the-firewall
* It's consistent with Stack's existing custom snapshot format
* It allows for packages to be specified outside of Hackage, such as arbitrary tarballs

For the past seven months, we've been generating new snapshots in the new format, and running a job to convert snapshots to the legacy format. This allows tools that have not yet updated to continue using newer snapshots.

As we mentioned at announcement, though, we wouldn't be continuing that conversion indefinitely. Today, we're announcing that within the next two weeks (likely sooner), we'll be turning off that job. It's never been automated correctly, has taken some work, and prevents us from using outside-of-Hackage packages.

Our plan is to continue converting LTS 14 files to the legacy format, but on the cut-off date suspend nightly legacy files, and never convert LTS 15 files to the legacy format at all.

## How this affects me

All currently existing snapshot files will remain. If you're using Stack 1.9 and an existing LTS or Nightly snapshot, that combination will continue to work indefinitely. However, you will not be able to use Stack 1.9 or earlier with newer snapshots. Additionally, the `stack new` and `stack init` features with older Stack versions will begin to fail without being explicitly told which snapshot to use.

At the time of writing, I don't know if other downstream projects of Stackage have migrated to the new snapshot file format. If they have, users of those tools will experience no impact. Otherwise, they will not be able to use new snapshots until converting over.
