# HTTP verb info: PATCH

The PATCH method is used to apply partial modifications to a resource.

## The PATCH method

The PATCH method requests that a set of changes described in the request
entity be applied to the resource identified by the Request- URI. The
set of changes is represented in a format called a "patch document"
identified by a media type. If the Request-URI does not point to an
existing resource, the server MAY create a new resource, depending on
the patch document type (whether it can logically modify a null
resource) and permissions, etc.

## References

<https://datatracker.ietf.org/doc/html/rfc5789>

## See also

[crul-package](https://docs.ropensci.org/crul/reference/crul-package.md)

Other verbs:
[`verb-DELETE`](https://docs.ropensci.org/crul/reference/verb-DELETE.md),
[`verb-GET`](https://docs.ropensci.org/crul/reference/verb-GET.md),
[`verb-HEAD`](https://docs.ropensci.org/crul/reference/verb-HEAD.md),
[`verb-POST`](https://docs.ropensci.org/crul/reference/verb-POST.md),
[`verb-PUT`](https://docs.ropensci.org/crul/reference/verb-PUT.md)

## Examples

``` r
if (FALSE) { # \dontrun{
x <- HttpClient$new(url = "https://hb.opencpu.org")
x$patch(path = 'patch', body = list(hello = "mars"))
} # }
```
