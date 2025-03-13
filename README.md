## Run this repository in a web browser using Binder. Push the button \>\> [![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/e-kotov/demographic-research.44-19-containerized/HEAD?urlpath=rstudio)


# Brief log of how this repo was created

```bash
docker run --platform linux/amd64 -it --rm -v "$(pwd):/home/rstudio" -p 8787:8787 rocker/geospatial:4.2.2
```

```r
install.packages("renv", repos = "https://p3m.dev/cran/__linux__/jammy/latest")
```

```r
renv::init(force=TRUE)
```

Restart R

```r
renv::settings$ppm.enabled(value = TRUE)
renv::settings$snapshot.type(value = "all")
options("renv.config.pak.enabled" = TRUE)
```

Also add `options("renv.config.pak.enabled" = TRUE)` to `.Rprofile`.

```r
install.packages("pak", repos = "https://p3m.dev/cran/__linux__/jammy/latest")
```

```r
renv::status()
```

Many packages will still be missing, install them manually as you go through the R scripts.
Easiest way to install them is to open the source files and let RStudio show the button with missing dependencies and click install. The background job will use renv and pak.
Some packages will be missing even after that, so install them manually.

```r
renv::snapshot()
```

```r
install.packages(c("cpp11", "progress", "RcppArmadillo"))
```


```r
renv::snapshot()
```

```r
renv::status()
```

Stop the docker container.

Create the Dockerfile in Dockerfile4build.

```bash
docker build --platform linux/amd64 -f Dockerfile4build/Dockerfile -t r422 .
```

```bash
docker tag r422 ghcr.io/e-kotov/demographic-research.44-19-containerized:latest
```

```bash
docker push ghcr.io/e-kotov/demographic-research.44-19-containerized:latest
```

Create a `Dockerfile` file for Binder in the root of the project
