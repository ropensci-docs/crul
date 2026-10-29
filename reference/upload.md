# upload file

upload file

## Usage

``` r
upload(path, type = NULL)
```

## Arguments

- path:

  (character) a single path, file must exist

- type:

  (character) a file type, guessed by
  [mime::guess_type](https://rdrr.io/pkg/mime/man/guess_type.html) if
  not given

## Examples

``` r
if (FALSE) { # \dontrun{
# image
path <- file.path(Sys.getenv("R_DOC_DIR"), "html/logo.jpg")
(x <- HttpClient$new(url = "https://hb.opencpu.org"))
res <- x$post(path = "post", body = list(y = upload(path)))
res$content

# text file, in a list
file <- upload(system.file("CITATION"))
res <- x$post(path = "post", body = list(y = file))
jsonlite::fromJSON(res$parse("UTF-8"))

# text file, as data
res <- x$post(path = "post", body = file)
jsonlite::fromJSON(res$parse("UTF-8"))
} # }
```
