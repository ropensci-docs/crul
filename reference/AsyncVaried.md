# Async client for different request types

An async client to do many requests, each with different URLs, curl
options, etc.

## Value

An object of class `AsyncVaried` with variables and methods.
[HttpResponse](https://docs.ropensci.org/crul/reference/HttpResponse.md)
objects are returned in the order they are passed in. We print the first
10.

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
[`Async`](https://docs.ropensci.org/crul/reference/Async.md),
[`AsyncQueue`](https://docs.ropensci.org/crul/reference/AsyncQueue.md),
[`HttpRequest`](https://docs.ropensci.org/crul/reference/HttpRequest.md)

## Public fields

- `mock`:

  a mocking function. could be `NULL` too

## Methods

### Public methods

- [`AsyncVaried$print()`](#method-AsyncVaried-print)

- [`AsyncVaried$new()`](#method-AsyncVaried-new)

- [`AsyncVaried$request()`](#method-AsyncVaried-request)

- [`AsyncVaried$responses()`](#method-AsyncVaried-responses)

- [`AsyncVaried$requests()`](#method-AsyncVaried-requests)

- [`AsyncVaried$parse()`](#method-AsyncVaried-parse)

- [`AsyncVaried$status_code()`](#method-AsyncVaried-status_code)

- [`AsyncVaried$status()`](#method-AsyncVaried-status)

- [`AsyncVaried$content()`](#method-AsyncVaried-content)

- [`AsyncVaried$times()`](#method-AsyncVaried-times)

- [`AsyncVaried$clone()`](#method-AsyncVaried-clone)

------------------------------------------------------------------------

### Method [`print()`](https://rdrr.io/r/base/print.html)

print method for AsyncVaried objects

#### Usage

    AsyncVaried$print(x, ...)

#### Arguments

- `x`:

  self

- `...`:

  ignored

------------------------------------------------------------------------

### Method `new()`

Create a new AsyncVaried object

#### Usage

    AsyncVaried$new(..., .list = list(), mock = getOption("crul_mock", NULL))

#### Arguments

- `..., .list`:

  Any number of objects of class
  [`HttpRequest()`](https://docs.ropensci.org/crul/reference/HttpRequest.md),
  must supply inputs to one of these parameters, but not both

- `mock`:

  A mocking function. If supplied, this function is called with the
  request. It should return either `NULL` (if it doesn't want to handle
  the request) or a
  [HttpResponse](https://docs.ropensci.org/crul/reference/HttpResponse.md)
  (if it does).

#### Returns

A new `AsyncVaried` object

------------------------------------------------------------------------

### Method `request()`

Execute asynchronous requests

#### Usage

    AsyncVaried$request()

#### Returns

nothing, responses stored inside object, though will print messages if
you choose verbose output

------------------------------------------------------------------------

### Method `responses()`

List responses

#### Usage

    AsyncVaried$responses()

#### Details

An S3 print method is used to summarise results.
[unclass](https://rdrr.io/r/base/class.html) the output to see the list,
or index to results, e.g., `[1]`, `[1:3]`

#### Returns

a list of `HttpResponse` objects, empty list before requests made

------------------------------------------------------------------------

### Method `requests()`

List requests

#### Usage

    AsyncVaried$requests()

#### Returns

a list of `HttpRequest` objects, empty list before requests made

------------------------------------------------------------------------

### Method [`parse()`](https://rdrr.io/r/base/parse.html)

parse content

#### Usage

    AsyncVaried$parse(encoding = "UTF-8")

#### Arguments

- `encoding`:

  (character) the encoding to use in parsing. default:"UTF-8"

#### Returns

character vector, empty character vector before requests made

------------------------------------------------------------------------

### Method `status_code()`

Get HTTP status codes for each response

#### Usage

    AsyncVaried$status_code()

#### Returns

numeric vector, empty numeric vector before requests made

------------------------------------------------------------------------

### Method `status()`

List HTTP status objects

#### Usage

    AsyncVaried$status()

#### Returns

a list of `http_code` objects, empty list before requests made

------------------------------------------------------------------------

### Method `content()`

Get raw content for each response

#### Usage

    AsyncVaried$content()

#### Returns

raw list, empty list before requests made

------------------------------------------------------------------------

### Method `times()`

curl request times

#### Usage

    AsyncVaried$times()

#### Returns

list of named numeric vectors, empty list before requests made

------------------------------------------------------------------------

### Method `clone()`

The objects of this class are cloneable with this method.

#### Usage

    AsyncVaried$clone(deep = FALSE)

#### Arguments

- `deep`:

  Whether to make a deep clone.

## Examples

``` r
if (FALSE) { # interactive()
# pass in requests via ...
req1 <- HttpRequest$new(
  url = "https://hb.opencpu.org/get",
  opts = list(verbose = TRUE),
  headers = list(foo = "bar")
)$get()
req2 <- HttpRequest$new(url = "https://hb.opencpu.org/post")$post()

# Create an AsyncVaried object
out <- AsyncVaried$new(req1, req2)

# before you make requests, the methods return empty objects
out$status()
out$status_code()
out$content()
out$times()
out$parse()
out$responses()

# make requests
out$request()

# access various parts
## http status objects
out$status()
## status codes
out$status_code()
## content (raw data)
out$content()
## times
out$times()
## parsed content
out$parse()
## response objects
out$responses()

# use $verb() method to select http verb
method <- "post"
req1 <- HttpRequest$new(
  url = "https://hb.opencpu.org/post",
  opts = list(verbose = TRUE),
  headers = list(foo = "bar")
)$verb(method)
req2 <- HttpRequest$new(url = "https://hb.opencpu.org/post")$verb(method)
out <- AsyncVaried$new(req1, req2)
out
out$request()
out$responses()

# pass in requests in a list via .list param
reqlist <- list(
  HttpRequest$new(url = "https://hb.opencpu.org/get")$get(),
  HttpRequest$new(url = "https://hb.opencpu.org/post")$post(),
  HttpRequest$new(url = "https://hb.opencpu.org/put")$put(),
  HttpRequest$new(url = "https://hb.opencpu.org/delete")$delete(),
  HttpRequest$new(url = "https://hb.opencpu.org/get?g=5")$get(),
  HttpRequest$new(
    url = "https://hb.opencpu.org/post")$post(body = list(y = 9)),
  HttpRequest$new(
    url = "https://hb.opencpu.org/get")$get(query = list(hello = "world"))
)

out <- AsyncVaried$new(.list = reqlist)
out$request()
out$status()
out$status_code()
out$content()
out$times()
out$parse()

# using auth with async
url <- "https://hb.opencpu.org/basic-auth/user/passwd"
auth <- auth(user = "user", pwd = "passwd")
reqlist <- list(
  HttpRequest$new(url = url, auth = auth)$get(),
  HttpRequest$new(url = url, auth = auth)$get(query = list(a=5)),
  HttpRequest$new(url = url, auth = auth)$get(query = list(b=3))
)
out <- AsyncVaried$new(.list = reqlist)
out$request()
out$status()
out$parse()

# failure behavior
## e.g. when a URL doesn't exist, a timeout, etc.
reqlist <- list(
  HttpRequest$new(url = "http://stuffthings.gvb")$get(),
  HttpRequest$new(url = "https://hb.opencpu.org")$head(),
  HttpRequest$new(url = "https://hb.opencpu.org",
   opts = list(timeout_ms = 10))$head()
)
(tmp <- AsyncVaried$new(.list = reqlist))
tmp$request()
tmp$responses()
tmp$parse("UTF-8")

# access intemediate redirect headers
dois <- c("10.7202/1045307ar", "10.1242/jeb.088898", "10.1121/1.3383963")
reqlist <- list(
  HttpRequest$new(url = paste0("https://doi.org/", dois[1]))$get(),
  HttpRequest$new(url = paste0("https://doi.org/", dois[2]))$get(),
  HttpRequest$new(url = paste0("https://doi.org/", dois[3]))$get()
)
tmp <- AsyncVaried$new(.list = reqlist)
tmp$request()
tmp
lapply(tmp$responses(), "[[", "response_headers_all")

# retry
reqlist <- list(
  HttpRequest$new(url = "https://hb.opencpu.org/get")$get(),
  HttpRequest$new(url = "https://hb.opencpu.org/post")$post(),
  HttpRequest$new(url = "https://hb.opencpu.org/status/404")$retry("get"),
  HttpRequest$new(url = "https://hb.opencpu.org/status/429")$retry("get",
   retry_only_on = c(403, 429), times = 2)
)
tmp <- AsyncVaried$new(.list = reqlist)
tmp
tmp$request()
tmp$responses()[[3]]

# mock
url <- "https://hb.opencpu.org/get"
mock_fun <- function(status) {
  function(req) {
    HttpResponse$new(method = "GET", url = "http://google.com",
      status_code = status)
  }
}
reqlist <- list(
  HttpRequest$new(url = url)$get(mock = mock_fun(status=418L)),
  HttpRequest$new(url = url)$get(mock = mock_fun(status=201)),
  HttpRequest$new(url = url)$get(mock = mock_fun(status=501L))
)
tmp <- AsyncVaried$new(.list = reqlist)
tmp
tmp$request()
tmp$status()
}
```
