# HTTP request object

Create HTTP requests

## Details

This R6 class doesn't do actual HTTP requests as does
[`HttpClient()`](https://docs.ropensci.org/crul/reference/HttpClient.md) -
it is for building requests to use for async HTTP requests in
[`AsyncVaried()`](https://docs.ropensci.org/crul/reference/AsyncVaried.md)

Note that you can access HTTP verbs after creating an `HttpRequest`
object, just as you can with `HttpClient`. See examples for usage.

Also note that when you call HTTP verbs on a `HttpRequest` object you
don't need to assign the new object to a variable as the new details
you've added are added to the object itself.

See
[`HttpClient()`](https://docs.ropensci.org/crul/reference/HttpClient.md)
for information on parameters.

## R6 classes

This is an R6 class from the package R6. Find out more about R6 at
<https://r6.r-lib.org/>. After creating an instance of an R6 class
(e.g., `x <- HttpClient$new(url = "https://hb.opencpu.org")`) you can
access values and methods on the object `x`.

## See also

[http-headers](https://docs.ropensci.org/crul/reference/http-headers.md),
[writing-options](https://docs.ropensci.org/crul/reference/writing-options.md)

Other async:
[`Async`](https://docs.ropensci.org/crul/reference/Async.md),
[`AsyncQueue`](https://docs.ropensci.org/crul/reference/AsyncQueue.md),
[`AsyncVaried`](https://docs.ropensci.org/crul/reference/AsyncVaried.md)

## Public fields

- `url`:

  (character) a url

- `opts`:

  (list) named list of curl options

- `proxies`:

  a [`proxy()`](https://docs.ropensci.org/crul/reference/proxies.md)
  object

- `auth`:

  an [`auth()`](https://docs.ropensci.org/crul/reference/auth.md) object

- `headers`:

  (list) named list of headers, see
  [http-headers](https://docs.ropensci.org/crul/reference/http-headers.md)

- `handle`:

  a [`handle()`](https://docs.ropensci.org/crul/reference/handle.md)

- `progress`:

  only supports `httr::progress()`, see
  [progress](https://docs.ropensci.org/crul/reference/progress.md)

- `payload`:

  resulting payload after request

## Methods

### Public methods

- [`HttpRequest$print()`](#method-HttpRequest-print)

- [`HttpRequest$new()`](#method-HttpRequest-new)

- [`HttpRequest$get()`](#method-HttpRequest-get)

- [`HttpRequest$post()`](#method-HttpRequest-post)

- [`HttpRequest$put()`](#method-HttpRequest-put)

- [`HttpRequest$patch()`](#method-HttpRequest-patch)

- [`HttpRequest$delete()`](#method-HttpRequest-delete)

- [`HttpRequest$head()`](#method-HttpRequest-head)

- [`HttpRequest$verb()`](#method-HttpRequest-verb)

- [`HttpRequest$retry()`](#method-HttpRequest-retry)

- [`HttpRequest$method()`](#method-HttpRequest-method)

- [`HttpRequest$clone()`](#method-HttpRequest-clone)

------------------------------------------------------------------------

### Method [`print()`](https://rdrr.io/r/base/print.html)

print method for `HttpRequest` objects

#### Usage

    HttpRequest$print(x, ...)

#### Arguments

- `x`:

  self

- `...`:

  ignored

------------------------------------------------------------------------

### Method [`new()`](https://rdrr.io/r/methods/new.html)

Create a new `HttpRequest` object

#### Usage

    HttpRequest$new(url, opts, proxies, auth, headers, handle, progress)

#### Arguments

- `url`:

  (character) A url. One of `url` or `handle` required.

- `opts`:

  any curl options

- `proxies`:

  a [`proxy()`](https://docs.ropensci.org/crul/reference/proxies.md)
  object

- `auth`:

  an [`auth()`](https://docs.ropensci.org/crul/reference/auth.md) object

- `headers`:

  named list of headers, see
  [http-headers](https://docs.ropensci.org/crul/reference/http-headers.md)

- `handle`:

  a [`handle()`](https://docs.ropensci.org/crul/reference/handle.md)

- `progress`:

  only supports `httr::progress()`, see
  [progress](https://docs.ropensci.org/crul/reference/progress.md)

- `urls`:

  (character) one or more URLs

#### Returns

A new `HttpRequest` object

------------------------------------------------------------------------

### Method [`get()`](https://rdrr.io/r/base/get.html)

Define a GET request

#### Usage

    HttpRequest$get(
      path = NULL,
      query = list(),
      disk = NULL,
      stream = NULL,
      mock = getOption("crul_mock", NULL),
      ...
    )

#### Arguments

- `path`:

  URL path, appended to the base URL

- `query`:

  query terms, as a named list

- `disk`:

  a path to write to. if NULL (default), memory used. See
  [`curl::curl_fetch_disk()`](https://jeroen.r-universe.dev/curl/reference/curl_fetch.html)
  for help.

- `stream`:

  an R function to determine how to stream data. if NULL (default),
  memory used. See
  [`curl::curl_fetch_stream()`](https://jeroen.r-universe.dev/curl/reference/curl_fetch.html)
  for help

- `mock`:

  A mocking function. If supplied, this function is called with the
  request. It should return either `NULL` (if it doesn't want to handle
  the request) or a
  [HttpResponse](https://docs.ropensci.org/crul/reference/HttpResponse.md)
  (if it does).

- `...`:

  curl options, only those in the acceptable set from
  [`curl::curl_options()`](https://jeroen.r-universe.dev/curl/reference/curl_options.html)
  except the following: httpget, httppost, post, postfields,
  postfieldsize, and customrequest

------------------------------------------------------------------------

### Method `post()`

Define a POST request

#### Usage

    HttpRequest$post(
      path = NULL,
      query = list(),
      body = NULL,
      disk = NULL,
      stream = NULL,
      encode = "multipart",
      mock = getOption("crul_mock", NULL),
      ...
    )

#### Arguments

- `path`:

  URL path, appended to the base URL

- `query`:

  query terms, as a named list

- `body`:

  body as an R list

- `disk`:

  a path to write to. if NULL (default), memory used. See
  [`curl::curl_fetch_disk()`](https://jeroen.r-universe.dev/curl/reference/curl_fetch.html)
  for help.

- `stream`:

  an R function to determine how to stream data. if NULL (default),
  memory used. See
  [`curl::curl_fetch_stream()`](https://jeroen.r-universe.dev/curl/reference/curl_fetch.html)
  for help

- `encode`:

  one of form, multipart, json, or raw

- `mock`:

  A mocking function. If supplied, this function is called with the
  request. It should return either `NULL` (if it doesn't want to handle
  the request) or a
  [HttpResponse](https://docs.ropensci.org/crul/reference/HttpResponse.md)
  (if it does).

- `...`:

  curl options, only those in the acceptable set from
  [`curl::curl_options()`](https://jeroen.r-universe.dev/curl/reference/curl_options.html)
  except the following: httpget, httppost, post, postfields,
  postfieldsize, and customrequest

------------------------------------------------------------------------

### Method `put()`

Define a PUT request

#### Usage

    HttpRequest$put(
      path = NULL,
      query = list(),
      body = NULL,
      disk = NULL,
      stream = NULL,
      encode = "multipart",
      mock = getOption("crul_mock", NULL),
      ...
    )

#### Arguments

- `path`:

  URL path, appended to the base URL

- `query`:

  query terms, as a named list

- `body`:

  body as an R list

- `disk`:

  a path to write to. if NULL (default), memory used. See
  [`curl::curl_fetch_disk()`](https://jeroen.r-universe.dev/curl/reference/curl_fetch.html)
  for help.

- `stream`:

  an R function to determine how to stream data. if NULL (default),
  memory used. See
  [`curl::curl_fetch_stream()`](https://jeroen.r-universe.dev/curl/reference/curl_fetch.html)
  for help

- `encode`:

  one of form, multipart, json, or raw

- `mock`:

  A mocking function. If supplied, this function is called with the
  request. It should return either `NULL` (if it doesn't want to handle
  the request) or a
  [HttpResponse](https://docs.ropensci.org/crul/reference/HttpResponse.md)
  (if it does).

- `...`:

  curl options, only those in the acceptable set from
  [`curl::curl_options()`](https://jeroen.r-universe.dev/curl/reference/curl_options.html)
  except the following: httpget, httppost, post, postfields,
  postfieldsize, and customrequest

------------------------------------------------------------------------

### Method `patch()`

Define a PATCH request

#### Usage

    HttpRequest$patch(
      path = NULL,
      query = list(),
      body = NULL,
      disk = NULL,
      stream = NULL,
      encode = "multipart",
      mock = getOption("crul_mock", NULL),
      ...
    )

#### Arguments

- `path`:

  URL path, appended to the base URL

- `query`:

  query terms, as a named list

- `body`:

  body as an R list

- `disk`:

  a path to write to. if NULL (default), memory used. See
  [`curl::curl_fetch_disk()`](https://jeroen.r-universe.dev/curl/reference/curl_fetch.html)
  for help.

- `stream`:

  an R function to determine how to stream data. if NULL (default),
  memory used. See
  [`curl::curl_fetch_stream()`](https://jeroen.r-universe.dev/curl/reference/curl_fetch.html)
  for help

- `encode`:

  one of form, multipart, json, or raw

- `mock`:

  A mocking function. If supplied, this function is called with the
  request. It should return either `NULL` (if it doesn't want to handle
  the request) or a
  [HttpResponse](https://docs.ropensci.org/crul/reference/HttpResponse.md)
  (if it does).

- `...`:

  curl options, only those in the acceptable set from
  [`curl::curl_options()`](https://jeroen.r-universe.dev/curl/reference/curl_options.html)
  except the following: httpget, httppost, post, postfields,
  postfieldsize, and customrequest

------------------------------------------------------------------------

### Method `delete()`

Define a DELETE request

#### Usage

    HttpRequest$delete(
      path = NULL,
      query = list(),
      body = NULL,
      disk = NULL,
      stream = NULL,
      encode = "multipart",
      mock = getOption("crul_mock", NULL),
      ...
    )

#### Arguments

- `path`:

  URL path, appended to the base URL

- `query`:

  query terms, as a named list

- `body`:

  body as an R list

- `disk`:

  a path to write to. if NULL (default), memory used. See
  [`curl::curl_fetch_disk()`](https://jeroen.r-universe.dev/curl/reference/curl_fetch.html)
  for help.

- `stream`:

  an R function to determine how to stream data. if NULL (default),
  memory used. See
  [`curl::curl_fetch_stream()`](https://jeroen.r-universe.dev/curl/reference/curl_fetch.html)
  for help

- `encode`:

  one of form, multipart, json, or raw

- `mock`:

  A mocking function. If supplied, this function is called with the
  request. It should return either `NULL` (if it doesn't want to handle
  the request) or a
  [HttpResponse](https://docs.ropensci.org/crul/reference/HttpResponse.md)
  (if it does).

- `...`:

  curl options, only those in the acceptable set from
  [`curl::curl_options()`](https://jeroen.r-universe.dev/curl/reference/curl_options.html)
  except the following: httpget, httppost, post, postfields,
  postfieldsize, and customrequest

------------------------------------------------------------------------

### Method [`head()`](https://rdrr.io/r/utils/head.html)

Define a HEAD request

#### Usage

    HttpRequest$head(path = NULL, mock = getOption("crul_mock", NULL), ...)

#### Arguments

- `path`:

  URL path, appended to the base URL

- `mock`:

  A mocking function. If supplied, this function is called with the
  request. It should return either `NULL` (if it doesn't want to handle
  the request) or a
  [HttpResponse](https://docs.ropensci.org/crul/reference/HttpResponse.md)
  (if it does).

- `...`:

  curl options, only those in the acceptable set from
  [`curl::curl_options()`](https://jeroen.r-universe.dev/curl/reference/curl_options.html)
  except the following: httpget, httppost, post, postfields,
  postfieldsize, and customrequest

------------------------------------------------------------------------

### Method `verb()`

Use an arbitrary HTTP verb supported on this class Supported verbs: get,
post, put, patch, delete, head

#### Usage

    HttpRequest$verb(verb, ...)

#### Arguments

- `verb`:

  an HTTP verb supported on this class: get, post, put, patch, delete,
  head. Also supports retry.

- `...`:

  curl options, only those in the acceptable set from
  [`curl::curl_options()`](https://jeroen.r-universe.dev/curl/reference/curl_options.html)
  except the following: httpget, httppost, post, postfields,
  postfieldsize, and customrequest

#### Examples

    z <- HttpRequest$new(url = "https://hb.opencpu.org/get")
    res <- z$verb('get', query = list(hello = "world"))
    res$payload

------------------------------------------------------------------------

### Method `retry()`

Define a RETRY request

#### Usage

    HttpRequest$retry(
      verb,
      ...,
      pause_base = 1,
      pause_cap = 60,
      pause_min = 1,
      times = 3,
      terminate_on = NULL,
      retry_only_on = NULL,
      onwait = NULL
    )

#### Arguments

- `verb`:

  an HTTP verb supported on this class: get, post, put, patch, delete,
  head. Also supports retry.

- `...`:

  curl options, only those in the acceptable set from
  [`curl::curl_options()`](https://jeroen.r-universe.dev/curl/reference/curl_options.html)
  except the following: httpget, httppost, post, postfields,
  postfieldsize, and customrequest

- `pause_base, pause_cap, pause_min`:

  basis, maximum, and minimum for calculating wait time for retry. Wait
  time is calculated according to the exponential backoff with full
  jitter algorithm. Specifically, wait time is chosen randomly between
  `pause_min` and the lesser of `pause_base * 2` and `pause_cap`, with
  `pause_base` doubling on each subsequent retry attempt. Use
  `pause_cap = Inf` to not terminate retrying due to cap of wait time
  reached.

- `times`:

  the maximum number of times to retry. Set to `Inf` to not stop
  retrying due to exhausting the number of attempts.

- `terminate_on, retry_only_on`:

  a vector of HTTP status codes. For `terminate_on`, the status codes
  for which to terminate retrying, and for `retry_only_on`, the status
  codes for which to retry the request.

- `onwait`:

  a callback function if the request will be retried and a wait time is
  being applied. The function will be passed two parameters, the
  response object from the failed request, and the wait time in seconds.
  Note that the time spent in the function effectively adds to the wait
  time, so it should be kept simple.

------------------------------------------------------------------------

### Method `method()`

Get the HTTP method (if defined)

#### Usage

    HttpRequest$method()

#### Returns

(character) the HTTP method

------------------------------------------------------------------------

### Method `clone()`

The objects of this class are cloneable with this method.

#### Usage

    HttpRequest$clone(deep = FALSE)

#### Arguments

- `deep`:

  Whether to make a deep clone.

## Examples

``` r
x <- HttpRequest$new(url = "https://hb.opencpu.org/get")
## note here how the HTTP method is shown on the first line to the right
x$get()
#> <crul http request> get
#>   url: https://hb.opencpu.org/get
#>   curl options: 
#>   proxies: 
#>   auth: 
#>   headers: 
#>   progress: FALSE
#>   mock: 

## assign to a new object to keep the output
z <- x$get()
### get the HTTP method
z$method()
#> [1] "get"

(x <- HttpRequest$new(url = "https://hb.opencpu.org/get")$get())
#> <crul http request> get
#>   url: https://hb.opencpu.org/get
#>   curl options: 
#>   proxies: 
#>   auth: 
#>   headers: 
#>   progress: FALSE
#>   mock: 
x$url
#> [1] "https://hb.opencpu.org/get"
x$payload
#> $url
#> $url$url
#> [1] "https://hb.opencpu.org/get"
#> 
#> $url$handle
#> <curl handle> (https://hb.opencpu.org/get)
#> 
#> 
#> $method
#> [1] "get"
#> 
#> $options
#> $options$httpget
#> [1] TRUE
#> 
#> 
#> $headers
#> $headers$`Accept-Encoding`
#> [1] "gzip, deflate"
#> 
#> $headers$Accept
#> [1] "application/json, text/xml, application/xml, */*"
#> 
#> 

(x <- HttpRequest$new(url = "https://hb.opencpu.org/post"))
#> <crul http request> 
#>   url: https://hb.opencpu.org/post
#>   curl options: 
#>   proxies: 
#>   auth: 
#>   headers: 
#>   progress: FALSE
#>   mock: 
x$post(body = list(foo = "bar"))
#> <crul http request> post
#>   url: https://hb.opencpu.org/post
#>   curl options: 
#>   proxies: 
#>   auth: 
#>   headers: 
#>   progress: FALSE
#>   mock: 

HttpRequest$new(
  url = "https://hb.opencpu.org/get",
  headers = list(
    `Content-Type` = "application/json"
  )
)
#> <crul http request> 
#>   url: https://hb.opencpu.org/get
#>   curl options: 
#>   proxies: 
#>   auth: 
#>   headers: 
#>     Content-Type: application/json
#>   progress: FALSE
#>   mock: 

# retry
(x <- HttpRequest$new(url = "https://hb.opencpu.org/post"))
#> <crul http request> 
#>   url: https://hb.opencpu.org/post
#>   curl options: 
#>   proxies: 
#>   auth: 
#>   headers: 
#>   progress: FALSE
#>   mock: 
x$retry("post", body = list(foo = "bar"))
#> <crul http request> post (retry)
#>   url: https://hb.opencpu.org/post
#>   curl options: 
#>   proxies: 
#>   auth: 
#>   headers: 
#>   progress: FALSE
#>   mock: 

# mock
x <- HttpRequest$new(url = "https://hb.opencpu.org/get")
fun <- function() {
  HttpResponse$new(method = "GET", url = "http://google.com",
    status_code = 200L)
}
x$get(mock = fun)
#> <crul http request> get
#>   url: https://hb.opencpu.org/get
#>   curl options: 
#>   proxies: 
#>   auth: 
#>   headers: 
#>   progress: FALSE
#>   mock: <function>

## ------------------------------------------------
## Method `HttpRequest$verb`
## ------------------------------------------------

z <- HttpRequest$new(url = "https://hb.opencpu.org/get")
res <- z$verb('get', query = list(hello = "world"))
res$payload
#> $url
#> $url$url
#> [1] "https://hb.opencpu.org/get?hello=world"
#> 
#> $url$handle
#> <curl handle> (https://hb.opencpu.org/get?hello=world)
#> 
#> 
#> $method
#> [1] "get"
#> 
#> $options
#> $options$httpget
#> [1] TRUE
#> 
#> 
#> $headers
#> $headers$`Accept-Encoding`
#> [1] "gzip, deflate"
#> 
#> $headers$Accept
#> [1] "application/json, text/xml, application/xml, */*"
#> 
#> 
```
