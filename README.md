# wkhtmltopdf_binary_gem

## Tracking large files with Git LFS

You also need to have Git LFS (Large File Storage) installed and the binary files tracked with it
(e.g. `bin/wkhtmltopdf_*`). See [git-lfs](https://git-lfs.github.com/).

    brew install git-lfs
    git lfs install
    git lfs track "bin/wkhtmltopdf_*"

## Extracting binaries

Hints for extracting binaries from https://wkhtmltopdf.org/downloads.html (dpkg and rpm2cpio is available on Homebrew).

Debian/Ubuntu

    dpkg -x wkhtmltox_0.12.5-1.trusty_amd64.deb .

CentOS

    rpm2cpio wkhtmltox-0.12.5-1.centos7.x86_64.rpm | cpio -idmv

macOS

    xar -xf wkhtmltox-0.12.5-1.macos-cocoa.pkg
    cat Payload | gunzip -dc | cpio -i

## Testing with Docker

Make sure you have Docker and Docker Compose installed (see https://docs.docker.com/compose/install/ for more
information).

There are Dockerfiles for the supported Linux based distributions under `.docker`. You can build them all with
`docker-compose build` and run each individually with e.g. `docker-compose run ubuntu_18.04`.

There also is a rudimentary minitest test that simply invokes `docker-compose run` for each distribution and
expects to see the output of `wkhtmltopdf --version`. Just run `rake` to run it. 

You can clean up after testing with `docker-compose down --rmi all`.
