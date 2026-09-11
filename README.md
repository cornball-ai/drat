# drat

CRAN-style source repository for [cornball.ai](https://cornball.ai) R packages,
including packages not on CRAN and current versions of packages also on CRAN:

- `bonsaisitter` — tree-sitter runtime for R, zero hard dependencies
- `treesitter.python`, `treesitter.cpp`, `treesitter.rust`,
  `treesitter.javascript`, `treesitter.go` — grammar packages for the runtime
- `mirar` — structured runtime inspection of R sessions
- `chat.api` — transport-agnostic chat contract for R agents, with
  adapters for Matrix, Slack, and IRC
- `janssonr` — strict JSON encode/decode via the Jansson C library
  (links system `libjansson-dev` >= 2.11 when present, compiles its
  bundled copy otherwise; needs R >= 4.4)
- `hacer`, `RcppOTIO`

The Matrix packages are also carried here:

- `mx.api`: Matrix client-server API bindings
- `mx.crypto`: Matrix end-to-end encryption primitives
- `mx.client`: stateful Matrix client helpers

Keep each carried package aligned with the `Version:` on its `main` branch.
Retain releases here after CRAN publication. Preserve older archives and
index only the latest version of each package.

The exact versions live in `src/contrib/PACKAGES` rather than in this
list, which only says why a package is here.

## Usage

```r
install.packages("bonsaisitter",
                 repos = c("https://cornball-ai.github.io/drat",
                           getOption("repos")))
```

For source packages, R selects the highest available version across the
repositories. Repository order breaks ties when versions are equal.

Source packages only. `RcppOTIO` needs the OpenTimelineIO C++ library (>= 0.18),
Imath headers, and a C++17 compiler -- see its `SystemRequirements`.

## Adding a release

```r
file.copy("pkg_x.y.z.tar.gz", "~/drat/src/contrib/")
tools::write_PACKAGES("~/drat/src/contrib", type = "source", latestOnly = TRUE)
```

Verify the archive matches the package's `main` version and tested source.
Publish new archives first and verify their bytes on GitHub Pages. Then
commit and publish the regenerated indexes, and verify the public index
and archive checksums. Keep older tarballs in place.
