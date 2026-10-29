# Set curl options, proxy, and basic auth

Set curl options, proxy, and basic auth

## Usage

``` r
set_opts(...)

set_verbose()

set_proxy(x)

set_auth(x)

set_headers(...)

crul_settings(reset = FALSE)
```

## Arguments

- ...:

  For `set_opts()` any curl option in the set
  [`curl::curl_options()`](https://jeroen.r-universe.dev/curl/reference/curl_options.html).
  For `set_headers()` a named list of headers

- x:

  For `set_proxy()` a `proxy` object made with
  [`proxy()`](https://docs.ropensci.org/crul/reference/proxies.md). For
  `set_auth()` an `auth` object made with
  [`auth()`](https://docs.ropensci.org/crul/reference/auth.md)

- reset:

  (logical) reset all settings (aka, delete them). Default: `FALSE`

## Details

- `set_opts()`: set curl options; supports any options in
  [`curl::curl_options()`](https://jeroen.r-universe.dev/curl/reference/curl_options.html)

- `set_verbose()`: set custom curl verbose; sets `verbose=TRUE` and
  `debugfunction` to the callback result from
  [`curl_verbose()`](https://docs.ropensci.org/crul/reference/curl_verbose.md)

- `set_proxy()`: set proxy settings, accepts
  [`proxy()`](https://docs.ropensci.org/crul/reference/proxies.md)

- `set_auth()`: set authorization, accepts
  [`auth()`](https://docs.ropensci.org/crul/reference/auth.md)

- `set_headers()`: set request headers, a named list

- `crul_settings()`: list all settigns set via these functions

## Note

the `mock` option will be seen in output of `crul_settings()` but is set
via the function
[`mock()`](https://docs.ropensci.org/crul/reference/mock.md)

## Examples

``` r
if (interactive()) {
# get settings
crul_settings()

# curl options
set_opts(timeout_ms = 1000)
crul_settings()
set_opts(timeout_ms = 4000)
crul_settings()
set_opts(verbose = TRUE)
crul_settings()
if (FALSE) { # \dontrun{
HttpClient$new('https://hb.opencpu.org')$get('get')
} # }
# set_verbose - sets: `verbose=TRUE`, and `debugfunction` to
# result of call to `curl_verbose()`, see `?curl_verbose`
set_verbose()
crul_settings()

# basic authentication
set_auth(auth(user = "foo", pwd = "bar", auth = "basic"))
crul_settings()

# proxies
set_proxy(proxy("http://97.77.104.22:3128"))
crul_settings()

# headers
crul_settings(TRUE) # reset first
set_headers(foo = "bar")
crul_settings()
set_headers(`User-Agent` = "hello world")
crul_settings()
if (FALSE) { # \dontrun{
set_opts(verbose = TRUE)
HttpClient$new('https://hb.opencpu.org')$get('get')
} # }

# reset
crul_settings(TRUE)
crul_settings()

# works with async functions
## Async
set_opts(verbose = TRUE)
cc <- Async$new(urls = c(
    'https://hb.opencpu.org/get?a=5',
    'https://hb.opencpu.org/get?foo=bar'))
(res <- cc$get())

## AsyncVaried
set_opts(verbose = TRUE)
set_headers(stuff = "things")
reqlist <- list(
  HttpRequest$new(url = "https://hb.opencpu.org/get")$get(),
  HttpRequest$new(url = "https://hb.opencpu.org/post")$post())
out <- AsyncVaried$new(.list = reqlist)
out$request()
}
```
