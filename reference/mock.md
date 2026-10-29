# Mocking HTTP requests

**\[deprecated\]**

Mocking is now controlled by params within the various clients:
[`HttpClient()`](https://docs.ropensci.org/crul/reference/HttpClient.md),
[`Async()`](https://docs.ropensci.org/crul/reference/Async.md) and
[`AsyncVaried()`](https://docs.ropensci.org/crul/reference/AsyncVaried.md)

## Usage

``` r
mock(on = TRUE)
```

## Arguments

- on:

  (logical) turn mocking on with `TRUE` or turn off with `FALSE`. By
  default is `FALSE`
