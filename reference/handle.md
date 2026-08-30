# Make a handle

Make a handle

## Usage

``` r
handle(url, ...)
```

## Arguments

- url:

  (character) A url. required.

- ...:

  options passed on to
  [`curl::new_handle()`](https://jeroen.r-universe.dev/curl/reference/handle.html)

## Examples

``` r
handle("https://hb.opencpu.org")
#> $url
#> [1] "https://hb.opencpu.org"
#> 
#> $handle
#> <curl handle> (empty)
#> 

# handles - pass in your own handle
if (FALSE) { # \dontrun{
h <- handle("https://hb.opencpu.org")
(res <- HttpClient$new(handle = h))
out <- res$get("get")
} # }
```
