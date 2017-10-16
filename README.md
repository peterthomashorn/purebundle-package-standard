# PureBundle Package Standard

The key words “MUST”, “MUST NOT”, “REQUIRED”, “SHALL”, “SHALL NOT”, “SHOULD”, “SHOULD NOT”, “RECOMMENDED”, “MAY”, and “OPTIONAL” in this document are to be interpreted as described in [RFC 2119](https://tools.ietf.org/html/rfc2119).

The following document describes the structure of reusable and self-contained packages for development with PureBasic.

## Versioning

Bundles **must** use [semantic versioning](http://semver.org).

## Manifest

Every package MUST have a JSON document at its root level containing meta information as described below.

## Files

An example overview of the possible organization within a package:

    Builds/
    Examples/
      Embedded.pb
    Packages/
    Resources/
    Sources/
      Main.pb
      Package.pbp
    Tests/
      TestModule.pb
    Package.json


### Source Code

* All PureBasic source code files MUST adhere to the [PureBundle Code Standard](https://github.com/peterthomashorn/purebundle-code-standard).
* Additionally, all code MUST be encapsulated within a `Module` and SHOULD NOT expose anything more than what is supposed to be used externally.
* A PureBasic IDE project MAY be provided with the source code

### Dependencies

All dependencies MUST be stored in the `Packages` directory. Each dependency MUST have its own subdirectory with the directory name corresponding to the dependency packages name.

### Build Products

Build products MAY be placed within the `Builds` directory. However it and its contents SHOULD NOT be added to version control.

### Examples

Example source code MAY be placed in the `Examples` directory.

### Resources

Additional resources like images, databases or BLOBs MAY be placed within the `Resources` directory.

### Tests

Tests MAY be placed in the `Tests` directory.
