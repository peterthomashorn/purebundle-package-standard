# PureBundle Package Standard

The key words “MUST”, “MUST NOT”, “REQUIRED”, “SHALL”, “SHALL NOT”, “SHOULD”, “SHOULD NOT”, “RECOMMENDED”, “MAY”, and “OPTIONAL” in this document are to be interpreted as described in [RFC 2119](https://tools.ietf.org/html/rfc2119).

The following document describes the structure of reusable and self-contained packages for development with PureBasic.

## Versioning

Bundles **must** use [semantic versioning](http://semver.org).

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


### Manifest

Every package MUST have a JSON document at its root level containing meta information as described below.

    {
      "name": "Example",
      "description": "Lorem ipsum, sit dolor amet.",
      "type": "Library",
      "url": "https://github.com/vendor/package",
      "repository": "https://github.com/vendor/package.git",
      "keywords": [
        "Development",
        "Tools"
      ],
      "license": "MIT",
      "compatibility": {
        "windows": ">=5.00",
        "macos": ">=5.00",
        "linux": ">=5.00"
      },
      "targets": {
        "default": {
          "source": "Sources/Main.pb",
          "unicode": true,
          "multithreading": false
        }
      }
    }

* The package `name` MUST be specified. The name MUST be alphanumeric and MUST NOT contain any whitespace characters.
* The package `description` MAY be specified.
* The package `type` SHOULD be specified. It can either be `project` or `library`. If omitted, it implicitly is interpreted as `library`.
* The package `url` MAY be specified. It MAY be used to reference a website of related authors or the project itself.
* The package `repository` URL MAY be specified. It MAY be used to reference the development repository of the project.
* The package `keywords` MAY be specified. Keywords can improve visibility in eventual package registries.
* The package `license` SHOULD be specified as an abbreviation.
* The package `compatibility` SHOULD be specified. If omitted, it implicitly is interpreted as compatible with all PureBasic platforms and versions.
* The package `targets` MAY be specified. See more information below under _Build Targets_.

### Source Code

* All PureBasic source code files MUST adhere to the [PureBundle Code Standard](https://github.com/peterthomashorn/purebundle-code-standard).
* Additionally, all code MUST be encapsulated within a `Module` and SHOULD NOT expose anything more than what is supposed to be used externally.
* A PureBasic IDE project MAY be provided with the source code
* If the package is a library, then a single source code file to include all package features MUST be available as `Sources/Main.pbi`

### Dependencies

All dependencies MUST be stored in the `Packages` directory. Each dependency MUST have its own subdirectory with the directory name corresponding to the dependency packages name. However it and its contents SHOULD NOT be added to version control.

### Build Targets

If no build targets are specified in the package manifest, `Sources/Main.pb` will be compiled to `Builds/<binaryname>` without any special flags. The binary name varies from platform to platform (Windows binaries have the `.exe`-suffix) and equals the package name by default.

Individual build targets are defined as an object with their names as the keys. The name `default` is reserved and MUST be specified, if `targets` are defined. An example:

    "targets": {
      "default": {
        "source": "Sources/Main.pb"
      },
      "alternative": {
        "source": "Sources/CLI.pb",
        "output": "Builds/<Package Name>-cli"
      }
    }

The following options are available for build targets:

+ `source` (optional): The entry source file to use for compilation (relative from package root). Defaults to `Sources/Main.pb`.
+ `output` (optional): The output binary filename. Defaults to `Builds/<Package Name>`.

### Build Products

Build products MAY be placed within the `Builds` directory. However it and its contents SHOULD NOT be added to version control.

### Examples

Example source code MAY be placed in the `Examples` directory.

### Resources

Additional resources like images, databases or BLOBs MAY be placed within the `Resources` directory.

### Tests

Tests MAY be placed in the `Tests` directory.
