# What's new in 2.0.1

## Compatibility 

Works with CDH3, CDH4, Apache 1.0.4 and MapR 2.0.1. See [Compatibility](compatibility.md)

## Fixes
* Fixed `rmr.sample`. The function in 2.0 was broken due to a commit mishap.
* Hardened `keyval` argument recycling feature against some edge cases (not `NULL` but 0-length keys or values).
* Local mode again compatible with mixed type input files. The local backend failed when multiple inputs were provided but they represented different record types, which is typical of joins. No longer.
* Fixed equijoin with new reduce default. The 2.0 version had a number of problems due to an incomplete port to the 2.0 API. The new reduce default does a `merge` of left and right side in most cases, returns left and right groups as they are when lists are involved.
* Hardened streaming backend against user code or packages writing to `stdout`. This output stream is reserved for hadoop streaming use. We now capture all output at package load time and from the map and reduce functions and redirect it to standard error. There is one case we can't handle, see #40.
* Improved environment load  on the nodes. In some cases local variables could be overwritten by global environment variables, not anymore.
* Hardened hdfs functions against some small platform variations. This seemed to give rise only to error messages without further consequences in most cases, but had been a source of alarm for users.

## Features
* automatic package install & update feature (experimental). At default, nothing changes, you need to install all the packages you need on all the nodes. If you set the package option `install.args` to a list, even empty, rmr will try to install missing packages using that list as additional arguments for `install.packages` (the `libs` argument is set to the current list of loaded packages) . Same logic with `update.args`. This feature is experimental and, as we said, off by default. Testing has been very limited, please consider this a preview of a feature targted for 2.1

## Behind the scenes
* prettified a lot of code to show directly in documents and presentations using literate programming. This is important because the same code is showed everywhere, no copy and paste, no pseudo-code, no nothing. The code in the [Tutorial] and other documents is always real, fresh and tested. Documents are generated with knitr and presentation with knitr and pandoc. Thanks to  Yihui Xie and John MacFarlane for these great software and direct support.
