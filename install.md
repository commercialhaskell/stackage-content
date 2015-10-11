<div class="container content">
<div class="row">
<div class="span12">

# Install stack

The recommended method for getting up and running is to [install
stack](https://github.com/commercialhaskell/stack/blob/master/doc/install_and_upgrade.md). You can find
out more information about stack on [the stack
homepage](https://github.com/commercialhaskell/stack#readme). As a quick
overview: stack is a full-featured Haskell build tool that will install
necessary build tools (like the Glasgow Haskell Compiler- GHC), and is
preloaded with support for Stackage snapshots- both LTS Haskell and Stackage
Nightly.

[Return to Stackage homepage](/)

* * *

# Alternatively, manually install Haskell tools

We've kept these installation instructions in case they are useful but note that
they are __no longer recommended__.

This is a general purpose guide for installing a Haskell toolchain.
The Haskell toolchain consists of:

1. The GHC compiler (version 7.8.4)
2. The cabal-install build tool (version 1.18 or 1.20 recommended)
3. On Windows, MSYS, needed for building some common packages

If you already have the above tools installed, you can [start using Stackage
now](/). Otherwise, please choose the appropriate OS below.

* [Ubuntu](#ubuntu)
* [Arch](#arch)
* [Mac OS X](#mac-os-x)
* [Other \*nix](#other-nix)
* [Windows](#windows)

[Why not Haskell Platform?](#why-not-haskell-platform)

These instructions were inspired by [Chris Allen's installation
instructions](https://github.com/bitemyapp/learnhaskell/blob/master/README.md).

## OS-specific instructions

### Ubuntu

Use [Hebert's PPA](http://launchpad.net/~hvr/+archive/ghc) to install GHC and
cabal-install, add appropriate directories to your PATH, and build some
commonly needed tools.

```
sudo apt-get update
sudo apt-get install -y software-properties-common
sudo add-apt-repository -y ppa:hvr/ghc
sudo apt-get update
sudo apt-get install -y cabal-install-1.20 ghc-7.8.4
cat >> ~/.bashrc <<EOF
export PATH=~/.cabal/bin:/opt/cabal/1.20/bin:/opt/ghc/7.8.4/bin:$PATH
EOF
export PATH=~/.cabal/bin:/opt/cabal/1.20/bin:/opt/ghc/7.8.4/bin:$PATH
cabal update
cabal install alex happy
```

Tweak the above as necessary depending on your choice in shell.

[Return to Stackage homepage](/)

### Arch

`su -c "pacman -S cabal-install ghc happy alex haddock"`

[Return to Stackage homepage](/)

### Mac OS X

For 10.9, please use [GHC for Mac OS X](http://ghcformacosx.github.io/). For
others, follow the [Other \*nix instructions](#other-nix).

[Return to Stackage homepage](/)

### Other \*nix

If you're on a different flavor of Linux, FreeBSD, or an older Mac OS X, the
installation process is essentially the same:

* [Download GHC](https://www.haskell.org/ghc/download_ghc_7_8_4#binaries)

*   Unpack the GHC tarball, and run

        ./configure --prefix=/some/prefix
        make install

* Add `/some/prefix/bin` and `$HOME/.cabal/bin` to your `PATH`
* [Download cabal-install](http://hackage.haskell.org/package/cabal-install-1.20.0.3/cabal-install-1.20.0.3.tar.gz)
* Unpack the tarball and run `sh bootstrap.sh` inside the new directory
* Run `cabal update && cabal install alex happy`

[Return to Stackage homepage](/)

### Windows

Run the [MinGHC
installer](https://s3.amazonaws.com/download.fpcomplete.com/minghc/minghc-7.8.3.exe)
([more information](https://github.com/snoyberg/minghc#readme)). After
installation, open a command prompt and run `cabal update` and `cabal install
alex happy`.

[Return to Stackage homepage](/)

## Why not Haskell Platform?

We do not currently recommend using the Haskell Platform installer due to some
limitations:

* On Windows, it does not provide a complete environment (missing MSYS).
* By placing a large number of packages in the global package database, Haskell Platform installations are more easily corrupted.
* The choice of package versions conflicts with the needs of many commonly used packages.
* Some of the package versions included with the platform have known and severe bugs, and cannot be reliably upgraded.

We hope these limitations are overcome in the future, but for now they make it
impractical to use.

[Return to Stackage homepage](/)

</div>
</div>
</div>
