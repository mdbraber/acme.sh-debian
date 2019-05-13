# acme.sh-debian

This projects helps to package [acme.sh](https://github.com/neilpang/acme.sh) as a Debian archive (.deb). acme.sh actually has a pretty go installer (`acme.sh --install`) but if you want to use a (personal) APT repository (e.g. with using [unattended-upgrades](https://packages.debian.org/stretch/unattended-upgrades)) this could help make it easier to install. Also this could be used to create a package that already holds your personal configuration files. 

The resulting package will do the following:

1. Install `acme.sh` and all library files (`dnsapi/`, `deploy/` and `notify`) in `/usr/lib/acme.sh`
2. Install `account.conf` in `/etc/acme.sh/account.conf`
3. Set `/etc/acme.sh/cert` as the location for certificates (via `$CERT_HOME`)
4. Install the cronjob for renewing the certificates as `root`
5. Set up an alias for root (`alias acme.sh=/usr/lib/acme.sh/acme.sh`)

# Configure

Change the `$PROJECT` and `$BRANCH` variables in `debian/rules` to make sure you're using the right package. E.g. if you've created your own branch/fork of `acme.sh` you can use that here. Also make sure to adapt `account-etc.conf` (to be installed in `/etc/acme.sh/account.conf` to your needs).

After you've adapted the package update the changelog with `dch` (which also determines the version number for this package)

# Build

Build the package using `make debian` in the main directory.

# Install

Install the resulting package with `dpkg -i` or add it to your personal APT repository
