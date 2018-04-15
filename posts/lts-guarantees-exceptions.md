---
author: Michael Snoyman
title: LTS Guarantees and Exceptions
description: A proposal for slight tweaks to the LTS guarantees and exceptions
timestamp: 2018-04-15T07:35:00Z
---

I've written up a PR
[slightly tweaking the LTS guarantees and exceptions](https://github.com/fpco/stackage/pull/3526). I
encourage those interested to comment on the PR itself, and/or use the
+1/-1 buttons on the PR description. I'll include the text I'm
suggesting we add to the `MAINTAINERS.md` document here. Note that the
PR may be updated based on feedback, so it's best to read the PR
itself!

* * *

## LTS package guarantees and exceptions

In general, we try to stick to some rules when it comes to the
packages included in LTS minor bumps. In particular:

* If a package exists in LTS-X.Y, it should also exist in LTS-X.(Y+1)
* We should not include a major version bump of a package between
  LTS-X.Y and LTS-X.(Y+1)

However, there are some cases where exceptions may be made, based
purely on Stackage Curator discretion. The most common examples are:

*   If a package does not follow the PVP in its version number policy,
    applying the standard version bump rules would not necessarily
    makes sense. As an example, suppose package `foo` decides to
    follow SemVer instead of the PVP. By our standard rules of version
    bumps, a change from `foo-1.2.0` to `foo-1.3.0` would be
    considered a major version bump, and disallowed in an LTS minor
    version bump. However, if a package is following SemVer, this
    would not be a breaking change, and curators may elect to include
    it.

*   If a package has overly restrictive version bounds on a
    dependency, in particular constraining a minor version
    unnecessarily, we may drop that package instead of artificially
    holding back the dependency. As an example: suppose `LTS-20.1`
    includes `foo-1.2.0` and `bar-1`. `bar-1` has a dependency `foo >=
    1.2.0 && < 1.2.1`, which is overly constrained on the minor
    version number according to the PVP. Then `foo-1.2.1` is
    released. The Stackage Curator team would have two choices:

    * Reject `foo-1.2.1` from `LTS-20.2`, since that is what `bar-1`
      requires.
    * Drop `bar-1` from `LTS-20.2`, and allow `foo-1.2.1`.

    Decisions will need to be taken on a case-by-case basis, and may
    depend on such issues as whether an important bugfix or security
    update in included. The curator team may also try to notify the
    author of `bar` to try and get a patched version released.
