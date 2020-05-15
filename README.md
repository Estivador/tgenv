# Terragrunt Version Manager (tgenv)
[![Build Status](https://travis-ci.com/Estivador/tgenv.svg?branch=master)](https://travis-ci.com/Estivador/tgenv)

[Terragrunt](https://github.com/gruntwork-io/terragrunt) version manager inspired by [tfenv](https://github.com/kamatama41/tfenv)

[Origin](https://github.com/sigsegv13/tgenv) of my version of `tgenv`.

## Support
Currently tgenv supports the following OSes
- Mac OS X (64bit)
- Linux (64bit)

## Installation
### Automatic
Install via [Homebrew](https://docs.brew.sh/Installation)

  ```console
  $ brew tap Estivador/tgenv
  $ brew install tgenv
  ```

Note: The Hombrew tap is maintained [here: Estivador/homebrew-tgenv](https://github.com/Estivador/homebrew-tgenv)

### Manual

1. Check out tgenv into any path (here is `${HOME}/.tgenv`)

  ```console
  $ git clone https://github.com/Estivador/tgenv.git ~/.tgenv
  ```

2. Add `~/.tgenv/bin` to your `$PATH` any way you like

  ```console
  $ echo 'export PATH="$HOME/.tgenv/bin:$PATH"' >> ~/.bash_profile
  ```

  OR you can make symlinks for `tgenv/bin/*` scripts into a path that is already added to your `$PATH` (e.g. `/usr/local/bin`) `OSX/Linux Only!`

  ```console
  $ ln -s ~/.tgenv/bin/* /usr/local/bin
  ```

  On Ubuntu/Debian touching `/usr/local/bin` might require sudo access, but you can create `${HOME}/bin` or `${HOME}/.local/bin` and on next login it will get added to the session `$PATH`
  or by running `. ${HOME}/.profile` it will get added to the current shell session's `$PATH`.

  ```console
  $ mkdir -p ~/.local/bin/
  $ . ~/.profile
  $ ln -s ~/.tgenv/bin/* ~/.local/bin
  $ which tgenv
  ```

## Usage
### tgenv install [version]
Install a specific version of Terragrunt.  Available options for version:
- `i.j.k` exact version to install
- `latest` is a syntax to install latest version
- `latest:<regex>` is a syntax to install latest version matching regex (used by grep -e)
- `min-required` is currently not supported as it is not yet a feature of Terragrunt. See [Ensure minimum Terragrunt version #182](https://github.com/gruntwork-io/terragrunt/issues/182).

```console
$ tgenv install 0.23.14
$ tgenv install latest
$ tgenv install latest:^0.23
$ tgenv install
```

If `shasum` is present in the path, `tgenv` will verify the download against Gruntwork's published sha256 hash.

> Note: As of v0.18.1 Gruntwork provides signature verification. If you want to install older version, please set the envvar `TGENV_IGNORE_SHA` with any value. E.g. `export TGENV_IGNORE_SHA=1`

#### .terragrunt-version
If you use [.terragrunt-version](#terragrunt-version), `tgenv install` (no argument) will install the version written in it.

#### min-required
Currently not supported as it is not yet a feature of Terragrunt. See [Ensure minimum Terragrunt version #182](https://github.com/gruntwork-io/terragrunt/issues/182) to voice your support for this feature or even contribute to help make it happen.

### tgenv use &lt;version>
Switch a version to use

`latest` is a syntax to use the latest installed version

`latest:<regex>` is a syntax to use latest installed version matching regex (used by grep -e)

```console
$ tgenv use 0.23.14
$ tgenv use latest
$ tgenv use latest:^0.23
```

### tgenv uninstall &lt;version>
Uninstall a specific version of terragrunt
`latest` is a syntax to uninstall latest version
`latest:<regex>` is a syntax to uninstall latest version matching regex (used by grep -e)

```console
$ tgenv uninstall 0.23.14
$ tgenv uninstall latest
$ tgenv uninstall latest:^0.23
```

### tgenv list
List installed versions

```console
% tgenv list
* 0.23.14 (set by /opt/tgenv/version)
  0.22.5
  0.21.13
  0.20.5
```

### tgenv list-remote
List the 20 most recent installable versions

```console
% tgenv list-remote
0.23.14
0.23.13
0.23.12
0.23.11
0.23.10
0.23.9
0.23.8
0.23.7
0.23.6
0.23.5
0.23.4
0.23.3
0.23.2
0.23.1
0.23.0
0.22.5
0.22.4
0.22.3
0.22.2
0.22.1
0.22.0
```

### tgenv list-remote-all
List all of the installable versions

```console
% tgenv list-remote-all
0.23.14
0.23.13
0.23.12
0.23.11
0.23.10
0.23.9
0.23.8
0.23.7
0.23.6
0.23.5
0.23.4
0.23.3
0.23.2
0.23.1
0.23.0
0.22.5
0.22.4
0.22.3
0.22.2
0.22.1
0.22.0
...
```

## .terragrunt-version
If you put `.terragrunt-version` file on your project root, or in your home directory, tgenv detects it and uses the version written in it. If the version is `latest` or `latest:<regex>`, the latest matching version currently installed will be selected.

```console
$ tgenv list
  0.23.14
  0.22.5
  0.21.13
* 0.20.5 (set by /home/user/.terragrunt-version)

$ cat .terragrunt-version
0.20.5

$ terragrunt --version
terragrunt version v0.20.5

$ echo 0.23.14 > .terragrunt-version

$ terragrunt --version
terragrunt v0.23.14

$ echo latest:^0.22 > .terragrunt-version

$ terragrunt --version
terragrunt v0.22.5
```

## Upgrading
### Automatic
Upgrading via Homebrew

```console
$ brew update                    # Updates the tap
$ brew upgrade tgenv             # Upgrades the app
```

### Manual

```console
$ git --git-dir=~/.tgenv/.git pull
```

## Uninstalling
### Automatic
Uninstalling via Homebrew

```sh
$ brew uninstall tgenv        # Uninstalls tgenv and associated Terragrunt release(s)
$ brew untap Estivador/tgenv  # Removes the tap
```

### Manual

```console
$ rm -rf /some/path/to/tgenv
```

## LICENSE
- [tgenv](https://github.com/Estivador/tgenv/blob/master/LICENSE) : My version of `tgenv`
- [tgenv source](https://github.com/cunymatthieu/tgenv/blob/master/LICENSE) : Origin of my version of `tgenv`
- [tfenv](https://github.com/kamatama41/tgenv/blob/master/LICENSE) : `tgenv` is based on `tfenv`'s source code
