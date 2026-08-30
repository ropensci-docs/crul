# curl verbose method

curl verbose method

## Usage

``` r
curl_verbose(data_out = TRUE, data_in = FALSE, info = FALSE, ssl = FALSE)
```

## Arguments

- data_out:

  Show data sent to the server

- data_in:

  Show data recieved from the server

- info:

  Show informational text from curl. This is mainly useful for debugging
  https and auth problems, so is disabled by default

- ssl:

  Show even data sent/recieved over SSL connections?

## Details

line prefixes:

- `*` informative curl messages

- `=>` headers sent (out)

- `>` data sent (out)

- `*>` ssl data sent (out)

- `<=` headers received (in)

- `<` data received (in)

- `<*` ssl data received (in)

## Note

adapted from `httr::verbose`
