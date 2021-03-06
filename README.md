Bash archive helpers
====================

[![Tests Status](https://img.shields.io/travis/desbma/bash_archive_helpers/master.svg?label=tests&style=flat)](https://travis-ci.org/desbma/bash_archive_helpers/)

This is a collections of 19 Bash functions to create/extract archives (gz, bzip2, xz, tar, tar.gz, tar.bzip2 or tar.xz) from Bash, while providing the following useful features:
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

* Download it to your home directory, ie with:  
`curl https://raw.githubusercontent.com/desbma/bash_archive_helpers/master/archive_helpers > ~/bash_archive_helpers`
* Add this line to your _~/.bashrc_ file:  
`. ~/bash_archive_helpers`


## List of functions & usage

Name | Description | Parallel processing | Usage
---- | ----------- | ------------------- | -----
UnTar | Extract an tar archive, uncompressed or compressed with gz, bzip2 or xz (detected from extension). | Yes (for gz and bzip2 archives) | `Untar INPUT_TAR_FILE`.
Tar | Create a tar archive. | No | `Tar INPUT [OUTPUT_TAR_FILE [OPTIONS_PASSED_TO_TAR...]]`. If `OUTPUT_TAR_FILE` is omitted, output is redirected to stdout.
TarNpb | Same as previous, but does not display a progress bar. This is useful with huge directory trees, because input size calculation will be skipped. | No | `TarNpb INPUT [OUTPUT_TAR_FILE [OPTIONS_PASSED_TO_TAR...]]`. If `OUTPUT_TAR_FILE` is omitted, output is redirected to stdout.
TarExclude | Create a tar archive, excluding some files or directories from the input. | No | `TarExclude INPUT [OUTPUT_TAR_FILE [PATHS_TO_EXCLUDE...]]`. If `OUTPUT_TAR_FILE` is omitted, output is redirected to stdout.
Gz |  Compress a file with gzip compression. | Yes | `Gz INPUT [OUTPUT]`. If `OUTPUT` is omitted, output is redirected to stdout.
UnGz |  Decompress a gzip file. | Yes | `UnGz INPUT [OUTPUT]`. If `OUTPUT` is omitted, output is same as `INPUT` with the `gz` extension removed.
TarGz | Create a tar archive with gzip compression. | Yes | `TarGz INPUT [OUTPUT_TAR_GZ_FILE [OPTIONS_PASSED_TO_TAR...]]`. If `OUTPUT_TAR_GZ_FILE` is omitted, output is redirected to stdout.
TarGzNpb | Same as previous, but does not display a progress bar. This is useful with huge directory trees, because input size calculation will be skipped. | Yes | `TarGzNpb INPUT [OUTPUT_TAR_GZ_FILE [OPTIONS_PASSED_TO_TAR...]]`. If `OUTPUT_TAR_GZ_FILE` is omitted, output is redirected to stdout.
TarGzExclude | Create a tar archive, with gzip compression, excluding some files or directories from the input. | Yes | `TarGzExclude INPUT [OUTPUT_TAR_GZ_FILE [PATHS_TO_EXCLUDE...]]`. If `OUTPUT_TAR_GZ_FILE` is omitted, output is redirected to stdout.
Bz2 | Compress a file with bzip2 compression. | Yes | `Bz2 INPUT [OUTPUT]`. If `OUTPUT` is omitted, output is redirected to stdout.
UnBz2 |  Decompress a bzip2 file. | Yes | `UnBz2 INPUT [OUTPUT]`. If `OUTPUT` is omitted, output is same as `INPUT` with the `bz2` extension removed.
TarBz2 | Create a tar archive with bzip2 compression. | Yes | `TarBz2 INPUT [OUTPUT_TAR_BZ2_FILE [OPTIONS_PASSED_TO_TAR...]]`. If `OUTPUT_TAR_BZ2_FILE` is omitted, output is redirected to stdout.
TarBz2Npb | Same as previous, but does not display a progress bar.  This is useful with huge directory trees, because input size calculation will be skipped. | Yes | `TarBz2Npb INPUT [OUTPUT_TAR_BZ2_FILE [OPTIONS_PASSED_TO_TAR...]]`. If `OUTPUT_TAR_BZ2_FILE` is omitted, output is redirected to stdout.
TarBz2Exclude | Create a tar archive, with bzip2 compression, excluding some files or directories from the input. | Yes | `TarBz2Exclude INPUT [OUTPUT_TAR_BZ2_FILE [PATHS_TO_EXCLUDE...]]`. If `OUTPUT_TAR_BZ2_FILE` is omitted, output is redirected to stdout.
Xz | Compress a file with xz compression. | No | `Xz INPUT [OUTPUT]`. If `OUTPUT` is omitted, output is redirected to stdout.
UnXz |  Decompress a xz file. | Yes | `UnXz INPUT [OUTPUT]`. If `OUTPUT` is omitted, output is same as `INPUT` with the `xz` extension removed.
TarXz | Create a tar archive with xz compression. | No | `TarXz INPUT [OUTPUT_TAR_XZ_FILE [OPTIONS_PASSED_TO_TAR...]]`. If `OUTPUT_TAR_XZ_FILE` is omitted, output is redirected to stdout.
TarXzNpb | Same as previous, but does not display a progress bar. This is useful with huge directory trees, because input size calculation will be skipped. | No | `TarXzNpb INPUT [OUTPUT_TAR_XZ_FILE [OPTIONS_PASSED_TO_TAR...]]`. If `OUTPUT_TAR_XZ_FILE` is omitted, output is redirected to stdout.
TarXzExclude | Create a tar archive, with xz compression, excluding some files or directories from the input. | No | `TarXzExclude INPUT [OUTPUT_TAR_XZ_FILE [PATHS_TO_EXCLUDE...]]`. If `OUTPUT_TAR_XZ_FILE` is omitted, output is redirected to stdout.


## Known issues & limitations

* Size calculations are sometimes inexact when creating tar archives for large directory trees, as a result the progress bar may reach for example 102%
* Tar errors are not displayed


## License

[Mozilla Public License Version 2.0](https://www.mozilla.org/MPL/2.0/)
