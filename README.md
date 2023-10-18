# Unshelve Build Output

GitHub action for unshelving a build output from the cache, where it was shelved by [shelve-output-action], to be able to upload it as artefacts for a new release.

Only platforms Linux, macOS, Windows on the architecture X64 are supported.

## Usage

Download archives with binary executables produced on each platform and shelved earlier to the project root:

```yml
- uses: prantlf/unshelve-output-action@v1
```

Use a different name, platform and architecture that defaults in the package archive name. Specify a custom path to the binary:

```yml
jobs:
  release:
    steps:
    ...
    - uses: prantlf/unshelve-output-action@v1
      with:
        name: vpm
```

## Inputs

The following parameters can be specified using the `with` object:

### name

Type: `String`<br>
Default: (read from `v.mod`)

The name of the archive without the platform and architecture and without the `.zip` extension. The project name from `v.mod` will be used by default. The expected names of the archives will be `{name}-{os}-{arch}.zip`, for example: `newchanges-linux-x64.zip`.

## License

Copyright (C) 2023 Ferdinand Prantl

Licensed under the [MIT License].

[MIT License]: http://en.wikipedia.org/wiki/MIT_License
[shelve-output-action]: https://github.com/prantlf/shelve-output-action
