# Paginator client

A client to help you paginate

## Value

a list, with objects of class
[`HttpResponse()`](https://docs.ropensci.org/crul/reference/HttpResponse.md).
Responses are returned in the order they are passed in.

## Details

See
[`HttpClient()`](https://docs.ropensci.org/crul/reference/HttpClient.md)
for information on parameters

## R6 classes

This is an R6 class from the package R6. Find out more about R6 at
<https://r6.r-lib.org/>. After creating an instance of an R6 class
(e.g., `x <- HttpClient$new(url = "https://hb.opencpu.org")`) you can
access values and methods on the object `x`.

## Methods to paginate

Supported now:

- `limit_offset`: the most common way (in my experience), so is the
  default. This method involves setting how many records and what record
  to start at for each request. We send these query parameters for you.

- `page_perpage`: set the page to fetch and (optionally) how many
  records to get per page

Supported later, hopefully:

- `link_headers`: link headers are URLS for the next/previous/last
  request given in the response header from the server. This is
  relatively uncommon, though is recommended by JSONAPI and is
  implemented by a well known API (GitHub).

- `cursor`: this works by a single string given back in each response,
  to be passed in the subsequent response, and so on until no more
  records remain. This is common in Solr

## Public fields

- `http_req`:

  an object of class `HttpClient`

- `by`:

  (character) how to paginate. Only 'limit_offset' supported for now. In
  the future will support 'link_headers' and 'cursor'. See Details.

- `chunk`:

  (numeric/integer) the number by which to chunk requests, e.g., 10
  would be be each request gets 10 records. number is passed through
  [`format()`](https://rdrr.io/r/base/format.html) to prevent larger
  numbers from being scientifically formatted

- `limit_param`:

  (character) the name of the limit parameter. Default: limit

- `offset_param`:

  (character) the name of the offset parameter. Default: offset

- `limit`:

  (numeric/integer) the maximum records wanted. number is passed through
  [`format()`](https://rdrr.io/r/base/format.html) to prevent larger
  numbers from being scientifically formatted

- `page_param`:

  (character) the name of the page parameter. Default: NULL

- `per_page_param`:

  (character) the name of the per page parameter. Default: NULL

- `progress`:

  (logical) print a progress bar, using
  [utils::txtProgressBar](https://rdrr.io/r/utils/txtProgressBar.html).
  Default: `FALSE`.

## Methods

### Public methods

- [`Paginator$print()`](#method-Paginator-print)

- [`Paginator$new()`](#method-Paginator-new)

- [`Paginator$get()`](#method-Paginator-get)

- [`Paginator$post()`](#method-Paginator-post)

- [`Paginator$put()`](#method-Paginator-put)

- [`Paginator$patch()`](#method-Paginator-patch)

- [`Paginator$delete()`](#method-Paginator-delete)

- [`Paginator$head()`](#method-Paginator-head)

- [`Paginator$responses()`](#method-Paginator-responses)

- [`Paginator$status_code()`](#method-Paginator-status_code)

- [`Paginator$status()`](#method-Paginator-status)

- [`Paginator$parse()`](#method-Paginator-parse)

- [`Paginator$content()`](#method-Paginator-content)

- [`Paginator$times()`](#method-Paginator-times)

- [`Paginator$url_fetch()`](#method-Paginator-url_fetch)

- [`Paginator$clone()`](#method-Paginator-clone)

------------------------------------------------------------------------

### Method [`print()`](https://rdrr.io/r/base/print.html)

print method for `Paginator` objects

#### Usage

    Paginator$print(x, ...)

#### Arguments

- `x`:

  self

- `...`:

  ignored

------------------------------------------------------------------------

### Method [`new()`](https://rdrr.io/r/methods/new.html)

Create a new `Paginator` object

#### Usage

    Paginator$new(
      client,
      by = "limit_offset",
      limit_param = NULL,
      offset_param = NULL,
      limit = NULL,
      chunk = NULL,
      page_param = NULL,
      per_page_param = NULL,
      progress = FALSE
    )

#### Arguments

- `client`:

  an object of class `HttpClient`, from a call to
  [HttpClient](https://docs.ropensci.org/crul/reference/HttpClient.md)

- `by`:

  (character) how to paginate. Only 'limit_offset' supported for now. In
  the future will support 'link_headers' and 'cursor'. See Details.

- `limit_param`:

  (character) the name of the limit parameter. Default: limit

- `offset_param`:

  (character) the name of the offset parameter. Default: offset

- `limit`:

  (numeric/integer) the maximum records wanted

- `chunk`:

  (numeric/integer) the number by which to chunk requests, e.g., 10
  would be be each request gets 10 records

- `page_param`:

  (character) the name of the page parameter.

- `per_page_param`:

  (character) the name of the per page parameter.

- `progress`:

  (logical) print a progress bar, using
  [utils::txtProgressBar](https://rdrr.io/r/utils/txtProgressBar.html).
  Default: `FALSE`.

#### Returns

A new `Paginator` object

------------------------------------------------------------------------

### Method [`get()`](https://rdrr.io/r/base/get.html)

make a paginated GET request

#### Usage

    Paginator$get(path = NULL, query = list(), ...)

#### Arguments

- `path`:

  URL path, appended to the base URL

- `query`:

  query terms, as a named list. any numeric values are passed through
  [`format()`](https://rdrr.io/r/base/format.html) to prevent larger
  numbers from being scientifically formatted

- `...`:

  For `retry`, the options to be passed on to the method implementing
  the requested verb, including curl options. Otherwise, curl options,
  only those in the acceptable set from
  [`curl::curl_options()`](https://jeroen.r-universe.dev/curl/reference/curl_options.html)
  except the following: httpget, httppost, post, postfields,
  postfieldsize, and customrequest

------------------------------------------------------------------------

### Method `post()`

make a paginated POST request

#### Usage

    Paginator$post(
      path = NULL,
      query = list(),
      body = NULL,
      encode = "multipart",
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

- `encode`:

  one of form, multipart, json, or raw

- `...`:

  For `retry`, the options to be passed on to the method implementing
  the requested verb, including curl options. Otherwise, curl options,
  only those in the acceptable set from
  [`curl::curl_options()`](https://jeroen.r-universe.dev/curl/reference/curl_options.html)
  except the following: httpget, httppost, post, postfields,
  postfieldsize, and customrequest

------------------------------------------------------------------------

### Method `put()`

make a paginated PUT request

#### Usage

    Paginator$put(
      path = NULL,
      query = list(),
      body = NULL,
      encode = "multipart",
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

- `encode`:

  one of form, multipart, json, or raw

- `...`:

  For `retry`, the options to be passed on to the method implementing
  the requested verb, including curl options. Otherwise, curl options,
  only those in the acceptable set from
  [`curl::curl_options()`](https://jeroen.r-universe.dev/curl/reference/curl_options.html)
  except the following: httpget, httppost, post, postfields,
  postfieldsize, and customrequest

------------------------------------------------------------------------

### Method `patch()`

make a paginated PATCH request

#### Usage

    Paginator$patch(
      path = NULL,
      query = list(),
      body = NULL,
      encode = "multipart",
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

- `encode`:

  one of form, multipart, json, or raw

- `...`:

  For `retry`, the options to be passed on to the method implementing
  the requested verb, including curl options. Otherwise, curl options,
  only those in the acceptable set from
  [`curl::curl_options()`](https://jeroen.r-universe.dev/curl/reference/curl_options.html)
  except the following: httpget, httppost, post, postfields,
  postfieldsize, and customrequest

------------------------------------------------------------------------

### Method `delete()`

make a paginated DELETE request

#### Usage

    Paginator$delete(
      path = NULL,
      query = list(),
      body = NULL,
      encode = "multipart",
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

- `encode`:

  one of form, multipart, json, or raw

- `...`:

  For `retry`, the options to be passed on to the method implementing
  the requested verb, including curl options. Otherwise, curl options,
  only those in the acceptable set from
  [`curl::curl_options()`](https://jeroen.r-universe.dev/curl/reference/curl_options.html)
  except the following: httpget, httppost, post, postfields,
  postfieldsize, and customrequest

------------------------------------------------------------------------

### Method [`head()`](https://rdrr.io/r/utils/head.html)

make a paginated HEAD request

#### Usage

    Paginator$head(path = NULL, ...)

#### Arguments

- `path`:

  URL path, appended to the base URL

- `...`:

  For `retry`, the options to be passed on to the method implementing
  the requested verb, including curl options. Otherwise, curl options,
  only those in the acceptable set from
  [`curl::curl_options()`](https://jeroen.r-universe.dev/curl/reference/curl_options.html)
  except the following: httpget, httppost, post, postfields,
  postfieldsize, and customrequest

#### Details

not sure if this makes any sense or not yet

------------------------------------------------------------------------

### Method `responses()`

list responses

#### Usage

    Paginator$responses()

#### Returns

a list of `HttpResponse` objects, empty list before requests made

------------------------------------------------------------------------

### Method `status_code()`

Get HTTP status codes for each response

#### Usage

    Paginator$status_code()

#### Returns

numeric vector, empty numeric vector before requests made

------------------------------------------------------------------------

### Method `status()`

List HTTP status objects

#### Usage

    Paginator$status()

#### Returns

a list of `http_code` objects, empty list before requests made

------------------------------------------------------------------------

### Method [`parse()`](https://rdrr.io/r/base/parse.html)

parse content

#### Usage

    Paginator$parse(encoding = "UTF-8")

#### Arguments

- `encoding`:

  (character) the encoding to use in parsing. default:"UTF-8"

#### Returns

character vector, empty character vector before requests made

------------------------------------------------------------------------

### Method `content()`

Get raw content for each response

#### Usage

    Paginator$content()

#### Returns

raw list, empty list before requests made

------------------------------------------------------------------------

### Method `times()`

curl request times

#### Usage

    Paginator$times()

#### Returns

list of named numeric vectors, empty list before requests made

------------------------------------------------------------------------

### Method `url_fetch()`

get the URL that would be sent (i.e., before executing the request) the
only things that change the URL are path and query parameters; body and
any curl options don't change the URL

#### Usage

    Paginator$url_fetch(path = NULL, query = list())

#### Arguments

- `path`:

  URL path, appended to the base URL

- `query`:

  query terms, as a named list. any numeric values are passed through
  [`format()`](https://rdrr.io/r/base/format.html) to prevent larger
  numbers from being scientifically formatted

#### Returns

URLs (character)

#### Examples

    \dontrun{
    cli <- HttpClient$new(url = "https://api.crossref.org")
    cc <- Paginator$new(client = cli, limit_param = "rows",
       offset_param = "offset", limit = 50, chunk = 10)
    cc$url_fetch('works')
    cc$url_fetch('works', query = list(query = "NSF"))
    }

------------------------------------------------------------------------

### Method `clone()`

The objects of this class are cloneable with this method.

#### Usage

    Paginator$clone(deep = FALSE)

#### Arguments

- `deep`:

  Whether to make a deep clone.

## Examples

``` r
if (FALSE) { # \dontrun{
if (interactive()) {
# limit/offset approach
con <- HttpClient$new(url = "https://api.crossref.org")
cc <- Paginator$new(client = con, limit_param = "rows",
   offset_param = "offset", limit = 50, chunk = 10)
cc
cc$get('works')
cc
cc$responses()
cc$status()
cc$status_code()
cc$times()
# cc$content()
cc$parse()
lapply(cc$parse(), jsonlite::fromJSON)

# page/per page approach (with no per_page param allowed)
conn <- HttpClient$new(url = "https://discuss.ropensci.org")
cc <- Paginator$new(client = conn, by = "page_perpage",
 page_param = "page", per_page_param = "per_page", limit = 90, chunk = 30)
cc
cc$get('c/usecases/l/latest.json')
cc$responses()
lapply(cc$parse(), jsonlite::fromJSON)

# page/per_page
conn <- HttpClient$new('https://api.inaturalist.org')
cc <- Paginator$new(conn, by = "page_perpage", page_param = "page",
 per_page_param = "per_page", limit = 90, chunk = 30)
cc
cc$get('v1/observations', query = list(taxon_name="Helianthus"))
cc$responses()
res <- lapply(cc$parse(), jsonlite::fromJSON)
res[[1]]$total_results
vapply(res, "[[", 1L, "page")
vapply(res, "[[", 1L, "per_page")
vapply(res, function(w) NROW(w$results), 1L)
## another
ccc <- Paginator$new(conn, by = "page_perpage", page_param = "page",
 per_page_param = "per_page", limit = 500, chunk = 30, progress = TRUE)
ccc
ccc$get('v1/observations', query = list(taxon_name="Helianthus"))
res2 <- lapply(ccc$parse(), jsonlite::fromJSON)
vapply(res2, function(w) NROW(w$results), 1L)

# progress bar
(con <- HttpClient$new(url = "https://api.crossref.org"))
cc <- Paginator$new(client = con, limit_param = "rows",
   offset_param = "offset", limit = 50, chunk = 10,
   progress = TRUE)
cc
cc$get('works')
}} # }

## ------------------------------------------------
## Method `Paginator$url_fetch`
## ------------------------------------------------

if (FALSE) { # \dontrun{
cli <- HttpClient$new(url = "https://api.crossref.org")
cc <- Paginator$new(client = cli, limit_param = "rows",
   offset_param = "offset", limit = 50, chunk = 10)
cc$url_fetch('works')
cc$url_fetch('works', query = list(query = "NSF"))
} # }
```
