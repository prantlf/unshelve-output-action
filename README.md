# Unshelve Build Output

GitHub action for unshelving a build output from the cache, where it was shelved by [shelve-output-action], to be able to upload it as artefacts for a new release.

Only platforms Linux, macOS, Windows on the architecture X64 are supported.

## Usage

Download archives with binary executables produced on each platform and shelved earlier to the project root:

```yml
- uses: prantlf/unshelve-output-action@v1
```

Depending on the `name` of the executable, it will download the following archives from the cache. For example, for the name `newchanges`:

|    OS   |            Archive           |            Cache Key               |
|:--------|:-----------------------------|:-----------------------------------|
| Linux   | `newchanges-linux-x64.zip`   | `newchanges-linux-x64.zip-{sha}`   |
| macOS   | `newchanges-macos-x64.zip`   | `newchanges-macos-x64.zip-{sha}`   |
| Windows | `newchanges-windows-x64.zip` | `newchanges-windows-x64.zip-{sha}` |

The name prefix of the archives can be specified by `name`. If not specified, it will be inferred from the project configuration (`v.mod`). The `{sha}` in the cache key is the SHA-1 hash of the current commit.

Use a different name prefix than the default in the package archive name:

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

### enable

Type: `Boolean`<br>
Default: `true`

Can be set to `false` to prevent this action from downloading the archives. It's helpful in the pipeline, which will not continue releasing, but only building and testing, and that will be decided in the middle of a job execution.

### include-linux

Type: `Boolean`<br>
Default: `true`

Include the archive for Linux.

### include-macos

Type: `Boolean`<br>
Default: `true`

Include the archive for macOS.

### include-windows

Type: `Boolean`<br>
Default: `true`

Include the archive for Windows.

## License

Copyright (C) 2023 Ferdinand Prantl

Licensed under the [MIT License].

[MIT License]: http://en.wikipedia.org/wiki/MIT_License
[shelve-output-action]: https://github.com/prantlf/shelve-output-action
