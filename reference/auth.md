# Authentication

Authentication

## Usage

``` r
auth(user, pwd, auth = "basic")
```

## Arguments

- user:

  (character) username, required. see Details.

- pwd:

  (character) password, required. see Details.

- auth:

  (character) authentication type, one of basic (default), digest,
  digest_ie, gssnegotiate, ntlm, or any. required

## Details

Only supporting simple auth for now, OAuth later maybe.

For `user` and `pwd` you are required to pass in some value. The value
can be `NULL` to - which is equivalent to passing in an empty string
like `""` in `httr::authenticate`. You may want to pass in `NULL` for
both `user` and `pwd` for example if you are using `gssnegotiate` auth
type. See example below.

## Examples

``` r
auth(user = "foo", pwd = "bar", auth = "basic")
#> $userpwd
#> [1] "foo:bar"
#> 
#> $httpauth
#> [1] 1
#> 
#> attr(,"class")
#> [1] "auth"
#> attr(,"type")
#> [1] "basic"
auth(user = "foo", pwd = "bar", auth = "digest")
#> $userpwd
#> [1] "foo:bar"
#> 
#> $httpauth
#> [1] 2
#> 
#> attr(,"class")
#> [1] "auth"
#> attr(,"type")
#> [1] "digest"
auth(user = "foo", pwd = "bar", auth = "ntlm")
#> $userpwd
#> [1] "foo:bar"
#> 
#> $httpauth
#> [1] 8
#> 
#> attr(,"class")
#> [1] "auth"
#> attr(,"type")
#> [1] "ntlm"
auth(user = "foo", pwd = "bar", auth = "any")
#> $userpwd
#> [1] "foo:bar"
#> 
#> $httpauth
#> [1] -17
#> 
#> attr(,"class")
#> [1] "auth"
#> attr(,"type")
#> [1] "any"

# gssnegotiate auth
auth(NULL, NULL, "gssnegotiate")
#> $httpauth
#> [1] 4
#> 
#> attr(,"class")
#> [1] "auth"
#> attr(,"type")
#> [1] "gssnegotiate"

if (FALSE) { # \dontrun{
# with HttpClient
(res <- HttpClient$new(
  url = "https://hb.opencpu.org/basic-auth/user/passwd",
  auth = auth(user = "user", pwd = "passwd")
))
res$auth
x <- res$get()
jsonlite::fromJSON(x$parse("UTF-8"))

# with HttpRequest
(res <- HttpRequest$new(
  url = "https://hb.opencpu.org/basic-auth/user/passwd",
  auth = auth(user = "user", pwd = "passwd")
))
res$auth
} # }
```
