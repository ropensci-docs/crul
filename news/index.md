# Changelog

## crul (development version)

## crul 1.6.0

CRAN release: 2025-07-23

#### NEW FEATURES

- generic mocking is now controlled in each HTTP client (`HttpClient`,
  `Async`, and `AsyncVaried`) via an initialization parameter
  `AsyncVaried` or through each HTTP class method (e.g., `get`, `post`
  on `HttpClient`, `Async`). mocking used to be tied to `webmockr` but
  now can be controlled independently
  ([\#184](https://github.com/ropensci/crul/issues/184))

#### DEPRECATED

- [`mock()`](https://docs.ropensci.org/crul/reference/mock.md) is
  deprecated, and will be removed in a future version. Mocking is now
  controlled by parameters within the various HTTP clients:
  `HttpClient`, `Async`, and `AsyncVaried`
  ([\#184](https://github.com/ropensci/crul/issues/184))

## crul 1.5.0

CRAN release: 2024-07-19

#### NEW FEATURES

- gains ability to mock (via `webmockr`) async requests via either
  `Async` and/or `AsyncVaried` (thanks
  [@keller-mark](https://github.com/keller-mark))
  ([\#180](https://github.com/ropensci/crul/issues/180))

#### INTERNAL

- reduce use of single letter variables within crul code to make code
  easier to understand
  ([\#181](https://github.com/ropensci/crul/issues/181))

## crul 1.4.2

CRAN release: 2024-04-09

#### DOCUMENTATION

- fix typos (thanks [@mdsumner](https://github.com/mdsumner) and
  [@espinielli](https://github.com/espinielli))
  ([\#173](https://github.com/ropensci/crul/issues/173))
  ([\#176](https://github.com/ropensci/crul/issues/176))
- change to `_PACKAGE` pattern for pkg level man file
  ([\#177](https://github.com/ropensci/crul/issues/177))

#### INTERNAL

- tweak to test helper base url setup
  ([\#178](https://github.com/ropensci/crul/issues/178))

## crul 1.4

#### ASYNC RETRIES

Via the two issues
([\#135](https://github.com/ropensci/crul/issues/135)) and
([\#159](https://github.com/ropensci/crul/issues/159)) `crul` now
supports http retries in: `Async`, `AsyncVaried`, `AsyncQueue`, and the
request builder class `HttpRequest`

## crul 1.3

CRAN release: 2022-09-03

#### BUG FIXES

- improved error message for `Async` when `urls` and `disk` vector
  lengths do not match (they must match)
  ([\#165](https://github.com/ropensci/crul/issues/165)) thanks
  [@shakraz](https://github.com/shakraz)

## crul 1.2

#### DOCUMENTATION

- fix example in `AsyncQueue` docs
  ([\#146](https://github.com/ropensci/crul/issues/146)) thanks
  [@johnbaums](https://github.com/johnbaums) !
- update `HttpClient` docs to state that it’s an R6 class, and give some
  details on what an R6 class is and links to more info
  ([\#155](https://github.com/ropensci/crul/issues/155))

#### NEW FEATURES

- `AsyncQueue` gains methods: `parse`, `status_code`, `status`,
  `content`, and `times`
  ([\#156](https://github.com/ropensci/crul/issues/156))
- `$responses()` method now returns an S3 class with an associated print
  method to prevent printing a lot of results to the screen; print
  method pritns a summary of results, and at most 10 results, just
  status code and url
  ([\#157](https://github.com/ropensci/crul/issues/157))

#### MINOR IMPROVEMENTS

- parsing response headers gains a check for whether encoding is valid,
  and if not tries to set Latin1 encoding, and if that doesn’t work,
  fails out with message
  ([\#163](https://github.com/ropensci/crul/issues/163))
  ([\#164](https://github.com/ropensci/crul/issues/164)) thanks
  [@FlukeAndFeather](https://github.com/FlukeAndFeather)

## crul 1.1

#### NEW FEATURES

- `Paginator` gains support for query parameter combination
  `page`/`per_page` to automatically paginate
  ([\#145](https://github.com/ropensci/crul/issues/145))

#### MINOR IMPROVEMENTS

- fix typo ([\#149](https://github.com/ropensci/crul/issues/149)) thanks
  [@dpprdan](https://github.com/dpprdan)
- Change to how numbers are handled in query parameters. We
  unfortunately hadn’t tested this package with large numbers, which
  were being converted to scientific notation with a certain number of
  digits before a decimal. Fixed handling of query parameters to avoid
  this problem. Fix for `Paginator` as well as for `HttpClient`
  ([\#151](https://github.com/ropensci/crul/issues/151))
  ([\#152](https://github.com/ropensci/crul/issues/152))
  ([\#153](https://github.com/ropensci/crul/issues/153)) thanks
  [@ateucher](https://github.com/ateucher)

#### BUG FIXES

- sometimes weird response headers are returned in an HTTP response that
  can not be easily parsed; `crul` would raise an error when this header
  parsing happens, but now we raise a warning instead
  ([\#150](https://github.com/ropensci/crul/issues/150))

## crul 1.0

#### ok related changes

- [`ok()`](https://docs.ropensci.org/crul/reference/ok.md) can now
  accept more than 1 status code so that you can check if the status of
  a url is within a set of status codes rather than equal to 1 status
  code ([\#124](https://github.com/ropensci/crul/issues/124))
- [`ok()`](https://docs.ropensci.org/crul/reference/ok.md) gains a
  parameter `verb` to use either head or get requests. in addition added
  more documentation
  ([\#125](https://github.com/ropensci/crul/issues/125)) to the function
  on how to get the “right answer” for whether a url is ok/up
  ([\#123](https://github.com/ropensci/crul/issues/123))
  ([\#127](https://github.com/ropensci/crul/issues/127))
- [`ok()`](https://docs.ropensci.org/crul/reference/ok.md) gains
  parameter `ua_random`, which if `TRUE`, will use a random user agent
  string pulled from a vector of 50 user agent strings generated from
  `charlatan::UserAgentProvider`
  ([\#138](https://github.com/ropensci/crul/issues/138))

#### NEW FEATURES

- gains new async class `AsyncQueue` for doing async requests with rate
  limits ([\#139](https://github.com/ropensci/crul/issues/139))
- gains new functions
  [`curl_verbose()`](https://docs.ropensci.org/crul/reference/curl_verbose.md)
  and
  [`set_verbose()`](https://docs.ropensci.org/crul/reference/crul-options.md).
  [`curl_verbose()`](https://docs.ropensci.org/crul/reference/curl_verbose.md)
  can be set by passing to the initialize step (e.g.,
  `HttpClient$new(url, verbose=curl_verbose())`), and gets more compact
  verbose curl output, while also getting request body information (and
  response body optionally).
  [`set_verbose()`](https://docs.ropensci.org/crul/reference/crul-options.md)
  is sets
  [`curl_verbose()`](https://docs.ropensci.org/crul/reference/curl_verbose.md)
  globally ([\#141](https://github.com/ropensci/crul/issues/141))
- gains new vignette “How to choose a client” for choosing which crul
  class to use (e.g., `HttpClient` vs. `Async`)
  ([\#133](https://github.com/ropensci/crul/issues/133))
  ([\#143](https://github.com/ropensci/crul/issues/143))

#### MINOR IMPROVEMENTS

- package sticker done, shown in README
  ([\#42](https://github.com/ropensci/crul/issues/42))
- improve function/class reference page in docs site
  ([\#131](https://github.com/ropensci/crul/issues/131))
- improvements to the best practices vignette
  ([\#132](https://github.com/ropensci/crul/issues/132))
- removed unused private variable in the `AsyncVaried` class
  ([\#140](https://github.com/ropensci/crul/issues/140))
- fix inaccuracy in documentation for the RETRY method
  ([\#130](https://github.com/ropensci/crul/issues/130))
- `HttpRequest` now adds the query (if present) to the printed url in
  the print method for the class (it was absent before now)
  ([\#128](https://github.com/ropensci/crul/issues/128))
- use new roxygen2 support for R6 classes
  ([\#126](https://github.com/ropensci/crul/issues/126))
- removed `delete-requests` and `post-requests` manual files - mostly
  redundant with other documentation

## crul 0.9.0

CRAN release: 2019-11-06

#### NEW FEATURES

- `HttpResponse` response object gains new methods for checking response
  content types, includes: `raise_for_ct`, `raise_for_ct_html`,
  `raise_for_ct_json`, `raise_for_ct_xml`. these behave similarly to
  `raise_for_status`, and can behave as a warning or raise an error
  through stop ([\#119](https://github.com/ropensci/crul/issues/119))
  ([\#120](https://github.com/ropensci/crul/issues/120))

#### MINOR IMPROVEMENTS

- fix to prep_body internal function to handle various body inputs; now
  avoids warning about `as.character.form_file` when both httr and crul
  are loaded ([\#112](https://github.com/ropensci/crul/issues/112))
- finish off “Failing with fauxpas” section of the “API package best
  practices” vignette
  ([\#121](https://github.com/ropensci/crul/issues/121))

#### BUG FIXES

- the [`head()`](https://rdrr.io/r/utils/head.html) verb on `HttpClient`
  was no capturing `auth` when set on initialization
  ([\#122](https://github.com/ropensci/crul/issues/122))

## crul 0.8.4

CRAN release: 2019-08-02

#### MINOR IMPROVEMENTS

- `jsonlite` package moved to Imports
  ([\#112](https://github.com/ropensci/crul/issues/112))
- the [`parse()`](https://rdrr.io/r/base/parse.html) method in the
  `HttpResponse` object now checks whether the response raw bytes can be
  converted to character, and if not just returns raw bytes
  ([\#115](https://github.com/ropensci/crul/issues/115))
  ([\#116](https://github.com/ropensci/crul/issues/116))
- give vignettes titles
  ([\#113](https://github.com/ropensci/crul/issues/113))
  ([\#114](https://github.com/ropensci/crul/issues/114))

#### BUG FIXES

- no longer setting `cainfo` curl option, fixes problem arising from
  change in recent libcurl version
  ([\#117](https://github.com/ropensci/crul/issues/117))

## crul 0.8.0

CRAN release: 2019-06-28

#### NEW FEATURES

- you can now pass on parameters through the
  [`parse()`](https://rdrr.io/r/base/parse.html) method of an
  `HttpResponse` class to the internally called function
  [`iconv()`](https://rdrr.io/r/base/iconv.html) to finely control the
  usage of `iconv` for cases in which normal encoding conversion doesn’t
  work ([\#110](https://github.com/ropensci/crul/issues/110))

#### MINOR IMPROVEMENTS

- use `httpcode` package instead of `fauxpas` package within
  [`ok()`](https://docs.ropensci.org/crul/reference/ok.md) function
  ([\#108](https://github.com/ropensci/crul/issues/108))
  ([\#109](https://github.com/ropensci/crul/issues/109)) thanks
  [@maelle](https://github.com/maelle) !
- fix links to http testing book - ropensci -\> ropenscilabs
  ([\#111](https://github.com/ropensci/crul/issues/111))

## crul 0.7.4

CRAN release: 2019-03-28

#### NEW FEATURES

- event hooks added to `HttpClient`. both request and response hooks
  supported. not supported in async methods for now
  ([\#76](https://github.com/ropensci/crul/issues/76))
  ([\#107](https://github.com/ropensci/crul/issues/107))

#### MINOR IMPROVEMENTS

- improve `$parse()` behavior (in the `HttpResponse` object) when using
  disk or stream. `$parse()` was throwing a warning when using disk and
  an error when using stream. and improves behavior when doing async
  requests ([\#104](https://github.com/ropensci/crul/issues/104))
- `Paginator` gains optional progress bar through the new `progress`
  parameter. In addition, the [`cat()`](https://rdrr.io/r/base/cat.html)
  calls inside the method were removed, so as not to insert newlines
  with each page and to not print “OK” when done
  ([\#106](https://github.com/ropensci/crul/issues/106)) thanks
  [@boshek](https://github.com/boshek)

#### BUG FIXES

- passing on opts/headers now works with `Async`
  ([\#101](https://github.com/ropensci/crul/issues/101))
  ([\#103](https://github.com/ropensci/crul/issues/103))
- streaming was broken in `AsyncVaried` with `curl` of a certain
  version, works now
  ([\#102](https://github.com/ropensci/crul/issues/102))
  ([\#103](https://github.com/ropensci/crul/issues/103))

## crul 0.7.0

CRAN release: 2019-01-04

#### NEW FEATURES

- `HttpClient` gains a `retry` method: retries any request verb until
  successful (HTTP response status \< 400) or a condition for giving up
  is met. ([\#89](https://github.com/ropensci/crul/issues/89))
  ([\#95](https://github.com/ropensci/crul/issues/95)) thanks
  [@hlapp](https://github.com/hlapp)
- `HttpClient`, `HttpRequest`, and `Async` classes gain `verb` method
  for doing HTTP requests specifying any of the supported HTTP verbs
  ([\#97](https://github.com/ropensci/crul/issues/97))
- `HttpClient` and `Paginator` gain a `url_fetch` method: get the URL
  that would be sent in an HTTP request without sending the HTTP
  request. Useful for getting the URL before executing an HTTP request
  if you need to check something about the URL first.
  ([\#92](https://github.com/ropensci/crul/issues/92))
- new vignette for “API package best practices”
  ([\#65](https://github.com/ropensci/crul/issues/65))
- Package gains manual files for each HTTP verb to facilitate linking to
  package documentation for information on each HTTP verb
  ([\#98](https://github.com/ropensci/crul/issues/98))
- Intermediate headers (e.g., those in redirect chains) are now given
  back in a new slot in the `HttpResponse` class as
  `$response_headers_all` as an unnamed list, with each element a named
  list of headers; the last list in the set is the final response
  headers that match those given in the `$response_headers` slot
  ([\#60](https://github.com/ropensci/crul/issues/60))
  ([\#99](https://github.com/ropensci/crul/issues/99))

#### BUG FIXES

- some dangling file connections were left open - now fixed
  ([\#93](https://github.com/ropensci/crul/issues/93))
  ([\#95](https://github.com/ropensci/crul/issues/95))
- fix `url_parse`: lacked check that input was a string, and that it was
  length 1 - this PR fixed that
  ([\#100](https://github.com/ropensci/crul/issues/100)) thanks
  [@aaronwolen](https://github.com/aaronwolen)

#### DEFUNCT

- `HttpStubbedResponse` was removed from the package - it may have been
  used at some point, but is not used in the package anymore
  ([\#88](https://github.com/ropensci/crul/issues/88))

## crul 0.6.0

CRAN release: 2018-07-10

#### NEW FEATURES

- `Async` and `AsyncVaried` now support simple auth, see
  [`?auth`](https://docs.ropensci.org/crul/reference/auth.md)
  ([\#70](https://github.com/ropensci/crul/issues/70))
- gains new function
  [`ok()`](https://docs.ropensci.org/crul/reference/ok.md) to ping a URL
  to see if it’s up or not, returns a single boolean
  ([\#71](https://github.com/ropensci/crul/issues/71))
  ([\#73](https://github.com/ropensci/crul/issues/73))
- `HttpClient` and `HttpRequest` gain new parameter `progress` that
  accepts a function to use to construct a progress bar. For now accepts
  `httr::progress()` but will accept other options in the future
  ([\#20](https://github.com/ropensci/crul/issues/20))
  ([\#81](https://github.com/ropensci/crul/issues/81))
- gains a new vignette for curl options
  ([\#7](https://github.com/ropensci/crul/issues/7))
- can now set curl options globally using new functions
  [`set_auth()`](https://docs.ropensci.org/crul/reference/crul-options.md),
  [`set_headers()`](https://docs.ropensci.org/crul/reference/crul-options.md),
  [`set_opts()`](https://docs.ropensci.org/crul/reference/crul-options.md),
  [`set_proxy()`](https://docs.ropensci.org/crul/reference/crul-options.md),
  and
  [`crul_settings()`](https://docs.ropensci.org/crul/reference/crul-options.md)
  ([\#48](https://github.com/ropensci/crul/issues/48))
  ([\#85](https://github.com/ropensci/crul/issues/85))

#### MINOR IMPROVEMENTS

- explicitly import
  [`httpcode::http_code`](https://rdrr.io/pkg/httpcode/man/http.html)
  ([\#80](https://github.com/ropensci/crul/issues/80))
- fix vignette names to make them more clear and add numbers to order
  them ([\#64](https://github.com/ropensci/crul/issues/64))
- change print function for `Async` and `AsyncVaried` to print max of 10
  and tell user how many total and remaining not shown
  ([\#72](https://github.com/ropensci/crul/issues/72))
- added support to
  [`proxy()`](https://docs.ropensci.org/crul/reference/proxies.md) for
  socks, e.g. to use with TOR
  ([\#79](https://github.com/ropensci/crul/issues/79))
- now when `Async` and `AsyncVaried` requests fail, they don’t error but
  instead we capture the error and pass it back in the result. this way
  any failure requests don’t stop progress of the entire async request
  suite ([\#74](https://github.com/ropensci/crul/issues/74))
  ([\#84](https://github.com/ropensci/crul/issues/84))

## crul 0.5.2

CRAN release: 2018-02-24

#### MINOR IMPROVEMENTS

- Fixed handling of user agent: you can pass a UA string as a curl
  option or a header. Previously, we were wrongly overwriting the user
  input UA if given as a curl option - but were not doing so if given as
  a header. This is fixed now.
  ([\#63](https://github.com/ropensci/crul/issues/63)) thx to
  [@maelle](https://github.com/maelle) and
  [@dpprdan](https://github.com/dpprdan)

#### BUG FIXES

- Fix to `Paginator` - it wasn’t handling pagination correctly. In
  addition, fixed to hopefully handle all scenarios now. added more
  tests ([\#62](https://github.com/ropensci/crul/issues/62))
- Fixed handling of query parameters. We were using
  [`urltools::url_encode`](https://rdrr.io/pkg/urltools/man/encoder.html)
  to encode strings, but it wasn’t encoding correctly in some locales.
  Using
  [`curl::curl_escape`](https://jeroen.r-universe.dev/curl/reference/curl_escape.html)
  fixes the problem. Encoding is done on query values and names
  ([\#67](https://github.com/ropensci/crul/issues/67))
  ([\#68](https://github.com/ropensci/crul/issues/68))

## crul 0.5.0

CRAN release: 2018-01-22

#### NEW FEATURES

- Gains a new R6 class `Paginator` to help users automatically paginate
  through multiple requests. It only supports query parameter based
  paginating for now. We’ll add support later for other types including
  cursors (e.g., used in Solr servers), and for link headers (e.g., used
  in the GitHub API). Please get in touch if you find any problems with
  `Paginator`. ([\#56](https://github.com/ropensci/crul/issues/56))
- Async classes `Async` and `Asyncvaried` gain ability to write to disk
  and stream data (to disk or elsewhere, e.g. R console or to an R
  object) ([\#46](https://github.com/ropensci/crul/issues/46)) thanks
  [@artemklevtsov](https://github.com/artemklevtsov) for the push to do
  this

#### MINOR IMPROVEMENTS

- Improved documentation for `auth` to indicate that `user` and `pwd`
  are indeed required - and to further indicate that one can pass in
  `NULL` to those parameters (similar to an empty string `""` in
  `httr::authenticate`) when one e.g. may want to use `gssnegotiate`
  method ([\#43](https://github.com/ropensci/crul/issues/43))
- Fixed query builder so that one can now protect query parameters by
  wrapping them in [`I()`](https://rdrr.io/r/base/AsIs.html)
  ([\#55](https://github.com/ropensci/crul/issues/55))

#### BUG FIXES

- Fixed bug in `head` requests with `HttpClient` when passing `query`
  parameter - it was failing previously. Added `query` parameter back.
  ([\#52](https://github.com/ropensci/crul/issues/52))

## crul 0.4.0

CRAN release: 2017-10-02

#### NEW FEATURES

- file uploads now work, see new function
  [`upload()`](https://docs.ropensci.org/crul/reference/upload.md) and
  examples ([\#25](https://github.com/ropensci/crul/issues/25))

#### MINOR IMPROVEMENTS

- fixes to reused curl handles - within a connection object only, not
  across connection objects
  ([\#45](https://github.com/ropensci/crul/issues/45))
- `crul` now drops any options passed in to `opts` or to `...` that are
  not in set of allowed curl options, see
  [`curl::curl_options()`](https://jeroen.r-universe.dev/curl/reference/curl_options.html)
  ([\#49](https://github.com/ropensci/crul/issues/49))
- cookies should now be persisted across requests within a connection
  object, see new doc
  [`?cookies`](https://docs.ropensci.org/crul/reference/cookies.md) for
  how to set cookies
  ([\#44](https://github.com/ropensci/crul/issues/44))
- gather cainfo and use in curl options when applicable
  ([\#51](https://github.com/ropensci/crul/issues/51))
- remove `disk` and `stream` from `head` method in `HttpClient` and
  `HttpRequest` as no body returned in a HEAD request

## crul 0.3.8

CRAN release: 2017-06-14

#### BUG FIXES

- Fixed `AsyncVaried` to return async responses in the order that they
  were passed in. This also fixes this exact same behavior in `Async`
  because `Async` uses `AsyncVaried` internally.
  ([\#41](https://github.com/ropensci/crul/issues/41)) thanks
  [@dirkschumacher](https://github.com/dirkschumacher) for reporting

## crul 0.3.6

CRAN release: 2017-05-23

- Note: This version gains support for integration with `webmockr`,
  which is now on CRAN.

#### NEW FEATURES

- New function
  [`auth()`](https://docs.ropensci.org/crul/reference/auth.md) to do
  simple authentication
  ([\#33](https://github.com/ropensci/crul/issues/33))
- New function `HttpStubbedResponse` for making a stubbed response
  object for the `webmockr` integration
  ([\#4](https://github.com/ropensci/crul/issues/4))
- New function
  [`mock()`](https://docs.ropensci.org/crul/reference/mock.md) to turn
  on mocking - it’s off by default. If `webmockr` is not installed but
  user attempts to use mocking we error with message to install
  `webmockr` ([\#4](https://github.com/ropensci/crul/issues/4))

#### MINOR IMPROVEMENTS

- Use `gzip-deflate` by deafult for each request to make sure gzip
  compression is used if the server can do it
  ([\#34](https://github.com/ropensci/crul/issues/34))
- Change `useragent` to `User-Agent` as default user agent header
  ([\#35](https://github.com/ropensci/crul/issues/35))
- Now we make sure that user supplied headers override the default
  headers if they are of the same name
  ([\#36](https://github.com/ropensci/crul/issues/36))

## crul 0.3.4

CRAN release: 2017-03-31

#### NEW FEATURES

- New utility functions `url_build` and `url_parse`
  ([\#31](https://github.com/ropensci/crul/issues/31))

#### MINOR IMPROVEMENTS

- Now using markdown for documentation
  ([\#32](https://github.com/ropensci/crul/issues/32))
- Better documentation for `AsyncVaried`
  ([\#30](https://github.com/ropensci/crul/issues/30))
- New vignette on how to use `crul` in realistic scenarios rather than
  brief examples to demonstrate individual features
  ([\#29](https://github.com/ropensci/crul/issues/29))
- Better documentation for `HttpRequest`
  ([\#28](https://github.com/ropensci/crul/issues/28))
- Included more tests

#### BUG FIXES

- Fixed put/patch/delete as weren’t passing body correctly in
  `HttpClient` ([\#26](https://github.com/ropensci/crul/issues/26))
- DRY out code for preparing requests - simplify to use helper functions
  ([\#27](https://github.com/ropensci/crul/issues/27))

## crul 0.3.0

CRAN release: 2017-02-17

#### NEW FEATURES

- Added support for asynchronous HTTP requests, including two new R6
  classes: `Async` and `AsyncVaried`. The former being a simpler
  interface treating all URLs with same options/HTTP method, and the
  latter allowing any type of request through the new R6 class
  `HttpRequest` ([\#8](https://github.com/ropensci/crul/issues/8))
  ([\#24](https://github.com/ropensci/crul/issues/24))
- New R6 class `HttpRequest` to support `AsyncVaried` - this method only
  defines a request, but does not execute it.
  ([\#8](https://github.com/ropensci/crul/issues/8))

#### MINOR IMPROVEMENTS

- Added support for proxies
  ([\#22](https://github.com/ropensci/crul/issues/22))

#### BUG FIXES

- Fixed parsing of headers from FTP servers
  ([\#21](https://github.com/ropensci/crul/issues/21))

## crul 0.2.0

CRAN release: 2017-01-03

#### MINOR IMPROVEMENTS

- Created new manual files for various tasks to document usage better
  ([\#19](https://github.com/ropensci/crul/issues/19))
- URL encode paths - should fix any bugs where spaces between words
  caused errors previously
  ([\#17](https://github.com/ropensci/crul/issues/17))
- URL encode query parameters - should fix any bugs where spaces between
  words caused errors previously
  ([\#11](https://github.com/ropensci/crul/issues/11))
- request headers now passed correctly to response object
  ([\#13](https://github.com/ropensci/crul/issues/13))
- response headers now parsed to a list for easier access
  ([\#14](https://github.com/ropensci/crul/issues/14))
- Now supporting multiple query parameters of the same name, wasn’t
  possible in last version
  ([\#15](https://github.com/ropensci/crul/issues/15))

## crul 0.1.6

CRAN release: 2016-12-17

#### NEW FEATURES

- Improved options for using curl options. Can manually add to list of
  curl options or pass in via `...`. And we check that user doesn’t pass
  in prohibited options (`curl` package takes care of checking that
  options are valid) ([\#5](https://github.com/ropensci/crul/issues/5))
- Incorporated `fauxpas` package for dealing with HTTP conditions. It’s
  a Suggest, so only used if installed
  ([\#6](https://github.com/ropensci/crul/issues/6))
- Added support for streaming via
  [`curl::curl_fetch_stream`](https://jeroen.r-universe.dev/curl/reference/curl_fetch.html).
  `stream` param defaults to `NULL` (thus ignored), or pass in a
  function to use streaming. Only one of memory, streaming or disk
  allowed. ([\#9](https://github.com/ropensci/crul/issues/9))
- Added support for streaming via
  [`curl::curl_fetch_disk`](https://jeroen.r-universe.dev/curl/reference/curl_fetch.html).
  `disk` param defaults to `NULL` (thus ignored), or pass in a path to
  write to disk instead of use memory. Only one of memory, streaming or
  disk allowed. ([\#12](https://github.com/ropensci/crul/issues/12))

#### MINOR IMPROVEMENTS

- Added missing `raise_for_status()` method on the `HttpResponse` class
  ([\#10](https://github.com/ropensci/crul/issues/10))

#### BUG FIXES

- Was importing `httpcode` but wasn’t using it in the package. Now using
  the package in `HttpResponse`

## crul 0.1.0

CRAN release: 2016-11-09

#### NEW FEATURES

- Released to CRAN.
