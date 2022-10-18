renv-git-submodules
================

With renv 0.16.0, [hadley/emo](https://github.com/hadley/emo) is
installed as `"Source": "git"` because it uses submodules. (However, the
submodules are used in `data-raw/` so they aren’t needed for correct
package installation.)

``` r
getOption("repos")
```

    ##                       CRAN 
    ## "https://cran.rstudio.com"

``` r
str(renv:::renv_json_read("renv.lock")$Packages$emo)
```

    ## List of 12
    ##  $ Package       : chr "emo"
    ##  $ Version       : chr "0.0.0.9000"
    ##  $ Source        : chr "git"
    ##  $ RemoteType    : chr "git"
    ##  $ RemoteUrl     : chr "https://github.com/hadley/emo"
    ##  $ RemoteHost    : chr "api.github.com"
    ##  $ RemoteUsername: chr "hadley"
    ##  $ RemoteRepo    : chr "emo"
    ##  $ RemoteRef     : chr "3f03b11491ce3d6fc5601e210927eff73bf8e350"
    ##  $ RemoteSha     : chr "3f03b11491ce3d6fc5601e210927eff73bf8e350"
    ##  $ Hash          : chr "38cd5a58901f1ba87ca769667d557a76"
    ##  $ Requirements  :List of 8
    ##   ..$ : chr "assertthat"
    ##   ..$ : chr "crayon"
    ##   ..$ : chr "glue"
    ##   ..$ : chr "lubridate"
    ##   ..$ : chr "magrittr"
    ##   ..$ : chr "purrr"
    ##   ..$ : chr "rlang"
    ##   ..$ : chr "stringr"

The problem that arises is that I can’t deploy content that uses emo
installed with renv 0.16.0 to Connect because
`rsconnect::writeManifest()` can’t determine the repository URL.

``` r
rsconnect::writeManifest(appPrimaryDoc = "example.Rmd")
```

    ## Warning in FUN(X[[i]], ...): Package 'emo 0.0.0.9000' was installed from
    ## sources; Packrat will assume this package is available from a CRAN-like
    ## repository during future restores

    ## Warning: 
    ## * May be unable to deploy package dependency 'emo'; could not determine
    ##   a repository URL for the source 'CRAN'.
    ## 
    ## * Unable to determine the source location for some packages. Packages
    ##   should be installed from a package repository like CRAN or a version
    ##   control system. Check that options('repos') refers to a package
    ##   repository containing the needed package versions.
