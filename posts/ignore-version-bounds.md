---
author: Michael Snoyman
title: Should Stackage ignore version bounds?
description: Today, Stackage respects version bounds in cabal files. But there's a strong argument to be made that this is an incorrect decision.
timestamp: 2018-01-30T03:26:00Z
---

__NOTE__ The curator team is requesting feedback from the community on this
post. If you have thoughts you'd like to share, please add them to the official
Github discussion issue for this topic: [issue
#3241](https://github.com/fpco/stackage/issues/3241).

As it stands today, __Stackage respects version bounds__. This means
that, if `foo-1.0.0` is included in a snapshot, and its cabal file
says `build-depends: bar >= 1.0 && < 1.1`, that snapshot cannot
include `bar-1.1`. The vast majority of issues open on the Stackage
issue tracker are related to restrictive upper bounds preventing new
versions of dependencies into Stackage.

The question has recently been asked in a few places: __why does
Stackage respect version bounds?__ It makes perfect sense for a
dependency solver to use version bounds to guide its selection process
for constructing a build plan. But Stackage is a curated build
process. We should be able to build a snapshot, run the test suites,
and then say that, despite the package's claims to the contrary, two
versions of a package are in fact compatible.

Such a decision by Stackage would have a theoretically positive impact
on the ecosystem.

* Stackage could more easily upgrade to new versions of dependencies,
  and only hold back packages when actual incompatibility is detected.
    * This would reduce friction amongst package authors, and reduce
      curator efforts.
* The bounds in cabal files could be treated as being important only
  to cabal-install in the dependency solving case.
* Authors who follow the PVP would have less busywork to do regarding
  version bound relaxations.
* Stackage could entirely ignore Hackage's cabal file revisions,
  removing a source of tension (see the
  [Uncurated Hackage Layer](https://github.com/haskell/ecosystem-proposals/pull/6)
  proposal).

I believe these are the general arguments people have as to why
Stackage should ignore version bounds. If people have other reasons I
haven't mentioned here, please bring them up. I want to explain some
motivations for Stackage to continue respecting version bounds, and
then open up a community wide discussion on what the best path forward
is for the project.

## Hard versus soft bounds

When you see `bar >= 1.0 && < 1.1` in a cabal file, it can mean one of two things:

* This package is known to be incompatible with `bar-1.1`
* This package is not known to be compatible with `bar-1.1`

This has come to be known as hard versus soft bounds respectively,
which are currently not representable in cabal metadata. (There is
talk of the new `^>=` operator being used for this purpose, but its
current semantics in the code for Cabal and the documentation is
indistinguishable from the preexisting `>=` and `<` operators. For
more information, see
[Stack issue #3464](https://github.com/commercialhaskell/stack/issues/3464).)
In the case of soft bounds, it makes all the sense in the world for
Stackage to ignore such bounds, and leave them as a
dependency-solving-only concern.

However, hard bounds _do_ exist, and can be used to avoid known build
failures. In the world today where hard and soft bounds are
indistinguishable, choosing to ignore bounds means ignoring _all_
bounds, including known hard bounds. This will result in build
failures on the Stackage build server, and resulting error reports,
with the following problems:

* Package authors may be rightfully confused, and even annoyed, at
  receiving bug reports for build failures _they told us would
  happen_. Is it really fair to subject an author to a build failure
  message for incompatibility with `bar-1.1` if they told us in the
  cabal file that they don't support it?
    * Counterpoint: it could be considered _highly useful information_
      to have these error reports generated, allowing casual users to
      see incompatibilities with new versions of packages, and perhaps
      send PRs to fix them.
* This can waste Stackage Curator time. Instead of getting a version
  bound report and adding a temporary upper bound, us curators will
  now need to let the build server try to build the package, discover
  that it fails, determine which changed dependency caused the
  failure, and then add an upper bound. Counterpoints:
    * In my experience, many cases of restrictive upper bounds require
      no code changes, so the time lost on tracking down the breakage
      here can be saved in not having to file frivolous upper bounds
      reports.
    * This problem already exists, from authors not following the
      PVP. Again, in my experience, the cost has not been particularly
      high.

But a much greater issue is that of _semantic breaking changes_. With
API changes which cause build breakage, we're basically moving around
when detection occurs. But the build failure will _always_ be
detected. If a library introduces a breaking semantic change, there is
no guarantee that the Stackage build process will catch it. Ideally,
such runtime behavior will be tested by a test suite, but there is no
way to guarantee that.

On the other hand: in practice, I don't think this situation arises
often, and I don't think people are particularly good about noticing
these semantic changes and using bounds to inform of them. In other
words, packages that don't have comprehensive test suites won't be
affected by this change, and packages without comprehensive test
suites will likely fall prey to this problem regardless.

## Harder Stackage integration story

Stackage was originally designed to be used by cabal-install via the
`cabal.config` file. Stack has direct support for Stackage
snapshots. To my knowledge, Nix has relatively direct support as
well. There are issues with integration due to Hackage revisions (see,
e.g.,
[Stackage issue #3126](https://github.com/fpco/stackage/issues/3126)),
but things work relatively well.

If we stop respecting version bounds, we will end up with snapshots
regularly which have conflicting version bounds, leading to an extreme
version of issue #3126. Stack is (I believe) already designed to trust
a snapshot's statement about package versions, and ignore any version
conflicts. The same cannot be said of cabal-install and Nix, which I
believe would need to turn on some kind of flag for ignoring version
bounds.

More generally: by ignoring an entire aspect of the Cabal build
system, we're increasing the likelihood of incompatibility with other
tooling.

## Non-version bounds metadata revisions

One aspect mentions above is the ability to entirely ignore Hackage
revisions. That's not a hard requirement for this proposal. But if we
did so, we would need to deal with non-version bounds revisions. While
most Hackage revisions revolve around relaxing or tightening version
bounds, other edits are allowed, like modifying the description field,
or adding custom-setup stanzas. If we ignore these revisions, we'll
end up in a situation where:

* Metadata on Stackage may be confusingly different from that
  displayed on Hackage
* Broken builds that have been fixed via Hackage revisions (such as by
  adding a custom-setup stanza) will still be broken for Stackage,
  resulting in spurious error reports to authors and the same
  confusion/annoyance mentioned above

## Negative impacts on cabal-install users

For the first year or so of its existence, Stackage was viewed by many
as "CI for Hackage." It detected build errors and version conflicts
quickly and reported them to authors. While very few people directly
used Stackage snapshots in those days, and no one used Stack (because
it didn't exist), the positive impacts of Stackage were felt by many,
directly or indirectly.

We would be undoing some part of that with this change. Authors would
feel no pressure from Stackage to keep their version bounds as relaxed
as possible. For authors not following the PVP, this would likely have
no negative impact. Somewhat ironically, for the case of an author who
follows the PVP, however, pressure from the Stackage side would no
longer exist to relax upper bounds. The Hackage build matrix would
still consider the build in the green (because it would be a "build
plan not found" situation), but ultimately dependency solver users
would find diminished successful plans.

On the other hand, Stackage would still do a good job of notifying
authors of actual build breakages, and in fact would notify them of
those brekages sooner rather than later.

## Tweak: respect lower bounds, ignore upper bounds

Adam Bergmark (another Stackage Curator), upon review, noted that lower bounds
are almost always known breakages, changing the trade-offs noted above. A
slight tweak to this proposal would be to ignore upper bounds, but respect any
lower bounds stated.
