# IPATool (Custom Patched Version v2.3.1)

[![Release](https://img.shields.io/github/release/mehmetakifsimsek/ipatool.svg?label=Release)](https://github.com/mehmetakifsimsek/ipatool/releases/)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](https://github.com/mehmetakifsimsek/ipatool/blob/main/LICENSE)

`ipatool` is a command line tool that allows you to search for iOS apps on the [App Store](https://apps.apple.com) and download a copy of the app package, known as an _ipa_ file.

This is a custom patched version of `ipatool` containing critical fixes and new features.

- [Added Features & Enhancements](#added-features--enhancements)
- [Requirements](#requirements)
- [Installation](#installation)
  - [Manual](#manual)
- [Usage](#usage)
- [Compiling](#compiling)
- [License](#license)
- [Releases](https://github.com/mehmetakifsimsek/ipatool/releases)

---

## Added Features & Enhancements

This custom version includes the following updates:

1. **`--country` (`-c`) Flag on Search:**
   You can specify a storefront country code (e.g. `us`, `tr`, `nl`) when searching for apps, allowing you to find apps available in specific regions outside your account's primary region.
   
2. **Storefront & Country Detection:**
   The `auth info` command now automatically resolves and prints the 6-digit storefront ID and the mapped 2-letter country code of your Apple ID account.

3. **Friendly Connection Error Handling:**
   Instead of displaying cryptic plist parsing errors (e.g. `unexpected hex digit 'h'`) when Apple returns an HTML error page (due to rate-limits or temporary blocks), the tool now logs a clear, human-readable error.

---

## Requirements

- Supported operating system (Windows, Linux or macOS).
- Apple ID set up to use the App Store.

## Installation

### Manual

You can grab the latest custom version of `ipatool` from [GitHub releases](https://github.com/mehmetakifsimsek/ipatool/releases).

---

## Usage

To authenticate with the App Store, use the `auth` command.

```
Authenticate with the App Store

Usage:
  ipatool auth [command]

Available Commands:
  info        Show current account info (including storefront ID and country code)
  login       Login to the App Store
  revoke      Revoke your App Store credentials

Flags:
  -h, --help   help for auth

Global Flags:
      --format format     sets output format for command; can be 'text', 'json' (default text)
      --non-interactive   run in non-interactive session
      --verbose           enables verbose logs

Use "ipatool auth [command] --help" for more information about a command.
```

To search for apps on the App Store, use the `search` command.

```
Search for iOS and tvOS apps available on the App Store

Usage:
  ipatool search <term> [flags]

Flags:
  -c, --country string    Storefront country code to search (e.g. us, tr, nl)
  -h, --help              help for search
  -l, --limit int         maximum amount of search results to retrieve (default 5)
      --platform string   Platform to search: iphone, ipad, or appletv

Global Flags:
      --format format     sets output format for command; can be 'text', 'json' (default text)
      --non-interactive   run in non-interactive session
      --verbose           enables verbose logs
```

To obtain a license for an app, use the `purchase` command.

```
Obtain a license for the app from the App Store

Usage:
  ipatool purchase [flags]

Flags:
  -b, --bundle-identifier string   Bundle identifier of the target iOS app (required)
  -h, --help                       help for purchase

Global Flags:
      --format format     sets output format for command; can be 'text', 'json' (default text)
      --non-interactive   run in non-interactive session
      --verbose           enables verbose logs
```

To obtain a list of availble app versions to download, use the `list-versions` command.

```
List the available versions of an iOS app

Usage:
  ipatool list-versions [flags]

Flags:
  -i, --app-id int                 ID of the target iOS app (required)
  -b, --bundle-identifier string   The bundle identifier of the target iOS app (overrides the app ID)
  -h, --help                       help for list-versions

Global Flags:
      --format format                sets output format for command; can be 'text', 'json' (default text)
      --keychain-passphrase string   passphrase for unlocking keychain
      --non-interactive              run in non-interactive session
      --verbose                      enables verbose logs
```

To download a copy of the ipa file, use the `download` command.

```
Download (encrypted) iOS and tvOS app packages from the App Store

Usage:
  ipatool download [flags]

Flags:
  -i, --app-id int                   ID of the target iOS app (required)
  -b, --bundle-identifier string     The bundle identifier of the target iOS app (overrides the app ID)
      --external-version-id string   External version identifier of the target iOS app (defaults to latest version when not specified)
  -h, --help                         help for download
  -o, --output string                The destination path of the downloaded app package
      --platform string              Platform to download for: iphone, ipad, or appletv
      --purchase                     Obtain a license for the app if needed

Global Flags:
      --format format                sets output format for command; can be 'text', 'json' (default text)
      --keychain-passphrase string   passphrase for unlocking keychain
      --non-interactive              run in non-interactive session
      --verbose                      enables verbose logs
```

To resolve an external version identifier, returned by the `list-versions` command, use the `get-version-metadata` command.

```
Retrieves the metadata for a specific version of an app

Usage:
  ipatool get-version-metadata [flags]

Flags:
  -i, --app-id int                   ID of the target iOS app (required)
  -b, --bundle-identifier string     The bundle identifier of the target iOS app (overrides the app ID)
      --external-version-id string   External version identifier of the target iOS app (required)
  -h, --help                         help for get-version-metadata

Global Flags:
      --format format                sets output format for command; can be 'text', 'json' (default text)
      --keychain-passphrase string   passphrase for unlocking keychain
      --non-interactive              run in non-interactive session
      --verbose                      enables verbose logs
```

**Note:** the tool runs in interactive mode by default. Use the `--non-interactive` flag
if running in an automated environment.

## Compiling

The tool can be compiled using the Go toolchain.

```shell
$ go build -o ipatool
```

Unit tests can be executed with the following commands.

```shell
$ go generate github.com/mehmetakifsimsek/ipatool/v2/...
$ go test -v github.com/mehmetakifsimsek/ipatool/v2/...
```

## License

IPATool is released under the [MIT license](https://github.com/mehmetakifsimsek/ipatool/blob/main/LICENSE).

