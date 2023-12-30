![Platforms](https://img.shields.io/badge/platform-linux%20%7C%20osx%20%7C%20windows-informational)
![GitHub repo size](https://img.shields.io/github/repo-size/reanimate/reanimate)
[![Haskell CI](https://github.com/ruifengx/reanimate/actions/workflows/haskell.yml/badge.svg)](https://github.com/ruifengx/reanimate/actions/workflows/haskell.yml)

# Reanimate

Reanimate is a library for programmatically generating animations with a twist towards
mathematics / 2D vector drawings. A lot of inspiration was drawn from 3b1b's manim library.

Reanimate aims at being a batteries-included way of gluing together different technologies: SVG as
a universal image format, LaTeX for typesetting, ffmpeg for video encoding, inkscape/imagemagick
for rasterization, potrace for vectorization, blender/povray for 3D graphics, and Haskell for
scripting.

In more practical terms, reanimate is a library for turning code like this:

```haskell
main = reanimate $ docEnv $ playThenReverseA drawCircle
```

... into animations like this:

[![Draw Circle](https://i.imgur.com/C02hPw8.gif)](examples/doc_playThenReverseA.hs)

If you like what you see, boost reanimate's visibility with a star ⭐ or consider becoming a [sponsor ❤](https://github.com/sponsors/Lemmih).

# What is reanimate good at?

## Vector graphics and math
[![Tangent/Normal](https://i.imgur.com/w6gEkbl.gif)](examples/demo_tangent.hs)
[![Fourier](https://i.imgur.com/pX4YRa4.gif)](examples/tut_glue_fourier.hs)

## Mapping and tracing
[![Geo JSON](https://i.imgur.com/OrKiOqF.gif)](videos/map-projection/gif.hs)
[![Object tracing](https://i.imgur.com/Y6NsPWF.gif)](examples/tut_glue_potrace.hs)

## Mathematical typesetting and effects
[![LaTeX](https://i.imgur.com/e6oO4wz.gif)](examples/tut_glue_latex.hs)
[![Stars](https://i.imgur.com/yek3v4b.gif)](examples/demo_stars.hs)

## 2D physics and 3D graphics
[![2D Physics](https://i.imgur.com/ZHUfWdp.gif)](examples/tut_glue_physics.hs)
[![3D graphics](https://i.imgur.com/4wdtuJw.gif)](examples/tut_glue_povray.hs)

# Prerequisites

Reanimate is built using the Haskell Tool Stack. For installation instructions, see: https://docs.haskellstack.org/en/stable/README/

Optionally, you can install one or more of these programs to enable additional features:
 * [ffmpeg](https://www.ffmpeg.org/), enables rendering animations to video files.
 * [latex](https://www.latex-project.org/), enables mathematical typesetting.
 * [inkscape](https://inkscape.org/)/[imagemagick](https://imagemagick.org/index.php), enables SVG->PNG convertions.
 * [potrace](http://potrace.sourceforge.net/), enables PNG->SVG tracing.
 * [povray](https://www.povray.org/), enables raytracing.
 * [blender](https://www.blender.org/), enables 3D graphics.

I highly recommend that you install at least 'ffmpeg' and 'latex'.

# Getting started / Running an example

Reanimate offers stack templates for getting started with a minimal example and
automatic code reloading. Running the commands below will put a one-line animation
in the 'animate' folder and then display the animation in a browser window. You can
then edit the animation source code and watch the animation update in real time:

```console
$ stack new animate github:reanimate/plain
$ cd animate/
$ # both 'cabal repl' and 'stack repl' can be used here:
$ cabal repl
:cmd reanimateLive
```

## Running examples from the repository

Reanimate has a large collection of small examples which are both used for regression testing
and for GIFs in the API reference documentation. You can run these examples by first cloning the
repository and then running the examples as if they were executables:

```console
$ git clone https://github.com/reanimate/reanimate.git
$ cd reanimate/
$ stack build
$ stack ./examples/doc_drawCircle.hs
```

This should render the `doc_drawCircle` example in a new browser window. Automatic code reloading
will not be enabled unless you run `:cmd reanimateLive` from a GHCi session.


## Running examples from the repository using Cabal

It's also possible to use cabal instead of stack:

```console
$ git clone https://github.com/reanimate/reanimate.git
$ cd reanimate/
$ cabal v2-build
$ # Workaround for a cabal bug: https://github.com/haskell/cabal/issues/6235
$ export reanimate_datadir=`pwd`
$ cabal v2-exec -- runhaskell examples/doc_drawCircle.hs
```

## Using Nix

If you'd rather use nix to build an environment with all of the system dependencies mentioned previously do:

```console
$ git clone https://github.com/reanimate/reanimate.git
$ cd reanimate/
$ nix-shell
[nix-shell:./reanimate]$ cabal v2-build --write-ghc-environment-files=always
```

If you have cachix available run `cachix use cdodev` before you drop into the nix shell. This will significantly speed things up!

This will write a file in the working directory like
`.ghc.environment.x86_64-linux-8.8.3` which will enable commands like `runhaskell`
to pick up reanimate.

Now, still within the `nix-shell` you can run:

```console
[nix-shell:./reanimate]$ reanimate_datadir=. runhaskell examples/doc_drawCircle.hs
```


# Documentation

 * API reference: https://hackage.haskell.org/package/reanimate/docs/Reanimate.html
 * Core concepts: https://reanimate.readthedocs.io/en/latest/introduction.html
 * Design overview: https://reanimate.readthedocs.io/en/latest/glue_tut.html
 * N-Queens tutorial (somewhat dated, uses reanimate from October 2019): https://williamyaoh.com/posts/2020-05-31-reanimate-nqueens-tutorial.html
 * You can also ask questions in the discord channel: <https://discord.gg/Qs28Dv6>

# Features

- [x] Cross-platform. Official support for Linux, MacOS, and Windows.
- [x] Well-documented. API [reference documentation](https://hackage.haskell.org/package/reanimate/docs/Reanimate.html) include GIFs to illustrate behavior, and in-depth tutorial/explanation articles are hosted on [readthedocs.io](https://reanimate.readthedocs.io/en/latest/).
- [x] Advanced type-setting via LaTeX.
- [x] Voice control: Align animation timings with a transcript.
- [x] 3D graphics: Built-in support for integrating povray and blender.
- [x] Mapping: Built-in support for GeoJSON and map projections.
- [x] Online playground for toying with reanimate scripts.

# Roadmap

- Easy-to-use font selection when using latex/xelatex/luatex.
- Polygon morphing framework with support for several algorithms, including: linear interpolation, as-rigid-as-possible interpolation, and intersection-free interpolation.
- Built-in tools for creating presentations.

# Authors

  * David Himmelstrup.
  * Jan Hrcek.

# License

This is free and unencumbered software released into the public domain.

Anyone is free to copy, modify, publish, use, compile, sell, or
distribute this software, either in source code form or as a compiled
binary, for any purpose, commercial or non-commercial, and by any
means.

# Acknowledgments

  * Huge thanks to 3b1b's [manim](https://github.com/3b1b/manim) which inspired this library.
  * Thanks to [svg-tree](https://github.com/Twinside/svg-tree) for their SVG library.
  * Thanks to [CthulhuDen/chiphunk](https://github.com/CthulhuDen/chiphunk) for making a 2D physics
    library easily available.
  * Thanks to [Peter Johnson](https://github.com/missinglink) for reserving the 'reanimate' organization on GitHub.

# YouTube

Completed animations are uploaded to the [Reanimated Science](https://www.youtube.com/channel/UCbZujyI7i6JbI-I0shPvDgg) channel.

Animation snippets are uploaded to the [Reanimated Science Shorts](https://www.youtube.com/channel/UCL7MwXLtQbhJeb6Ts3_HooA) channel.
