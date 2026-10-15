# ansible-envoy

Installs the checksum-verified Envoy binary at `/usr/bin/envoy` on RedHat-family
Linux systems with x86-64 or AArch64 processors. The role does not configure Envoy
or install, enable, or start a service.

## Variables

- `envoy_version` defaults to `1.38.4`; set a string in `major.minor.patch` form
  without a leading `v`. The role replaces an installed binary when its version
  differs, including downgrades.
- `envoy_checksum` defaults to `""`; set a SHA-256 digest containing exactly 64
  hexadecimal characters to override checksum discovery. An empty string uses the
  embedded checksum for the exact version and architecture, then Tetrate release
  metadata if no pin exists. `null` is not accepted.

Run with root privileges and gathered facts. Installation requires HTTPS access
from the managed host to `archive.tetratelabs.io`. Other OS families are skipped.
The role leaves an already matching binary in place without retrieving release
metadata or downloading an archive; a checksum override applies only when
installation is needed. The role fails if it cannot identify an existing binary's
release version.
