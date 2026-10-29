# AsyncQueue

An AsyncQueue client

## R6 classes

This is an R6 class from the package R6. Find out more about R6 at
<https://r6.r-lib.org/>. After creating an instance of an R6 class
(e.g., `x <- HttpClient$new(url = "https://hb.opencpu.org")`) you can
access values and methods on the object `x`.

## See also

Other async:
[`Async`](https://docs.ropensci.org/crul/reference/Async.md),
[`AsyncVaried`](https://docs.ropensci.org/crul/reference/AsyncVaried.md),
[`HttpRequest`](https://docs.ropensci.org/crul/reference/HttpRequest.md)

## Super class

[`crul::AsyncVaried`](https://docs.ropensci.org/crul/reference/AsyncVaried.md)
-\> `AsyncQueue`

## Public fields

- `bucket_size`:

  (integer) number of requests to send at once

- `sleep`:

  (integer) number of seconds to sleep between each bucket

- `req_per_min`:

  (integer) requests per minute

## Methods

### Public methods

- [`AsyncQueue$print()`](#method-AsyncQueue-print)

- [`AsyncQueue$new()`](#method-AsyncQueue-new)

- [`AsyncQueue$request()`](#method-AsyncQueue-request)

- [`AsyncQueue$responses()`](#method-AsyncQueue-responses)

- [`AsyncQueue$parse()`](#method-AsyncQueue-parse)

- [`AsyncQueue$status_code()`](#method-AsyncQueue-status_code)

- [`AsyncQueue$status()`](#method-AsyncQueue-status)

- [`AsyncQueue$content()`](#method-AsyncQueue-content)

- [`AsyncQueue$times()`](#method-AsyncQueue-times)

- [`AsyncQueue$clone()`](#method-AsyncQueue-clone)

Inherited methods

- [`crul::AsyncVaried$requests()`](https://docs.ropensci.org/crul/reference/AsyncVaried.html#method-requests)

------------------------------------------------------------------------

### Method [`print()`](https://rdrr.io/r/base/print.html)

print method for AsyncQueue objects

#### Usage

    AsyncQueue$print(x, ...)

#### Arguments

- `x`:

  self

- `...`:

  ignored

------------------------------------------------------------------------

### Method `new()`

Create a new `AsyncQueue` object

#### Usage

    AsyncQueue$new(
      ...,
      .list = list(),
      bucket_size = 5,
      sleep = NULL,
      req_per_min = NULL
    )

#### Arguments

- `..., .list`:

  Any number of objects of class
  [`HttpRequest()`](https://docs.ropensci.org/crul/reference/HttpRequest.md),
  must supply inputs to one of these parameters, but not both

- `bucket_size`:

  (integer) number of requests to send at once. default: 5. See Details.

- `sleep`:

  (integer) seconds to sleep between buckets. default: NULL (not set)

- `req_per_min`:

  (integer) maximum number of requests per minute. if `NULL` (default),
  its ignored

#### Details

Must set either `sleep` or `req_per_min`. If you set `req_per_min` we
calculate a new `bucket_size` when `$new()` is called

#### Returns

A new `AsyncQueue` object

------------------------------------------------------------------------

### Method `request()`

Execute asynchronous requests

#### Usage

    AsyncQueue$request()

#### Returns

nothing, responses stored inside object, though will print messages if
you choose verbose output

------------------------------------------------------------------------

### Method `responses()`

List responses

#### Usage

    AsyncQueue$responses()

#### Returns

a list of `HttpResponse` objects, empty list before requests made

------------------------------------------------------------------------

### Method [`parse()`](https://rdrr.io/r/base/parse.html)

parse content

#### Usage

    AsyncQueue$parse(encoding = "UTF-8")

#### Arguments

- `encoding`:

  (character) the encoding to use in parsing. default:"UTF-8"

#### Returns

character vector, empty character vector before requests made

------------------------------------------------------------------------

### Method `status_code()`

Get HTTP status codes for each response

#### Usage

    AsyncQueue$status_code()

#### Returns

numeric vector, empty numeric vector before requests made

------------------------------------------------------------------------

### Method `status()`

List HTTP status objects

#### Usage

    AsyncQueue$status()

#### Returns

a list of `http_code` objects, empty list before requests made

------------------------------------------------------------------------

### Method `content()`

Get raw content for each response

#### Usage

    AsyncQueue$content()

#### Returns

raw list, empty list before requests made

------------------------------------------------------------------------

### Method `times()`

curl request times

#### Usage

    AsyncQueue$times()

#### Returns

list of named numeric vectors, empty list before requests made

------------------------------------------------------------------------

### Method `clone()`

The objects of this class are cloneable with this method.

#### Usage

    AsyncQueue$clone(deep = FALSE)

#### Arguments

- `deep`:

  Whether to make a deep clone.

## Examples

``` r
if (FALSE) { # \dontrun{
# Using sleep (note this works with retry requests)
reqlist <- list(
  HttpRequest$new(url = "https://hb.opencpu.org/get")$get(),
  HttpRequest$new(url = "https://hb.opencpu.org/post")$post(),
  HttpRequest$new(url = "https://hb.opencpu.org/put")$put(),
  HttpRequest$new(url = "https://hb.opencpu.org/delete")$delete(),
  HttpRequest$new(url = "https://hb.opencpu.org/get?g=5")$get(),
  HttpRequest$new(
    url = "https://hb.opencpu.org/post")$post(body = list(y = 9)),
  HttpRequest$new(
    url = "https://hb.opencpu.org/get")$get(query = list(hello = "world")),
  HttpRequest$new(url = "https://ropensci.org")$get(),
  HttpRequest$new(url = "https://ropensci.org/about")$get(),
  HttpRequest$new(url = "https://ropensci.org/packages")$get(),
  HttpRequest$new(url = "https://ropensci.org/community")$get(),
  HttpRequest$new(url = "https://ropensci.org/blog")$get(),
  HttpRequest$new(url = "https://ropensci.org/careers")$get(),
  HttpRequest$new(url = "https://hb.opencpu.org/status/404")$retry("get")
)
out <- AsyncQueue$new(.list = reqlist, bucket_size = 5, sleep = 3)
out
out$bucket_size # bucket size
out$requests() # list requests
out$request() # make requests
out$responses() # list responses

# Using requests per minute
if (interactive()) {
x="https://raw.githubusercontent.com/ropensci/roregistry/gh-pages/registry.json"
z <- HttpClient$new(x)$get()
urls <- jsonlite::fromJSON(z$parse("UTF-8"))$packages$url
repos = Filter(length, regmatches(urls, gregexpr("ropensci/[A-Za-z]+", urls)))
repos = unlist(repos)
auth <- list(Authorization = paste("token", Sys.getenv('GITHUB_PAT')))
reqs <- lapply(repos[1:50], function(w) {
  HttpRequest$new(paste0("https://api.github.com/repos/", w), headers = auth)$get()
})

out <- AsyncQueue$new(.list = reqs, req_per_min = 30)
out
out$bucket_size
out$requests()
out$request()
out$responses()
}} # }
```
