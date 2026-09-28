# Musical Motion from Shared Partials

A directed chord relation from ordered harmonic and pseudo-partial coincidences

## What this article adds, and why it matters

A chord can share sound with the next chord while changing the harmonic roles
that supply it. This article makes that idea into a directed relation: consonant
partial pairs contribute backward, stationary or forward weight according to
the order of their partial labels.

A complete three-component construction turns root, fifth and major-third roles
into an exact twelve-tone transition table. For C major to F major, it gives
components **(63, 274, 360)** and normalized direction **297/697**. The derivation
shows where every contribution comes from and how timbre, octave folding,
aggregation and normalization change the result.

The relation reverses with chord order and can form directed cycles. An unchanged
chord can contain balanced forward and backward contributions. These properties
make it useful for examining what a single motion score reveals, and what the full
component structure retains.

Which ordered harmonic roles correspond to heard continuation? How does changing
timbre change the direction? Can these local relations guide a useful progression
without imposing a global ranking of chords? The article gives explicit
constructions and comparison pairs for investigating these questions.

The mathematical ideas come from the author's Kotlin sonance models. The article
explains them through definitions, proofs, diagrams and worked musical examples.
It contains no code listings; no perceptual experiment is reported.

## Article and build

[Read the article (PDF)](musical-motion.pdf) · [Manuscript source](musical-motion.md)

Install GNU Make, GNU Coreutils, Pandoc, XeLaTeX and the TeX Gyre fonts, including the LaTeX
packages used by `preamble.tex` and `preamble-local.tex` and the TikZ/PGFPlots standalone figures.
Run `make pdf` from this repository. It regenerates changed figures and builds
the article without any sibling repository or private working files.

The first page gives the PDF creation time in UTC, followed by the
[GitHub repository](https://github.com/hobnilre/music-motion). An up-to-date PDF keeps its timestamp;
`make -B pdf` forces a rebuild. Intermediates go to ignored `build/` by default;
`BUILD_DIR=/absolute/path` selects another location. `make clean` removes that
build directory and keeps the published PDF and figure assets.

Shared typography is installed locally in `article-style.yaml`, `preamble.tex`
and `figures/figure-style.tex`. Article-specific definitions are in
`preamble-local.tex`. These files are complete build inputs; no tools checkout
is required.
