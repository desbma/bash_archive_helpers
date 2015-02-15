Bash archive helpers
====================

[![Tests Status](https://img.shields.io/travis/desbma/bash_archive_helpers/master.svg?label=tests&style=flat)](https://travis-ci.org/desbma/bash_archive_helpers/)

This is a collections of 16 Bash functions to create/extract archives (gz, bzip2, xz, tar, tar.gz, tar.bzip2 or tar.xz) from Bash, while providing the following useful features:
* Display a nice progress bar, with current and average rate, and estimated time to complete
* Automatically use parallel (de)compression for GZIP and BZIP2 (not supported for XZ) to use all CPU cores and speed up processing

Here is an example of terminal output:
![TarXz usage example](https://i.imgur.com/hrapRr3.png)

The command `TarXz some_directory archive.tar.xz` produces the same output file as `tar -cJf archive.tar.xz some_directory` would.

This is written in pure Bash and should be portable on most Unix systems as long as you meet the requirements below.

Automated unit tests are implemented using [assert.sh](https://github.com/lehmannro/assert.sh).


## Requirements

* [Bash](https://www.gnu.org/software/bash/) >= 4
* [tar](https://www.gnu.org/software/tar/)
* [pv](http://www.ivarch.com/programs/pv.shtml)
* [pigz](http://zlib.net/pigz/)
* [pbzip2](http://compression.ca/pbzip2/)
* [xz](http://tukaani.org/xz/)

Bash and tar are available by default on most Linux distributions.
On Ubuntu and other Debian derivatives, you can install the other dependencies with `sudo apt-get install pv pigz pbzip2 xz-utils`.


## Installation

* Download it to your home directory, ie with `curl https://raw.githubusercontent.com/desbma/bash_archive_helpers/master/archive_helpers > ~/archive_helpers`
* Add this line to your ~/.bashrc file: `. ~/archive_helpers`


## List of functions & usage

Name | Description | Usage
---- | ----------- | -----
UnTar | Extract an tar archive, uncompressed or compressed with gz, bzip2 or xz (detected from extension). | `Untar INPUT_TAR_FILE`.
Tar | Create a tar archive. | `Tar INPUT [OUTPUT_TAR_FILE [OPTIONS_PASSED_TO_TAR...]]`. If `OUTPUT_TAR_FILE` is omitted, output is redirected to stdout.
TarNpb | Same as previous, but does not display a progress bar. This is useful with huge directory trees, because input size calculation will be skipped.
TarExclude | Create a tar archive, excluding some files or directories from the input. | `TarExclude INPUT [OUTPUT_TAR_FILE [PATHS_TO_EXCLUDE...]]`. If `OUTPUT_TAR_FILE` is omitted, output is redirected to stdout.
Gz |  Compress a file with gzip compression. | `Gz INPUT [OUTPUT]`. If `OUTPUT` is omitted, output is redirected to stdout.
TarGz | Create a tar archive with gzip compression. | `TarGz INPUT [OUTPUT_TAR_GZ_FILE [OPTIONS_PASSED_TO_TAR...]]`. If `OUTPUT_TAR_GZ_FILE` is omitted, output is redirected to stdout.
TarGzNpb | Same as previous, but does not display a progress bar. This is useful with huge directory trees, because input size calculation will be skipped.
TarGzExclude | Create a tar archive, with gzip compression, excluding some files or directories from the input. | `TarGzExclude INPUT [OUTPUT_TAR_GZ_FILE [PATHS_TO_EXCLUDE...]]`. If `OUTPUT_TAR_GZ_FILE` is omitted, output is redirected to stdout.
Bz2 | Compress a file with bzip2 compression. | `Bz2 INPUT [OUTPUT]`. If `OUTPUT` is omitted, output is redirected to stdout.
TarBz2 | Create a tar archive with bzip2 compression. | `TarBz2 INPUT [OUTPUT_TAR_BZ2_FILE [OPTIONS_PASSED_TO_TAR...]]`. If `OUTPUT_TAR_BZ2_FILE` is omitted, output is redirected to stdout.
TarBz2Npb | Same as previous, but does not display a progress bar.  This is useful with huge directory trees, because input size calculation will be skipped.
TarBz2Exclude | Create a tar archive, with bzip2 compression, excluding some files or directories from the input. | `TarBz2Exclude INPUT [OUTPUT_TAR_BZ2_FILE [PATHS_TO_EXCLUDE...]]`. If `OUTPUT_TAR_BZ2_FILE` is omitted, output is redirected to stdout.
Xz | Compress a file with xz compression. | `Xz INPUT [OUTPUT]`. If `OUTPUT` is omitted, output is redirected to stdout.
TarXz | Create a tar archive with xz compression. | `TarXz INPUT [OUTPUT_TAR_XZ_FILE [OPTIONS_PASSED_TO_TAR...]]`. If `OUTPUT_TAR_XZ_FILE` is omitted, output is redirected to stdout.
TarXzNpb | Same as previous, but does not display a progress bar. This is useful with huge directory trees, because input size calculation will be skipped.
TarXzExclude | Create a tar archive, with xz compression, excluding some files or directories from the input. | `TarXzExclude INPUT [OUTPUT_TAR_XZ_FILE [PATHS_TO_EXCLUDE...]]`. If `OUTPUT_TAR_XZ_FILE` is omitted, output is redirected to stdout.


## Known issues & limitations

* Size calculations is sometimes inexact, as a result the progress bar may reach for example 102%
* Tar errors are not displayed


## License

[Mozilla Public License Version 2.0](https://www.mozilla.org/MPL/2.0/)
