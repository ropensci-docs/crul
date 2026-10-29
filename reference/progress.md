# progress bars

progress bars

## Details

pass `httr::progress()` to `progress` param in
[HttpClient](https://docs.ropensci.org/crul/reference/HttpClient.md),
which pulls out relevant info to pass down to curl

if file sizes known you get progress bar; if file sizes not known you
get bytes downloaded

See the README for examples
