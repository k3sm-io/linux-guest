# linux-guest

Guest kernel and initramfs artifacts for the k3sm `vm` RuntimeClass.

Each release publishes:

- `Image` — an uncompressed linux/arm64 kernel, built reproducibly from an
  unmodified upstream kernel.org source tarball with the committed
  `kernel.config` (published alongside as corresponding source).
- `k3sm-initramfs.cpio` — a byte-deterministic initramfs containing the k3sm
  guest init. The `runtimed` commit it was composed from is named in the
  release notes.
- `sha256sums` — digests for every asset.
- Corresponding source (GPLv2): `kernel.config`, the upstream tarball
  reference and its sha256, and a copy of the build script. The kernel source
  is the unmodified upstream tarball at the recorded reference; this follows
  the practice of binary distributions that ship unmodified upstream kernels
  and point at the upstream source.

k3sm pins these artifacts by sha256 in code
(`runtimed/pkg/guestartifacts`); the daemon fetches on cache miss and
verifies the digest on every use. A digest change is a code change and ships
only with a k3sm release.

Build reproduction: `runtimed/hack/guest-kernel/build.sh` in
[k3sm-io/runtimed](https://github.com/k3sm-io/runtimed). Two independent
builds from the published inputs produce byte-identical output.
