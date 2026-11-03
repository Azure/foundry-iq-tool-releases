# Foundry IQ tool releases

This repository hosts release packages for **TopicGraph** (`topicgraph`), a command-line tool that
builds a topic graph from an Azure AI Search vector index.

> **Download the packages from the _Assets_ list of a [release](../../releases).**
> The automatic "Source code (zip)" and "Source code (tar.gz)" links that GitHub adds to every
> release contain only this repository's files, not the tool. Please ignore them.

## Packages

Each release has one package per platform. `<version>` is the release version, for example `1.0.0`.

| Platform | Architecture | File |
|---|---|---|
| Windows | x64, arm64 | `topicGraphBuildTool-<version>-win-<arch>.zip` |
| Linux (Debian, Ubuntu) | x64, arm64 | `topicGraphBuildTool-<version>-linux-<arch>.deb` |
| Linux (RHEL, Fedora, other RPM) | x64, arm64 | `topicGraphBuildTool-<version>-linux-<arch>.rpm` |
| macOS | x64, arm64 | `topicGraphBuildTool-<version>-osx-<arch>.zip` |

Each release also has `release.json`, which lists the version, the source commit, and the SHA-256
of every package.

## Verify a download

Compare the SHA-256 of the file you downloaded with its entry in `release.json` (under `artifacts`).

```powershell
# Windows
(Get-FileHash .\topicGraphBuildTool-<version>-win-x64.zip -Algorithm SHA256).Hash.ToLower()
```

```bash
# Linux or macOS
sha256sum topicGraphBuildTool-<version>-linux-x64.deb      # Linux
shasum -a 256 topicGraphBuildTool-<version>-osx-arm64.zip  # macOS
```

The packages are signed: the Windows executable is Authenticode-signed, the macOS executable is
Developer ID-signed, and the Linux `.deb` and `.rpm` packages are PGP-signed.

## Install and run

**Windows:** extract the zip, then run `topicgraph.exe`.

**Debian or Ubuntu:**

```bash
sudo apt install ./topicGraphBuildTool-<version>-linux-<arch>.deb
```

**RHEL, Fedora, or another RPM-based distribution:**

```bash
sudo dnf install ./topicGraphBuildTool-<version>-linux-<arch>.rpm
```

**macOS:** extract the zip and restore the execute permission, which zip extraction does not
preserve:

```bash
unzip topicGraphBuildTool-<version>-osx-<arch>.zip
chmod 0755 ./topicgraph
```

Then create a `config.json` (a template is packaged with the tool), configure authentication, and run:

```bash
topicgraph preflight --config ./config.json
topicgraph build --config ./config.json --fresh
```

Do not store credentials in `config.json`. Use an Entra access token (`TOPICGRAPH_SEARCH_TOKEN`) or
an existing Azure CLI login.

## Support

<!-- Add the team contact or documentation link before publishing. -->
