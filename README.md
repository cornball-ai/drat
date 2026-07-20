# drat

CRAN-style package repository for [cornball.ai](https://cornball.ai) R packages
that aren't on CRAN (yet):

- `bonsaisitter` — tree-sitter runtime for R, zero hard dependencies
- `treesitter.python`, `treesitter.cpp`, `treesitter.rust`,
  `treesitter.javascript` — grammar packages for the runtime
- `mirar` — structured runtime inspection of R sessions
- `hacer`, `RcppOTIO`

## Usage

```r
install.packages("bonsaisitter",
                 repos = c("https://cornball-ai.github.io/drat",
                           getOption("repos")))
```

Source packages only. `RcppOTIO` needs the OpenTimelineIO C++ library (>= 0.18),
Imath headers, and a C++17 compiler -- see its `SystemRequirements`.

## Adding a release

```r
file.copy("pkg_x.y.z.tar.gz", "~/drat/src/contrib/")
tools::write_PACKAGES("~/drat/src/contrib", type = "source")
```

Then commit and push.
