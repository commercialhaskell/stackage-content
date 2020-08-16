---
author: Alexey Zabelin
title: Switching nightlies to GHC 8.10.2 and a workaround for Windows
description: GHC 8.10.2 is currently broken on Windows, here's a workaround you can use until 8.10.3 is out
timestamp: 2020-08-15T12:01:00Z
---

The nightly builds are now using GHC 8.10.2 which is 
[known to be broken on Windows](https://gitlab.haskell.org/ghc/ghc/-/issues/18550). 
This bug [should be fixed](https://gitlab.haskell.org/ghc/ghc/-/issues/18550#note_293049) in GHC 8.10.3.

To help alleviate some of the problems related to this we wanted to mention a
workaround you can use until GHC 8.10.3 comes out.

```
Javier Neira @jneira · 5 days ago

A direct workaround would be to change in X:\path\to\ghc-8.10.2\lib\settings:

("Merge objects command", " C:/GitLabRunner/builds/2WeHDSFP/0/ghc/ghc/inplace/mingw/bin/ld.exe")

with

("Merge objects command", "X:/path/to/ghc-8.10.2/mingw/bin/ld.exe")
```

[source](https://gitlab.haskell.org/ghc/ghc/-/issues/18550#note_293297)

Thanks to @mpilgrem for linking the workaround and suggesting we write this blog post!
