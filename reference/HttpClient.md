# HTTP client

Create and execute HTTP requests

## Value

an
[HttpResponse](https://docs.ropensci.org/crul/reference/HttpResponse.md)
object

## Note

A little quirk about `crul` is that because user agent string can be
passed as either a header or a curl option (both lead to a `User-Agent`
header being passed in the HTTP request), we return the user agent
string in the `request_headers` list of the response even if you pass in
a `useragent` string as a curl option. Note that whether you pass in as
a header like `User-Agent` or as a curl option like `useragent`, it is
returned as `request_headers$User-Agent` so at least accessing it in the
request headers is consistent.

## R6 classes

This is an R6 class from the package R6. Find out more about R6 at
<https://r6.r-lib.org/>. After creating an instance of an R6 class
(e.g., `x <- HttpClient$new(url = "https://hb.opencpu.org")`) you can
access values and methods on the object `x`.

## handles

curl handles are re-used on the level of the connection object, that is,
each `HttpClient` object is separate from one another so as to better
separate connections.

If you don't pass in a curl handle to the `handle` parameter, it gets
created when a HTTP verb is called. Thus, if you try to get `handle`
after creating a `HttpClient` object only passing `url` parameter,
`handle` will be `NULL`. If you pass a curl handle to the `handle`
parameter, then you can get the handle from the `HttpClient` object. The
response from a http verb request does have the handle in the `handle`
slot.

## See also

[http-headers](https://docs.ropensci.org/crul/reference/http-headers.md),
[writing-options](https://docs.ropensci.org/crul/reference/writing-options.md),
[cookies](https://docs.ropensci.org/crul/reference/cookies.md),
[hooks](https://docs.ropensci.org/crul/reference/hooks.md)

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

- `hooks`:

  a named list, see
  [hooks](https://docs.ropensci.org/crul/reference/hooks.md)

## Methods

### Public methods

- [`HttpClient$print()`](#method-HttpClient-print)

- [`HttpClient$new()`](#method-HttpClient-new)

- [`HttpClient$get()`](#method-HttpClient-get)

- [`HttpClient$post()`](#method-HttpClient-post)

- [`HttpClient$put()`](#method-HttpClient-put)

- [`HttpClient$patch()`](#method-HttpClient-patch)

- [`HttpClient$delete()`](#method-HttpClient-delete)

- [`HttpClient$head()`](#method-HttpClient-head)

- [`HttpClient$verb()`](#method-HttpClient-verb)

- [`HttpClient$retry()`](#method-HttpClient-retry)

- [`HttpClient$handle_pop()`](#method-HttpClient-handle_pop)

- [`HttpClient$url_fetch()`](#method-HttpClient-url_fetch)

- [`HttpClient$clone()`](#method-HttpClient-clone)

------------------------------------------------------------------------

### Method [`print()`](https://rdrr.io/r/base/print.html)

print method for `HttpClient` objects

#### Usage

    HttpClient$print(x, ...)

#### Arguments

- `x`:

  self

- `...`:

  ignored

------------------------------------------------------------------------

### Method [`new()`](https://rdrr.io/r/methods/new.html)

Create a new HttpClient object

#### Usage

    HttpClient$new(
      url,
      opts,
      proxies,
      auth,
      headers,
      handle,
      progress,
      hooks,
      verbose
    )

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

- `hooks`:

  a named list, see
  [hooks](https://docs.ropensci.org/crul/reference/hooks.md)

- `verbose`:

  a special handler for verbose curl output, accepts a function only.
  default is `NULL`. if used, `verbose` and `debugfunction` curl options
  are ignored if passed to `opts` on `$new()` and ignored if `...`
  passed to a http method call

- `urls`:

  (character) one or more URLs

#### Returns

A new `HttpClient` object

------------------------------------------------------------------------

### Method [`get()`](https://rdrr.io/r/base/get.html)

Make a GET request

#### Usage

    HttpClient$get(
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

  query terms, as a named list. any numeric values are passed through
  [`format()`](https://rdrr.io/r/base/format.html) to prevent larger
  numbers from being scientifically formatted

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

  For `retry`, the options to be passed on to the method implementing
  the requested verb, including curl options. Otherwise, curl options,
  only those in the acceptable set from
  [`curl::curl_options()`](https://jeroen.r-universe.dev/curl/reference/curl_options.html)
  except the following: httpget, httppost, post, postfields,
  postfieldsize, and customrequest

------------------------------------------------------------------------

### Method `post()`

Make a POST request

#### Usage

    HttpClient$post(
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

  query terms, as a named list. any numeric values are passed through
  [`format()`](https://rdrr.io/r/base/format.html) to prevent larger
  numbers from being scientifically formatted

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

  For `retry`, the options to be passed on to the method implementing
  the requested verb, including curl options. Otherwise, curl options,
  only those in the acceptable set from
  [`curl::curl_options()`](https://jeroen.r-universe.dev/curl/reference/curl_options.html)
  except the following: httpget, httppost, post, postfields,
  postfieldsize, and customrequest

------------------------------------------------------------------------

### Method `put()`

Make a PUT request

#### Usage

    HttpClient$put(
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

  query terms, as a named list. any numeric values are passed through
  [`format()`](https://rdrr.io/r/base/format.html) to prevent larger
  numbers from being scientifically formatted

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

  For `retry`, the options to be passed on to the method implementing
  the requested verb, including curl options. Otherwise, curl options,
  only those in the acceptable set from
  [`curl::curl_options()`](https://jeroen.r-universe.dev/curl/reference/curl_options.html)
  except the following: httpget, httppost, post, postfields,
  postfieldsize, and customrequest

------------------------------------------------------------------------

### Method `patch()`

Make a PATCH request

#### Usage

    HttpClient$patch(
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

  query terms, as a named list. any numeric values are passed through
  [`format()`](https://rdrr.io/r/base/format.html) to prevent larger
  numbers from being scientifically formatted

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

  For `retry`, the options to be passed on to the method implementing
  the requested verb, including curl options. Otherwise, curl options,
  only those in the acceptable set from
  [`curl::curl_options()`](https://jeroen.r-universe.dev/curl/reference/curl_options.html)
  except the following: httpget, httppost, post, postfields,
  postfieldsize, and customrequest

------------------------------------------------------------------------

### Method `delete()`

Make a DELETE request

#### Usage

    HttpClient$delete(
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

  query terms, as a named list. any numeric values are passed through
  [`format()`](https://rdrr.io/r/base/format.html) to prevent larger
  numbers from being scientifically formatted

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

  For `retry`, the options to be passed on to the method implementing
  the requested verb, including curl options. Otherwise, curl options,
  only those in the acceptable set from
  [`curl::curl_options()`](https://jeroen.r-universe.dev/curl/reference/curl_options.html)
  except the following: httpget, httppost, post, postfields,
  postfieldsize, and customrequest

------------------------------------------------------------------------

### Method [`head()`](https://rdrr.io/r/utils/head.html)

Make a HEAD request

#### Usage

    HttpClient$head(
      path = NULL,
      query = list(),
      mock = getOption("crul_mock", NULL),
      ...
    )

#### Arguments

- `path`:

  URL path, appended to the base URL

- `query`:

  query terms, as a named list. any numeric values are passed through
  [`format()`](https://rdrr.io/r/base/format.html) to prevent larger
  numbers from being scientifically formatted

- `mock`:

  A mocking function. If supplied, this function is called with the
  request. It should return either `NULL` (if it doesn't want to handle
  the request) or a
  [HttpResponse](https://docs.ropensci.org/crul/reference/HttpResponse.md)
  (if it does).

- `...`:

  For `retry`, the options to be passed on to the method implementing
  the requested verb, including curl options. Otherwise, curl options,
  only those in the acceptable set from
  [`curl::curl_options()`](https://jeroen.r-universe.dev/curl/reference/curl_options.html)
  except the following: httpget, httppost, post, postfields,
  postfieldsize, and customrequest

------------------------------------------------------------------------

### Method `verb()`

Use an arbitrary HTTP verb supported on this class Supported verbs:
"get", "post", "put", "patch", "delete", "head". Also supports retry

#### Usage

    HttpClient$verb(verb, ...)

#### Arguments

- `verb`:

  an HTTP verb supported on this class: "get", "post", "put", "patch",
  "delete", "head". Also supports retry.

- `...`:

  For `retry`, the options to be passed on to the method implementing
  the requested verb, including curl options. Otherwise, curl options,
  only those in the acceptable set from
  [`curl::curl_options()`](https://jeroen.r-universe.dev/curl/reference/curl_options.html)
  except the following: httpget, httppost, post, postfields,
  postfieldsize, and customrequest

#### Examples

    \dontrun{
    (x <- HttpClient$new(url = "https://hb.opencpu.org"))
    x$verb('get')
    x$verb('GET')
    x$verb('GET', query = list(foo = "bar"))
    x$verb('retry', 'GET', path = "status/400")
    }

------------------------------------------------------------------------

### Method `retry()`

Retry a request

#### Usage

    HttpClient$retry(
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

  an HTTP verb supported on this class: "get", "post", "put", "patch",
  "delete", "head". Also supports retry.

- `...`:

  For `retry`, the options to be passed on to the method implementing
  the requested verb, including curl options. Otherwise, curl options,
  only those in the acceptable set from
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

#### Details

Retries the request given by `verb` until successful (HTTP response
status \< 400), or a condition for giving up is met. Automatically
recognizes `Retry-After` and `X-RateLimit-Reset` headers in the response
for rate-limited remote APIs.

#### Examples

    \dontrun{
    x <- HttpClient$new(url = "https://hb.opencpu.org")

    # retry, by default at most 3 times
    (res_get <- x$retry("GET", path = "status/400"))

    # retry, but not for 404 NOT FOUND
    (res_get <- x$retry("GET", path = "status/404", terminate_on = c(404)))

    # retry, but only for exceeding rate limit (note that e.g. Github uses 403)
    (res_get <- x$retry("GET", path = "status/429", retry_only_on = c(403, 429)))
    }

------------------------------------------------------------------------

### Method `handle_pop()`

reset your curl handle

#### Usage

    HttpClient$handle_pop()

------------------------------------------------------------------------

### Method `url_fetch()`

get the URL that would be sent (i.e., before executing the request) the
only things that change the URL are path and query parameters; body and
any curl options don't change the URL

#### Usage

    HttpClient$url_fetch(path = NULL, query = list())

#### Arguments

- `path`:

  URL path, appended to the base URL

- `query`:

  query terms, as a named list. any numeric values are passed through
  [`format()`](https://rdrr.io/r/base/format.html) to prevent larger
  numbers from being scientifically formatted

#### Returns

URL (character)

#### Examples

    x <- HttpClient$new(url = "https://hb.opencpu.org")
    x$url_fetch()
    x$url_fetch('get')
    x$url_fetch('post')
    x$url_fetch('get', query = list(foo = "bar"))

------------------------------------------------------------------------

### Method `clone()`

The objects of this class are cloneable with this method.

#### Usage

    HttpClient$clone(deep = FALSE)

#### Arguments

- `deep`:

  Whether to make a deep clone.

## Examples

``` r
if (FALSE) { # \dontrun{
# set your own handle
(h <- handle("https://hb.opencpu.org"))
(x <- HttpClient$new(handle = h))
x$handle
x$url
(out <- x$get("get"))
x$handle
x$url
class(out)
out$handle
out$request_headers
out$response_headers
out$response_headers_all

# if you just pass a url, we create a handle for you
#  this is how most people will use HttpClient
(x <- HttpClient$new(url = "https://hb.opencpu.org"))
x$url
x$handle # is empty, it gets created when a HTTP verb is called
(r1 <- x$get("get"))
x$url
x$handle
r1$url
r1$handle
r1$content
r1$response_headers
r1$parse()

(res_get2 <- x$get("get", query = list(hello = "world")))
res_get2$parse()
library("jsonlite")
jsonlite::fromJSON(res_get2$parse())

# post request
(res_post <- x$post("post", body = list(hello = "world")))

## empty body request
x$post("post")

# put request
(res_put <- x$put("put"))

# delete request
(res_delete <- x$delete("delete"))

# patch request
(res_patch <- x$patch("patch"))

# head request
(res_head <- x$head())

# query params are URL encoded for you, so DO NOT do it yourself
## if you url encode yourself, it gets double encoded, and that's bad
(x <- HttpClient$new(url = "https://hb.opencpu.org"))
res <- x$get("get", query = list(a = "hello world"))

# access intermediate headers in response_headers_all
x <- HttpClient$new("https://doi.org/10.1007/978-3-642-40455-9_52-1")
bb <- x$get()
bb$response_headers_all
} # }

## ------------------------------------------------
## Method `HttpClient$verb`
## ------------------------------------------------

if (FALSE) { # \dontrun{
(x <- HttpClient$new(url = "https://hb.opencpu.org"))
x$verb('get')
x$verb('GET')
x$verb('GET', query = list(foo = "bar"))
x$verb('retry', 'GET', path = "status/400")
} # }

## ------------------------------------------------
## Method `HttpClient$retry`
## ------------------------------------------------

if (FALSE) { # \dontrun{
x <- HttpClient$new(url = "https://hb.opencpu.org")

# retry, by default at most 3 times
(res_get <- x$retry("GET", path = "status/400"))

# retry, but not for 404 NOT FOUND
(res_get <- x$retry("GET", path = "status/404", terminate_on = c(404)))

# retry, but only for exceeding rate limit (note that e.g. Github uses 403)
(res_get <- x$retry("GET", path = "status/429", retry_only_on = c(403, 429)))
} # }

## ------------------------------------------------
## Method `HttpClient$url_fetch`
## ------------------------------------------------

x <- HttpClient$new(url = "https://hb.opencpu.org")
x$url_fetch()
#> [1] "https://hb.opencpu.org/"
x$url_fetch('get')
#> [1] "https://hb.opencpu.org/get"
x$url_fetch('post')
#> [1] "https://hb.opencpu.org/post"
x$url_fetch('get', query = list(foo = "bar"))
#> [1] "https://hb.opencpu.org/get?foo=bar"
```
