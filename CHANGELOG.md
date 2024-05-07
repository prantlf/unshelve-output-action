# Changes

# [6.0.0](https://github.com/prantlf/unshelve-output-action/compare/v5.0.1...v6.0.0) (2024-05-07)

## Features

* Delete ARM64 archives from cache by default ([a8e49b4](https://github.com/prantlf/unshelve-output-action/commit/a8e49b4547a6ac50fc0e864ba9901572ccc9c232))

## Bug Fixes

* Upgrade dependencies ([d64b19f](https://github.com/prantlf/unshelve-output-action/commit/d64b19f7654efb76671afe6c03e3bb5fd68bc1fc))

## BREAKING CHANGES

GitHub actions which this action depends on were upgraded to their latest versions, which require Node.js 20 for running.

You probably produce the binaries for ARM64 already and
this won;t be a breaking change for you. If you don't, this task will
try deleting them by default. You can set `include-linux-arm64` and
`include-macos-arm64` to `false` to prevent it.

# [5.0.1](https://github.com/prantlf/unshelve-output-action/compare/v5.0.0...v5.0.1) (2024-04-26)

## Bug Fixes

* Enable ARM on Linux and macOS ([3163765](https://github.com/prantlf/unshelve-output-action/commit/316376514694b5d55e6a947d2863a70782712da6))

# [5.0.0](https://github.com/prantlf/unshelve-output-action/compare/v4.0.0...v5.0.0) (2023-12-14)

## Features

* Enable support for Linux ARM64 ([c9e8320](https://github.com/prantlf/unshelve-output-action/commit/c9e8320a4f86b98b441ef5258b2af294b37a814d))

## BREAKING CHANGES

Packages ending with -linux-arm64.zip will be
downloaded by default. If you do not produce them, prevent the
failure by setting the input `include-linux-arm64` to `false`.

# [4.0.0](https://github.com/prantlf/unshelve-output-action/compare/v3.0.0...v4.0.0) (2023-11-13)

## Features

* Include ARM64 architecture for macOS os ([67c8547](https://github.com/prantlf/unshelve-output-action/commit/67c8547222a63c3061db4a154b08e9c3cc727dd3))

## BREAKING CHANGES

The ARM64 architectrure for macOS os is included by
default. If you do not produce for it, disable it by adding an input
boolean `include-macos-arm64: false` to the `with` object.

# [3.0.0](https://github.com/prantlf/unshelve-output-action/compare/v2.0.0...v3.0.0) (2023-10-22)

## Features

* Prefer discarding the shelved archive from cache automatically ([60d2883](https://github.com/prantlf/unshelve-output-action/commit/60d28839747b6775f2b4fc8dfde93d06eb22e7a0))

## BREAKING CHANGES

If you used discard-shelf-action together with this one earlier, you do not have to any more. The shelved archives are discarded from the cache from now on. If you want to prevent it, set the input `discard-shelf` to `false`.

# [2.0.0](https://github.com/prantlf/unshelve-output-action/compare/v1.2.1...v2.0.0) (2023-10-22)

## Features

* Run only in specified branches ([9a6e59e](https://github.com/prantlf/unshelve-output-action/commit/9a6e59e8a424f7a9827ff5b7b92c443d867e8d08))

## BREAKING CHANGES

If you used this action for branches `main` or `master`, your configuration will continue working, because those branches are enabled by default. If you used it for other branches, specify all their names in the input `branches`. If you used this action on all branches, set the input `branches` to `*`.

# [1.2.1](https://github.com/prantlf/unshelve-output-action/compare/v1.2.0...v1.2.1) (2023-10-21)

## Bug Fixes

* Correct inputs for choosing the platfoms to unshelve ([5ae2368](https://github.com/prantlf/unshelve-output-action/commit/5ae2368cb74991ed89cea3c2147a106ac177b3f4))

# [1.2.0](https://github.com/prantlf/unshelve-output-action/compare/v1.1.0...v1.2.0) (2023-10-21)

## Features

* Add inputs for choosing the platfoms to unshelve ([9f111a1](https://github.com/prantlf/unshelve-output-action/commit/9f111a1695b56ce1e8cb5c189e5026607c4a24dc))

# [1.1.0](https://github.com/prantlf/unshelve-output-action/compare/v1.0.1...v1.1.0) (2023-10-21)

## Features

* Add input "enable" to optionally skip this action ([69f6571](https://github.com/prantlf/unshelve-output-action/commit/69f65710b65b09696f311f9ba553f4bf6d5f24d8))

# [1.0.1](https://github.com/prantlf/unshelve-output-action/compare/v1.0.0...v1.0.1) (2023-10-18)

## Bug Fixes

* Allow restoring the cache cross-os ([192159f](https://github.com/prantlf/unshelve-output-action/commit/192159fac7c3a35073e628894af33f69692d7f4b))

# 1.0.0 (2023-10-18)

Initial release
