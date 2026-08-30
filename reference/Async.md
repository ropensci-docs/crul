# Simple async client

An async client to work with many URLs, but all with the same HTTP
method

## Value

a list, with objects of class
[`HttpResponse()`](https://docs.ropensci.org/crul/reference/HttpResponse.md).
Responses are returned in the order they are passed in. We print the
first 10.

## Details

See
[`HttpClient()`](https://docs.ropensci.org/crul/reference/HttpClient.md)
for information on parameters.

## Failure behavior

HTTP requests mostly fail in ways that you are probably familiar with,
including when there's a 400 response (the URL not found), and when the
server made a mistake (a 500 series HTTP status code).

But requests can fail sometimes where there is no HTTP status code, and
no agreed upon way to handle it other than to just fail immediately.

When a request fails when using synchronous requests (see
[HttpClient](https://docs.ropensci.org/crul/reference/HttpClient.md))
you get an error message that stops your code progression immediately
saying for example:

- "Could not resolve host: https://foo.com"

- "Failed to connect to foo.com"

- "Resolving timed out after 10 milliseconds"

However, for async requests we don't want to fail immediately because
that would stop the subsequent requests from occurring. Thus, when we
find that a request fails for one of the reasons above we give back a
[HttpResponse](https://docs.ropensci.org/crul/reference/HttpResponse.md)
object just like any other response, and:

- capture the error message and put it in the `content` slot of the
  response object (thus calls to `content` and
  [`parse()`](https://rdrr.io/r/base/parse.html) work correctly)

- give back a `0` HTTP status code. we handle this specially when
  testing whether the request was successful or not with e.g., the
  `success()` method

## R6 classes

This is an R6 class from the package R6. Find out more about R6 at
<https://r6.r-lib.org/>. After creating an instance of an R6 class
(e.g., `x <- HttpClient$new(url = "https://hb.opencpu.org")`) you can
access values and methods on the object `x`.

## See also

Other async:
[`AsyncQueue`](https://docs.ropensci.org/crul/reference/AsyncQueue.md),
[`AsyncVaried`](https://docs.ropensci.org/crul/reference/AsyncVaried.md),
[`HttpRequest`](https://docs.ropensci.org/crul/reference/HttpRequest.md)

## Public fields

- `urls`:

  (character) one or more URLs

- `opts`:

  any curl options

- `proxies`:

  named list of headers

- `auth`:

  an object of class `auth`

- `headers`:

  named list of headers

## Methods

### Public methods

- [`Async$print()`](#method-Async-print)

- [`Async$new()`](#method-Async-new)

- [`Async$get()`](#method-Async-get)

- [`Async$post()`](#method-Async-post)

- [`Async$put()`](#method-Async-put)

- [`Async$patch()`](#method-Async-patch)

- [`Async$delete()`](#method-Async-delete)

- [`Async$head()`](#method-Async-head)

- [`Async$retry()`](#method-Async-retry)

- [`Async$verb()`](#method-Async-verb)

- [`Async$clone()`](#method-Async-clone)

------------------------------------------------------------------------

### Method [`print()`](https://rdrr.io/r/base/print.html)

print method for Async objects

#### Usage

    Async$print(x, ...)

#### Arguments

- `x`:

  self

- `...`:

  ignored

------------------------------------------------------------------------

### Method `new()`

Create a new Async object

#### Usage

    Async$new(urls, opts, proxies, auth, headers)

#### Arguments

- `urls`:

  (character) one or more URLs

- `opts`:

  any curl options

- `proxies`:

  a [`proxy()`](https://docs.ropensci.org/crul/reference/proxies.md)
  object

- `auth`:

  an [`auth()`](https://docs.ropensci.org/crul/reference/auth.md) object

- `headers`:

  named list of headers

#### Returns

A new `Async` object.

------------------------------------------------------------------------

### Method [`get()`](https://rdrr.io/r/base/get.html)

execute the `GET` http verb for the `urls`

#### Usage

    Async$get(
      path = NULL,
      query = list(),
      disk = NULL,
      stream = NULL,
      mock = getOption("crul_mock", NULL),
      ...
    )

#### Arguments

- `path`:

  (character) URL path, appended to the base URL

- `query`:

  (list) query terms, as a named list

- `disk`:

  a path to write to. if NULL (default), memory used. See
  [`curl::curl_fetch_disk()`](https://jeroen.r-universe.dev/curl/reference/curl_fetch.html)
  for help.

- `stream`:

  an R function to determine how to stream data. if `NULL` (default),
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

#### Examples

    \dontrun{
    (cc <- Async$new(urls = c(
        'https://hb.opencpu.org/',
        'https://hb.opencpu.org/get?a=5',
        'https://hb.opencpu.org/get?foo=bar'
      )))
    (res <- cc$get())
    }

------------------------------------------------------------------------

### Method `post()`

execute the `POST` http verb for the `urls`

#### Usage

    Async$post(
      path = NULL,
      query = list(),
      body = NULL,
      encode = "multipart",
      disk = NULL,
      stream = NULL,
      mock = getOption("crul_mock", NULL),
      ...
    )

#### Arguments

- `path`:

  (character) URL path, appended to the base URL

- `query`:

  (list) query terms, as a named list

- `body`:

  body as an R list

- `encode`:

  one of form, multipart, json, or raw

- `disk`:

  a path to write to. if NULL (default), memory used. See
  [`curl::curl_fetch_disk()`](https://jeroen.r-universe.dev/curl/reference/curl_fetch.html)
  for help.

- `stream`:

  an R function to determine how to stream data. if `NULL` (default),
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

### Method `put()`

execute the `PUT` http verb for the `urls`

#### Usage

    Async$put(
      path = NULL,
      query = list(),
      body = NULL,
      encode = "multipart",
      disk = NULL,
      stream = NULL,
      mock = getOption("crul_mock", NULL),
      ...
    )

#### Arguments

- `path`:

  (character) URL path, appended to the base URL

- `query`:

  (list) query terms, as a named list

- `body`:

  body as an R list

- `encode`:

  one of form, multipart, json, or raw

- `disk`:

  a path to write to. if NULL (default), memory used. See
  [`curl::curl_fetch_disk()`](https://jeroen.r-universe.dev/curl/reference/curl_fetch.html)
  for help.

- `stream`:

  an R function to determine how to stream data. if `NULL` (default),
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

### Method `patch()`

execute the `PATCH` http verb for the `urls`

#### Usage

    Async$patch(
      path = NULL,
      query = list(),
      body = NULL,
      encode = "multipart",
      disk = NULL,
      stream = NULL,
      mock = getOption("crul_mock", NULL),
      ...
    )

#### Arguments

- `path`:

  (character) URL path, appended to the base URL

- `query`:

  (list) query terms, as a named list

- `body`:

  body as an R list

- `encode`:

  one of form, multipart, json, or raw

- `disk`:

  a path to write to. if NULL (default), memory used. See
  [`curl::curl_fetch_disk()`](https://jeroen.r-universe.dev/curl/reference/curl_fetch.html)
  for help.

- `stream`:

  an R function to determine how to stream data. if `NULL` (default),
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

### Method `delete()`

execute the `DELETE` http verb for the `urls`

#### Usage

    Async$delete(
      path = NULL,
      query = list(),
      body = NULL,
      encode = "multipart",
      disk = NULL,
      stream = NULL,
      mock = getOption("crul_mock", NULL),
      ...
    )

#### Arguments

- `path`:

  (character) URL path, appended to the base URL

- `query`:

  (list) query terms, as a named list

- `body`:

  body as an R list

- `encode`:

  one of form, multipart, json, or raw

- `disk`:

  a path to write to. if NULL (default), memory used. See
  [`curl::curl_fetch_disk()`](https://jeroen.r-universe.dev/curl/reference/curl_fetch.html)
  for help.

- `stream`:

  an R function to determine how to stream data. if `NULL` (default),
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

### Method [`head()`](https://rdrr.io/r/utils/head.html)

execute the `HEAD` http verb for the `urls`

#### Usage

    Async$head(path = NULL, mock = getOption("crul_mock", NULL), ...)

#### Arguments

- `path`:

  (character) URL path, appended to the base URL

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

### Method `retry()`

execute the `RETRY` http verb for the `urls`. see
[`HttpRequest$retry`](https://docs.ropensci.org/crul/reference/HttpRequest.md)
method for parameters

#### Usage

    Async$retry(...)

#### Arguments

- `...`:

  curl options, only those in the acceptable set from
  [`curl::curl_options()`](https://jeroen.r-universe.dev/curl/reference/curl_options.html)
  except the following: httpget, httppost, post, postfields,
  postfieldsize, and customrequest

------------------------------------------------------------------------

### Method `verb()`

execute any supported HTTP verb

#### Usage

    Async$verb(verb, ...)

#### Arguments

- `verb`:

  (character) a supported HTTP verb: get, post, put, patch, delete,
  head.

- `...`:

  curl options, only those in the acceptable set from
  [`curl::curl_options()`](https://jeroen.r-universe.dev/curl/reference/curl_options.html)
  except the following: httpget, httppost, post, postfields,
  postfieldsize, and customrequest

#### Examples

    \dontrun{
    cc <- Async$new(
      urls = c(
        'https://hb.opencpu.org/',
        'https://hb.opencpu.org/get?a=5',
        'https://hb.opencpu.org/get?foo=bar'
      )
    )
    (res <- cc$verb('get'))
    lapply(res, function(z) z$parse("UTF-8"))
    }

------------------------------------------------------------------------

### Method `clone()`

The objects of this class are cloneable with this method.

#### Usage

    Async$clone(deep = FALSE)

#### Arguments

- `deep`:

  Whether to make a deep clone.

## Examples

``` r
if (FALSE) { # interactive()
cc <- Async$new(
  urls = c(
    'https://hb.opencpu.org/',
    'https://hb.opencpu.org/get?a=5',
    'https://hb.opencpu.org/get?foo=bar'
  )
)
cc
(res <- cc$get())
res[[1]]
res[[1]]$url
res[[1]]$success()
res[[1]]$status_http()
res[[1]]$response_headers
res[[1]]$method
res[[1]]$content
res[[1]]$parse("UTF-8")
lapply(res, function(z) z$parse("UTF-8"))

# curl options/headers with async
urls = c(
 'https://hb.opencpu.org/',
 'https://hb.opencpu.org/get?a=5',
 'https://hb.opencpu.org/get?foo=bar'
)
cc <- Async$new(urls = urls,
  opts = list(verbose = TRUE),
  headers = list(foo = "bar")
)
cc
(res <- cc$get())

# using auth with async
dd <- Async$new(
  urls = rep('https://hb.opencpu.org/basic-auth/user/passwd', 3),
  auth = auth(user = "foo", pwd = "passwd"),
  opts = list(verbose = TRUE)
)
dd
res <- dd$get()
res
vapply(res, function(z) z$status_code, double(1))
vapply(res, function(z) z$success(), logical(1))
lapply(res, function(z) z$parse("UTF-8"))

# failure behavior
## e.g. when a URL doesn't exist, a timeout, etc.
urls <- c("http://stuffthings.gvb", "https://foo.com",
  "https://hb.opencpu.org/get")
conn <- Async$new(urls = urls)
res <- conn$get()
res[[1]]$parse("UTF-8") # a failure
res[[2]]$parse("UTF-8") # a failure
res[[3]]$parse("UTF-8") # a success

# retry
urls = c("https://hb.opencpu.org/status/404", "https://hb.opencpu.org/status/429")
conn <- Async$new(urls = urls)
res <- conn$retry(verb="get")

# mock
cc <- Async$new(
  urls = c(
    'https://hb.opencpu.org/',
    'https://hb.opencpu.org/get?a=5',
    'https://hb.opencpu.org/get?foo=bar'
  )
)
fun <- function(req) {
  HttpResponse$new(method = "GET", url = "http://google.com",
    status_code = 401L)
}
cc$get(mock = fun)
}

## ------------------------------------------------
## Method `Async$get`
## ------------------------------------------------

if (FALSE) { # \dontrun{
(cc <- Async$new(urls = c(
    'https://hb.opencpu.org/',
    'https://hb.opencpu.org/get?a=5',
    'https://hb.opencpu.org/get?foo=bar'
  )))
(res <- cc$get())
} # }

## ------------------------------------------------
## Method `Async$verb`
## ------------------------------------------------

if (FALSE) { # \dontrun{
cc <- Async$new(
  urls = c(
    'https://hb.opencpu.org/',
    'https://hb.opencpu.org/get?a=5',
    'https://hb.opencpu.org/get?foo=bar'
  )
)
(res <- cc$verb('get'))
lapply(res, function(z) z$parse("UTF-8"))
} # }
```
