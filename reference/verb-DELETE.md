# HTTP verb info: DELETE

The DELETE method deletes the specified resource.

## The DELETE method

The DELETE method requests that the origin server remove the association
between the target resource and its current functionality. In effect,
this method is similar to the rm command in UNIX: it expresses a
deletion operation on the URI mapping of the origin server rather than
an expectation that the previously associated information be deleted.

## References

<https://datatracker.ietf.org/doc/html/rfc7231#section-4.3.5>

## See also

[crul-package](https://docs.ropensci.org/crul/reference/crul-package.md)

Other verbs:
[`verb-GET`](https://docs.ropensci.org/crul/reference/verb-GET.md),
[`verb-HEAD`](https://docs.ropensci.org/crul/reference/verb-HEAD.md),
[`verb-PATCH`](https://docs.ropensci.org/crul/reference/verb-PATCH.md),
[`verb-POST`](https://docs.ropensci.org/crul/reference/verb-POST.md),
[`verb-PUT`](https://docs.ropensci.org/crul/reference/verb-PUT.md)

## Examples

``` r
if (FALSE) { # \dontrun{
x <- HttpClient$new(url = "https://hb.opencpu.org")
x$delete(path = 'delete')

## a list
(res1 <- x$delete('delete', body = list(hello = "world"), verbose = TRUE))
jsonlite::fromJSON(res1$parse("UTF-8"))

## a string
(res2 <- x$delete('delete', body = "hello world", verbose = TRUE))
jsonlite::fromJSON(res2$parse("UTF-8"))

## empty body request
x$delete('delete', verbose = TRUE)
} # }
```
