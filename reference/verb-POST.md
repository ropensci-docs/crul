# HTTP verb info: POST

The POST method is used to submit an entity to the specified resource,
often causing a change in state or side effects on the server.

## The POST method

If one or more resources has been created on the origin server as a
result of successfully processing a POST request, the origin server
SHOULD send a 201 (Created) response containing a Location header field
that provides an identifier for the primary resource created (Section
7.1.2 <https://datatracker.ietf.org/doc/html/rfc7231#section-7.1.2>) and
a representation that describes the status of the request while
referring to the new resource(s).

## References

<https://datatracker.ietf.org/doc/html/rfc7231#section-4.3.3>

## See also

[crul-package](https://docs.ropensci.org/crul/reference/crul-package.md)

Other verbs:
[`verb-DELETE`](https://docs.ropensci.org/crul/reference/verb-DELETE.md),
[`verb-GET`](https://docs.ropensci.org/crul/reference/verb-GET.md),
[`verb-HEAD`](https://docs.ropensci.org/crul/reference/verb-HEAD.md),
[`verb-PATCH`](https://docs.ropensci.org/crul/reference/verb-PATCH.md),
[`verb-PUT`](https://docs.ropensci.org/crul/reference/verb-PUT.md)

## Examples

``` r
if (FALSE) { # \dontrun{
x <- HttpClient$new(url = "https://hb.opencpu.org")

# a named list
x$post(path='post', body = list(hello = "world"))

# a string
x$post(path='post', body = "hello world")

# an empty body request
x$post(path='post')

# encode="form"
res <- x$post(path="post",
  encode = "form",
  body = list(
    custname = 'Jane',
    custtel = '444-4444',
    size = 'small',
    topping = 'bacon',
    comments = 'make it snappy'
  )
)
jsonlite::fromJSON(res$parse("UTF-8"))

# encode="json"
res <- x$post("post",
  encode = "json",
  body = list(
    genus = 'Gagea',
    species = 'pratensis'
  )
)
jsonlite::fromJSON(res$parse())
} # }
```
