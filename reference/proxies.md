# proxy options

proxy options

## Usage

``` r
proxy(url, user = NULL, pwd = NULL, auth = "basic")
```

## Arguments

- url:

  (character) URL, with scheme (http/https), domain and port (must be
  numeric). required.

- user:

  (character) username, optional

- pwd:

  (character) password, optional

- auth:

  (character) authentication type, one of basic (default), digest,
  digest_ie, gssnegotiate, ntlm, any or `NULL`. optional

## Details

See https://www.hidemyass.com/proxy for a list of proxies you can use

## Examples

``` r
proxy("http://97.77.104.22:3128")
#> $proxy
#> [1] "97.77.104.22"
#> 
#> $proxyport
#> [1] 3128
#> 
#> $proxyauth
#> [1] 1
#> 
#> attr(,"class")
#> [1] "proxy"
proxy("97.77.104.22:3128")
#> $proxy
#> [1] "97.77.104.22"
#> 
#> $proxyport
#> [1] 3128
#> 
#> $proxyauth
#> [1] 1
#> 
#> attr(,"class")
#> [1] "proxy"
proxy("http://97.77.104.22:3128", "foo", "bar")
#> $proxy
#> [1] "97.77.104.22"
#> 
#> $proxyport
#> [1] 3128
#> 
#> $proxyuserpwd
#> [1] "foo:bar"
#> 
#> $proxyauth
#> [1] 1
#> 
#> attr(,"class")
#> [1] "proxy"
proxy("http://97.77.104.22:3128", "foo", "bar", auth = "digest")
#> $proxy
#> [1] "97.77.104.22"
#> 
#> $proxyport
#> [1] 3128
#> 
#> $proxyuserpwd
#> [1] "foo:bar"
#> 
#> $proxyauth
#> [1] 2
#> 
#> attr(,"class")
#> [1] "proxy"
proxy("http://97.77.104.22:3128", "foo", "bar", auth = "ntlm")
#> $proxy
#> [1] "97.77.104.22"
#> 
#> $proxyport
#> [1] 3128
#> 
#> $proxyuserpwd
#> [1] "foo:bar"
#> 
#> $proxyauth
#> [1] 8
#> 
#> attr(,"class")
#> [1] "proxy"

# socks
proxy("socks5://localhost:9050/", auth = NULL)
#> $proxy
#> [1] "socks5://localhost:9050/"
#> 
#> attr(,"class")
#> [1] "proxy"

if (FALSE) { # \dontrun{
# with proxy (look at request/outgoing headers)
# (res <- HttpClient$new(
#   url = "http://www.google.com",
#   proxies = proxy("http://97.77.104.22:3128")
# ))
# res$proxies
# res$get(verbose = TRUE)

# vs. without proxy (look at request/outgoing headers)
# (res2 <- HttpClient$new(url = "http://www.google.com"))
# res2$get(verbose = TRUE)


# Use authentication
# (res <- HttpClient$new(
#   url = "http://google.com",
#   proxies = proxy("http://97.77.104.22:3128", user = "foo", pwd = "bar")
# ))

# another example
# (res <- HttpClient$new(
#   url = "http://ip.tyk.nu/",
#   proxies = proxy("http://200.29.191.149:3128")
# ))
# res$get()$parse("UTF-8")
} # }
```
