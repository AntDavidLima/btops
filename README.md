# btops

bspwm desktop management that supports dymanic appending, removing, and renaming

This fork add the option to enable/disable the removal of a focused empty desktop.

## Introduction

Often times a workflow for a given day can't be defined by a set number of desktops with constant names. Btops enables you to define your workspaces based on what you're doing so you don't have worry about things like putting your applications in their respective desktops, running out of desktops, or leaving desktops unused and empty.

## Examples

- [Dynamic with classified renamers](https://github.com/antdavidlima/btops/blob/master/examples/classified.toml)
- [Minmax with numeric renamer](https://github.com/antdavidlima/btops/blob/master/examples/minmax.toml)
- [Static](https://github.com/antdavidlima/btops/blob/master/examples/static.toml)

## Configuration

btops supports config files in toml, json, and yaml format. It'll look in the following places for config files:

```
$XDG_CONFIG_HOME/btops/config.*
~/.config/btops/config.*
```

Below are the different configuration options available. Please look at [examples](https://github.com/antdavidlima/btops/tree/master/examples) for example usage

### Configuration Options

| Option               | Type     | Description                                                                                                                                    | Default     |
| -------------------- | -------- | ---------------------------------------------------------------------------------------------------------------------------------------------- | ----------- |
| min                  | Int      | Minimum number of desktops per monitor                                                                                                         | 1           |
| max                  | Int      | Maximum number of desktops per monitor                                                                                                         | infinity    |
| remove-empty         | Bool     | Removes empty desktops                                                                                                                         | true        |
| remove-focused       | Bool     | Removes focused desktops                                                                                                                       | true        |
| append-when-occupied | Bool     | Appends a new desktop when all other desktops are occupied                                                                                     | true        |
| watch-config         | Bool     | Reload btops on next event when configuration changes                                                                                          | true        |
| renamers             | []String | Order of [renamers](#renamers) to use for renaming desktops. If a given renamer is unable to rename a desktop, it cascades to the next renmaer | ["numeric"] |
| names                | Names    | [Names configuration object](#names)                                                                                                           | {}          |

### Renamers

| Name       | Description                                                                           |
| ---------- | ------------------------------------------------------------------------------------- |
| numeric    | Names desktops numerically in increasing order. e.g. 1, 2, 3, 4...                    |
| constant   | Names desktops using the "constant" option in the Names object                        |
| static     | Names desktops according to the static names array                                    |
| client     | Names desktops as a space separated string of opened clients                          |
| classified | Names desktops using the matched classification of opened clients in the names object |

### Names

names configuration object

| Option     | Type                                     | Description                                                                                                                                                  |
| ---------- | ---------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| constant   | String                                   | A single string that the constant renamer uses to rename desktops                                                                                            |
| static     | []String                                 | A list of desktop names that the static renamer uses to rename desktops                                                                                      |
| classified | []{ classification: []String (clients) } | An array of objects that match client names with a given classification. If multiple classifications are matched, the first will be used as the desktop name |

## Installation

- Ensure [Go](https://go.dev/) is installed and your [$GOPATH](https://go.dev/wiki/GOPATH) is set
- `go install github.com/antdavidlima/btops@latest`
- run `$GOPATH/bin/btops`

### Arch Linux

[btops-git](https://aur.archlinux.org/packages/btops-git/) is available in the aur
