# MichaelWeissDEV Homebrew tap

This repository contains `Formula/refhound.rb`, currently pointing to the
**0.1.0b1 beta** published on PyPI. The formula and its installation matrix
have not yet been validated; do not treat this beta as a stable release. The
formula will only be available to other users after the reviewed tap commit is
pushed to GitHub. No push or publication is performed by this repository.

Once the formula has passed CI and is published in this tap:

```sh
brew tap MichaelWeissDEV/tap
brew install MichaelWeissDEV/tap/refhound
refhound --version
refhound scan . --offline --quick --no-store
```

For upgrades use `brew update && brew upgrade refhound`; remove the package
with `brew uninstall refhound` and optionally remove the tap with
`brew untap MichaelWeissDEV/tap`. Git and Python are Homebrew dependencies;
the Python dependencies are installed in a formula-owned virtual environment.
The first source build needs Rust and can be slow. Python build backends and
Rust crate builds may access the network; versioned Python source resources
are SHA-256 checked but this is not a fully offline or hermetic build.

## Maintainer update procedure

1. Publish and verify the intended RefHound version separately, with explicit
   approval. Never invent an archive URL or checksum for an unpublished release.
2. Update the formula's source URL and SHA-256 using the exact PyPI sdist (or
   another reviewed immutable release archive). Regenerate **all** transitive
   Python resources for the selected Python interpreter, for example using
   `brew update-python-resources MichaelWeissDEV/tap/refhound` after the tap
   is installed locally. Review package versions, download locations and hashes.
3. Run `brew style`, build from source and run `brew test` on macOS ARM64 and
   x86_64. The CI workflow attempts both; platform availability depends on
   the GitHub account's hosted runner access. The test makes a synthetic Git
   repository and scans it.
4. Review and push the tap changes only after all required tests pass and
   publication is approved. Test `brew install` from the actual tap.

The source currently tracks the public **beta**, not the pending stable
`v0.1.0`. Dependency pins describe this formula, not a lockfile for pip users.
