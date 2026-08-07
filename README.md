# drat

CRAN-style package repository for [cornball.ai](https://cornball.ai) R packages
that aren't on CRAN (yet):

- `bonsaisitter` — tree-sitter runtime for R, zero hard dependencies
- `treesitter.python`, `treesitter.cpp`, `treesitter.rust`,
  `treesitter.javascript`, `treesitter.go` — grammar packages for the runtime
- `mirar` — structured runtime inspection of R sessions
- `chat.api` — transport-agnostic chat contract for R agents, with
  adapters for Matrix, Slack, and IRC
- `hacer`, `RcppOTIO`

It also carries development versions of packages that *are* on CRAN, when
something here needs a fix that has not been released yet:

- `mx.client` — CRAN has 0.2.0, which predates the encrypted-send fixes
  and the reaction and invite extractors that `chat.api` reads. Both
  `chat.api` and `corteza` declare floors above it, so the version here
  is whatever they currently need. Drops back to the CRAN copy once
  those changes ship as 0.2.1.

The exact versions live in `src/contrib/PACKAGES` rather than in this
list, which only says why a package is here.

## Usage

```r
install.packages("bonsaisitter",
                 repos = c("https://cornball-ai.github.io/drat",
                           getOption("repos")))
```

Listing this repo first is what makes the development versions win: R picks
the highest version it can see across the repositories given, so a package
here at 0.2.0.2 supersedes CRAN's 0.2.0 and one that only exists here is
found at all.

Source packages only. `RcppOTIO` needs the OpenTimelineIO C++ library (>= 0.18),
Imath headers, and a C++17 compiler -- see its `SystemRequirements`.

## Adding a release

```r
file.copy("pkg_x.y.z.tar.gz", "~/drat/src/contrib/")
tools::write_PACKAGES("~/drat/src/contrib", type = "source")
```

Then commit and push.
