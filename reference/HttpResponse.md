# Base HTTP response object

Class with methods for handling HTTP responses

## Details

**Additional Methods**

- `raise_for_ct(type, charset = NULL, behavior = "stop")`:

  Check response content-type; stop or warn if not matched. Parameters:

  - type: (character) a mime type to match against; see
    [mime::mimemap](https://rdrr.io/pkg/mime/man/mimemap.html) for
    allowed values

  - charset: (character) if a charset string given, we check that it
    matches the charset in the content type header. default: NULL

  - behavior: (character) one of stop (default) or warning

- `raise_for_ct_html(charset = NULL, behavior = "stop")`:

  Check that the response content-type is `text/html`; stop or warn if
  not matched. Parameters: see `raise_for_ct()`

- `raise_for_ct_json(charset = NULL, behavior = "stop")`:

  Check that the response content-type is `application/json`; stop or
  warn if not matched. Parameters: see `raise_for_ct()`

- `raise_for_ct_xml(charset = NULL, behavior = "stop")`:

  Check that the response content-type is `application/xml`; stop or
  warn if not matched. Parameters: see `raise_for_ct()`

## R6 classes

This is an R6 class from the package R6. Find out more about R6 at
<https://r6.r-lib.org/>. After creating an instance of an R6 class
(e.g., `x <- HttpClient$new(url = "https://hb.opencpu.org")`) you can
access values and methods on the object `x`.

## See also

[content-types](https://docs.ropensci.org/crul/reference/content-types.md)

## Public fields

- `method`:

  (character) one or more URLs

- `url`:

  (character) one or more URLs

- `opts`:

  (character) one or more URLs

- `handle`:

  (character) one or more URLs

- `status_code`:

  (character) one or more URLs

- `request_headers`:

  (character) one or more URLs

- `response_headers`:

  (character) one or more URLs

- `response_headers_all`:

  (character) one or more URLs

- `modified`:

  (character) one or more URLs

- `times`:

  (character) one or more URLs

- `content`:

  (character) one or more URLs

- `request`:

  (character) one or more URLs

- `raise_for_ct`:

  for ct method (general)

- `raise_for_ct_html`:

  for ct method (html)

- `raise_for_ct_json`:

  for ct method (json)

- `raise_for_ct_xml`:

  for ct method (xml)

## Methods

### Public methods

- [`HttpResponse$print()`](#method-HttpResponse-print)

- [`HttpResponse$new()`](#method-HttpResponse-new)

- [`HttpResponse$parse()`](#method-HttpResponse-parse)

- [`HttpResponse$success()`](#method-HttpResponse-success)

- [`HttpResponse$status_http()`](#method-HttpResponse-status_http)

- [`HttpResponse$raise_for_status()`](#method-HttpResponse-raise_for_status)

- [`HttpResponse$clone()`](#method-HttpResponse-clone)

------------------------------------------------------------------------

### Method [`print()`](https://rdrr.io/r/base/print.html)

print method for HttpResponse objects

#### Usage

    HttpResponse$print(x, ...)

#### Arguments

- `x`:

  self

- `...`:

  ignored

------------------------------------------------------------------------

### Method [`new()`](https://rdrr.io/r/methods/new.html)

Create a new HttpResponse object

#### Usage

    HttpResponse$new(
      method,
      url,
      opts,
      handle,
      status_code,
      request_headers,
      response_headers,
      response_headers_all,
      modified,
      times,
      content,
      request
    )

#### Arguments

- `method`:

  (character) HTTP method

- `url`:

  (character) A url, required

- `opts`:

  (list) curl options

- `handle`:

  A handle

- `status_code`:

  (integer) status code

- `request_headers`:

  (list) request headers, named list

- `response_headers`:

  (list) response headers, named list

- `response_headers_all`:

  (list) all response headers, including intermediate redirect headers,
  unnamed list of named lists

- `modified`:

  (character) modified date

- `times`:

  (vector) named vector

- `content`:

  (raw) raw binary content response

- `request`:

  request object, with all details

------------------------------------------------------------------------

### Method [`parse()`](https://rdrr.io/r/base/parse.html)

Parse the raw response content to text

#### Usage

    HttpResponse$parse(encoding = NULL, ...)

#### Arguments

- `encoding`:

  (character) A character string describing the current encoding. If
  left as `NULL`, we attempt to guess the encoding. Passed to `from`
  parameter in `iconv`

- `...`:

  additional parameters passed on to `iconv` (options: sub, mark,
  toRaw). See [`?iconv`](https://rdrr.io/r/base/iconv.html) for help

#### Returns

character string

------------------------------------------------------------------------

### Method `success()`

Was status code less than or equal to 201

#### Usage

    HttpResponse$success()

#### Returns

boolean

------------------------------------------------------------------------

### Method `status_http()`

Get HTTP status code, message, and explanation

#### Usage

    HttpResponse$status_http(verbose = FALSE)

#### Arguments

- `verbose`:

  (logical) whether to get verbose http status description, default:
  `FALSE`

#### Returns

object of class "http_code", a list with slots for status_code, message,
and explanation

------------------------------------------------------------------------

### Method `raise_for_status()`

Check HTTP status and stop with appropriate HTTP error code and message
if \>= 300. otherwise use httpcode. If you have `fauxpas` installed we
use that.

#### Usage

    HttpResponse$raise_for_status()

#### Returns

stop or warn with message

------------------------------------------------------------------------

### Method `clone()`

The objects of this class are cloneable with this method.

#### Usage

    HttpResponse$clone(deep = FALSE)

#### Arguments

- `deep`:

  Whether to make a deep clone.

## Examples

``` r
if (FALSE) { # \dontrun{
x <- HttpResponse$new(method = "get", url = "https://hb.opencpu.org")
x$url
x$method

x <- HttpClient$new(url = 'https://hb.opencpu.org')
(res <- x$get('get'))
res$request_headers
res$response_headers
res$parse()
res$status_code
res$status_http()
res$status_http()$status_code
res$status_http()$message
res$status_http()$explanation
res$success()

x <- HttpClient$new(url = 'https://hb.opencpu.org/status/404')
(res <- x$get())
# res$raise_for_status()

x <- HttpClient$new(url = 'https://hb.opencpu.org/status/414')
(res <- x$get())
# res$raise_for_status()
} # }
```
