# HTTP verb info: HEAD

The HEAD method asks for a response identical to that of a GET request,
but without the response body.

## The HEAD method

The HEAD method is identical to GET except that the server MUST NOT send
a message body in the response (i.e., the response terminates at the end
of the header section). The server SHOULD send the same header fields in
response to a HEAD request as it would have sent if the request had been
a GET, except that the payload header fields MAY be omitted. This method
can be used for obtaining metadata about the selected representation
without transferring the representation data and is often used for
testing hypertext links for validity, accessibility, and recent
modification.

## References

<https://datatracker.ietf.org/doc/html/rfc7231#section-4.3.2>

## See also

[crul-package](https://docs.ropensci.org/crul/reference/crul-package.md)

Other verbs:
[`verb-DELETE`](https://docs.ropensci.org/crul/reference/verb-DELETE.md),
[`verb-GET`](https://docs.ropensci.org/crul/reference/verb-GET.md),
[`verb-PATCH`](https://docs.ropensci.org/crul/reference/verb-PATCH.md),
[`verb-POST`](https://docs.ropensci.org/crul/reference/verb-POST.md),
[`verb-PUT`](https://docs.ropensci.org/crul/reference/verb-PUT.md)

## Examples

``` r
if (FALSE) { # \dontrun{
x <- HttpClient$new(url = "https://hb.opencpu.org")
x$head()
} # }
```
