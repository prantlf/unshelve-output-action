# Unshelve Build Output

GitHub action for unshelving a build output from the cache, where it was shelved by [shelve-output-action], to be able to upload it as artefacts for a new release.

Only platforms Linux, macOS, Windows on the architecture X64 are supported.

## Usage

Download archives with binary executables produced on each platform and shelved earlier to the project root and delete the shelf from the cache:

```yml
- uses: prantlf/unshelve-output-action@v5
```

Depending on the `name` of the executable, it will download the following archives from the cache. For example, for the name `newchanges`:

|    OS   | Architecture |            Archive             |            Cache Key                 |
|:--------|:-------------|:-------------------------------|:-------------------------------------|
| Linux   |      X64     | `newchanges-linux-x64.zip`     | `newchanges-linux-x64.zip-{sha}`     |
| Linux   |     ARM64    | `newchanges-linux-arm64.zip`   | `newchanges-linux-arm64.zip-{sha}`   |
| Linux   |    RISCV64   | `newchanges-linux-riscv64.zip` | `newchanges-linux-riscv64.zip-{sha}` |
| macOS   |     ARM64    | `newchanges-macos-arm64.zip`   | `newchanges-macos-arm64.zip-{sha}`   |
| macOS   |      X64     | `newchanges-macos-x64.zip`     | `newchanges-macos-x64.zip-{sha}`     |
| Windows |      X64     | `newchanges-windows-x64.zip`   | `newchanges-windows-x64.zip-{sha}`   |

The name prefix of the archives can be specified by `name`. If not specified, it will be inferred from the project configuration (`v.mod`). The `{sha}` in the cache key is the SHA-1 hash of the current commit.

Use a different name prefix than the default in the package archive name. Work only in specific release branches. Prevent deletion the shelf from the cache. Ignore the archive for macOS ARM64:

```yml
jobs:
  release:
    steps:
    ...
    - uses: prantlf/unshelve-output-action@v5
      with:
        name: vpm
        branches: master v1.x
        discard-shelf: false
        include-macos-arm64: false
```

## Inputs

The following parameters can be specified using the `with` object:

### name

Type: `String`<br>
Default: (read from `v.mod`)

The name of the archive without the platform and architecture and without the `.zip` extension. The project name from `v.mod` will be used by default. The expected names of the archives will be `{name}-{os}-{arch}.zip`, for example: `newchanges-linux-x64.zip`.

### branches

Type: `String`<br>
Default: `'main master'`

Branches which this action should run for, which are used to publishing releases. Use whitespace for separating the branch names. If you want to use multiple lines in YAML, introduce them with ">-". If you want to allow all branches, set the value to "*".

### enable

Type: `Boolean`<br>
Default: `true`

Can be set to `false` to prevent this action from downloading the archives. It's helpful in the pipeline, which will not continue releasing, but only building and testing, and that will be decided in the middle of a job execution.

### include-linux

Type: `Boolean`<br>
Default: `true`

Include the archive for Linux ARM64, RISCV64 and X64.

### include-linux-arm64

Type: `Boolean`<br>
Default: `true`

Include the archive for Linux ARM64.

### include-linux-riscv64

Type: `Boolean`<br>
Default: `true`

Include the archive for Linux RISCV64.

### include-linux-x64

Type: `Boolean`<br>
Default: `true`

Include the archive for Linux X64.

### include-macos

Type: `Boolean`<br>
Default: `true`

Include archives for macOS ARM64 and X64.

### include-macos-arm64

Type: `Boolean`<br>
Default: `true`

Include the archive for macOS ARM64.

### include-macos-x64

Type: `Boolean`<br>
Default: `true`

Include the archive for macOS X64.

### include-windows

Type: `Boolean`<br>
Default: `true`

Include the archive for Windows.

### discard-shelf

Type: `Boolean`<br>
Default: `true`

Can be set to `false` to prevent automatic discarding of the shelved files from the cache.

## License

Copyright (C) 2023-2024 Ferdinand Prantl

Licensed under the [MIT License].

[MIT License]: http://en.wikipedia.org/wiki/MIT_License
[shelve-output-action]: https://github.com/prantlf/shelve-output-action
