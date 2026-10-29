# crul: HTTP Client

A simple HTTP client, with tools for making HTTP requests, and mocking
HTTP requests. The package is built on R6, and takes inspiration from
Ruby's 'faraday' gem (<https://rubygems.org/gems/faraday>). The package
name is a play on curl, the widely used command line tool for HTTP, and
this package is built on top of the R package 'curl', an interface to
'libcurl' (<https://curl.se/libcurl/>).

## Package API

- [`HttpClient()`](https://docs.ropensci.org/crul/reference/HttpClient.md) -
  create a connection client, set all your http options, make http
  requests

- [`HttpResponse()`](https://docs.ropensci.org/crul/reference/HttpResponse.md) -
  mostly for internal use, handles http responses

- [`Paginator()`](https://docs.ropensci.org/crul/reference/Paginator.md) -
  auto-paginate through requests

- [`Async()`](https://docs.ropensci.org/crul/reference/Async.md) -
  asynchronous requests

- [`AsyncVaried()`](https://docs.ropensci.org/crul/reference/AsyncVaried.md) -
  varied asynchronous requests

- [`HttpRequest()`](https://docs.ropensci.org/crul/reference/HttpRequest.md) -
  generate an HTTP request, mostly for use in building requests to be
  used in `Async` or `AsyncVaried`

- [`mock()`](https://docs.ropensci.org/crul/reference/mock.md) - Turn
  on/off mocking, via `webmockr`

- [`auth()`](https://docs.ropensci.org/crul/reference/auth.md) - Simple
  authentication helper

- [`proxy()`](https://docs.ropensci.org/crul/reference/proxies.md) -
  Proxy helper

- [`upload()`](https://docs.ropensci.org/crul/reference/upload.md) -
  File upload helper

- set curl options globally:
  [`set_auth()`](https://docs.ropensci.org/crul/reference/crul-options.md),
  [`set_headers()`](https://docs.ropensci.org/crul/reference/crul-options.md),
  [`set_opts()`](https://docs.ropensci.org/crul/reference/crul-options.md),
  [`set_proxy()`](https://docs.ropensci.org/crul/reference/crul-options.md),
  and
  [`crul_settings()`](https://docs.ropensci.org/crul/reference/crul-options.md)

## HTTP verbs (or HTTP request methods)

See [verb-GET](https://docs.ropensci.org/crul/reference/verb-GET.md),
[verb-POST](https://docs.ropensci.org/crul/reference/verb-POST.md),
[verb-PUT](https://docs.ropensci.org/crul/reference/verb-PUT.md),
[verb-PATCH](https://docs.ropensci.org/crul/reference/verb-PATCH.md),
[verb-DELETE](https://docs.ropensci.org/crul/reference/verb-DELETE.md),
[verb-HEAD](https://docs.ropensci.org/crul/reference/verb-HEAD.md) for
details.

- [HttpClient](https://docs.ropensci.org/crul/reference/HttpClient.md)
  is the main interface for making HTTP requests, and includes methods
  for each HTTP verb

- [HttpRequest](https://docs.ropensci.org/crul/reference/HttpRequest.md)
  allows you to prepare a HTTP payload for use with
  [AsyncVaried](https://docs.ropensci.org/crul/reference/AsyncVaried.md),
  which provides asynchronous requests for varied HTTP methods

- [Async](https://docs.ropensci.org/crul/reference/Async.md) provides
  asynchronous requests for a single HTTP method at a time

- the `verb()` method can be used on all the above to request a specific
  HTTP verb

## Checking HTTP responses

[`HttpResponse()`](https://docs.ropensci.org/crul/reference/HttpResponse.md)
has helpers for checking and raising warnings/errors.

- [content-types](https://docs.ropensci.org/crul/reference/content-types.md)
  details the various options for checking content types and throwing a
  warning or error if the response content type doesn't match what you
  expect. Mis-matched content-types are typically a good sign of a bad
  response. There's methods built in for json, xml and html, with the
  ability to set any custom content type

- `raise_for_status()` is a method on
  [`HttpResponse()`](https://docs.ropensci.org/crul/reference/HttpResponse.md)
  that checks the HTTP status code, and errors with the appropriate
  message for the HTTP status code, optionally using the package
  `fauxpas` if it's installed.

## HTTP conditions

We use `fauxpas` if you have it installed for handling HTTP conditions
but if it's not installed we use httpcode

## Mocking

Mocking HTTP requests is supported via the webmockr package. See
[mock](https://docs.ropensci.org/crul/reference/mock.md) for guidance,
and <https://books.ropensci.org/http-testing/>

## Caching

Caching HTTP requests is supported via the vcr package. See
<https://books.ropensci.org/http-testing/>

## Links

Source code: <https://github.com/ropensci/crul>

Bug reports/feature requests: <https://github.com/ropensci/crul/issues>

## See also

Useful links:

- <https://docs.ropensci.org/crul/>

- <https://github.com/ropensci/crul>

- <https://books.ropensci.org/http-testing/>

- Report bugs at <https://github.com/ropensci/crul/issues>

## Author

**Maintainer**: Scott Chamberlain <myrmecocystus@gmail.com>
([ORCID](https://orcid.org/0000-0003-1444-9135))
