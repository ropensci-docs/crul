# Build and parse URLs

Build and parse URLs

## Usage

``` r
url_build(url, path = NULL, query = NULL)

url_parse(url)
```

## Arguments

- url:

  (character) a url, length 1

- path:

  (character) a path, length 1

- query:

  (list) a named list of query parameters

## Value

`url_build` returns a character string URL; `url_parse` returns a list
with URL components

## Examples

``` r
url_build("https://hb.opencpu.org")
#> [1] "https://hb.opencpu.org/"
url_build("https://hb.opencpu.org", "get")
#> [1] "https://hb.opencpu.org/get"
url_build("https://hb.opencpu.org", "post")
#> [1] "https://hb.opencpu.org/post"
url_build("https://hb.opencpu.org", "get", list(foo = "bar"))
#> [1] "https://hb.opencpu.org/get?foo=bar"

url_parse("hb.opencpu.org")
#> $scheme
#> [1] NA
#> 
#> $domain
#> [1] "hb.opencpu.org"
#> 
#> $port
#> [1] NA
#> 
#> $path
#> [1] NA
#> 
#> $parameter
#> [1] NA
#> 
#> $fragment
#> [1] NA
#> 
url_parse("https://hb.opencpu.org")
#> $scheme
#> [1] "https"
#> 
#> $domain
#> [1] "hb.opencpu.org"
#> 
#> $port
#> [1] NA
#> 
#> $path
#> [1] NA
#> 
#> $parameter
#> [1] NA
#> 
#> $fragment
#> [1] NA
#> 
url_parse(url = "https://hb.opencpu.org")
#> $scheme
#> [1] "https"
#> 
#> $domain
#> [1] "hb.opencpu.org"
#> 
#> $port
#> [1] NA
#> 
#> $path
#> [1] NA
#> 
#> $parameter
#> [1] NA
#> 
#> $fragment
#> [1] NA
#> 
url_parse("https://hb.opencpu.org/get")
#> $scheme
#> [1] "https"
#> 
#> $domain
#> [1] "hb.opencpu.org"
#> 
#> $port
#> [1] NA
#> 
#> $path
#> [1] "get"
#> 
#> $parameter
#> [1] NA
#> 
#> $fragment
#> [1] NA
#> 
url_parse("https://hb.opencpu.org/get?foo=bar")
#> $scheme
#> [1] "https"
#> 
#> $domain
#> [1] "hb.opencpu.org"
#> 
#> $port
#> [1] NA
#> 
#> $path
#> [1] "get"
#> 
#> $parameter
#> $parameter$foo
#> [1] "bar"
#> 
#> 
#> $fragment
#> [1] NA
#> 
url_parse("https://hb.opencpu.org/get?foo=bar&stuff=things")
#> $scheme
#> [1] "https"
#> 
#> $domain
#> [1] "hb.opencpu.org"
#> 
#> $port
#> [1] NA
#> 
#> $path
#> [1] "get"
#> 
#> $parameter
#> $parameter$foo
#> [1] "bar"
#> 
#> $parameter$stuff
#> [1] "things"
#> 
#> 
#> $fragment
#> [1] NA
#> 
url_parse("https://hb.opencpu.org/get?foo=bar&stuff=things[]")
#> $scheme
#> [1] "https"
#> 
#> $domain
#> [1] "hb.opencpu.org"
#> 
#> $port
#> [1] NA
#> 
#> $path
#> [1] "get"
#> 
#> $parameter
#> $parameter$foo
#> [1] "bar"
#> 
#> $parameter$stuff
#> [1] "things[]"
#> 
#> 
#> $fragment
#> [1] NA
#> 
```
