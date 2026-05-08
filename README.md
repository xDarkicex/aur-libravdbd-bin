# aur-libravdbd-bin

Arch Linux User Repository (AUR) package for **libravdbd-bin** — prebuilt binary of the libravdbd daemon.

---

## Package Details

| Attribute | Value |
|------:|------|
| **Package** | libravdbd-bin |
| **Version** | **1.4.25** (latest) |
| **Architecture** | x86_64, aarch64 |
| **License** | Proprietary (see upstream) |
| **Provides** | libravdbd |
| **Conflicts** | libravdbd (from source) |
| **Binary Source** | [homebrew-openclaw-libravdb-memory/releases](https://github.com/xDarkicex/homebrew-openclaw-libravdb-memory/releases) |

### Binary Artifacts

| Target | URL |
|------|---|
| amd64 | `libravdbd-linux-amd64` |
| arm64 | `libravdbd-linux-arm64` |

Artifacts are fetched at build time from the upstream release channel, tagged by version.

### SHA256 Checksums (v1.4.25)

| File | SHA256 |
|------|---|
| `libravdbd-linux-amd64` | `d9f07945bd8657d7104c2282b59d05b9fecd9a59e112b4174e87cd9db8d015cc` |
| `libravdbd-linux-arm64` | `4ba911a82ddf0deffc762e8cc46a04992e4f89b1c2ddb113cb58ef6d05bb24a3` |
| `provision.sh` | `28c66f8cbda906cc07116e39377957af93df29c055e5bdc28396d183d57df29d` |

---

## Installation

### From AUR (recommended)

```bash
# Using an AUR helper (yay, paru, etc.)
yay -S aur-libravdbd-bin

# Or manually
git clone https://github.com/JuanHuaXu/aur-libravdbd-bin.git
cd aur-libravdbd-bin
makepkg -si
```

### Manual PKGBUILD

```bash
# Clone this repo
git clone https://github.com/JuanHuaXu/aur-libravdbd-bin.git
cd aur-libravdbd-bin

# Build and install
makepkg -si
```

---

## Usage

### Start the daemon

```bash
# Start (user service)
systemctl --user start libravdbd

# Check status
systemctl --user status libravdbd

# Enable auto-start
systemctl --user enable libravdbd
```

### Provision ML Models

The daemon ships without bundled models or ONNX Runtime. Install them after the daemon:

```bash
sudo /usr/lib/libravdbd/provision.sh --target /var/lib/libravdbd
```

### Configuration

Environment variables can be set via:

```bash
# /etc/libravdbd/env (optional)
LIBRAVDB_RPC_ENDPOINT=unix:%h/.clawdb/run/libravdb.sock
LIBRAVDB_DB_PATH=%h/.clawdb/data.libravdb
LIBRAVDB_MODEL_PATH=/var/lib/libravdbd/models
```

Or directly in the service unit.

---

## Installed Files

| Path | Description |
|------|------|
| `/usr/bin/libravdbd` | Main daemon binary |
| `/usr/lib/libravdbd/provision.sh` | ML model provisioning script |
| `/usr/lib/systemd/user/libravdbd.service` | User systemd service unit |

---

## Service Unit

The included `libravdbd.service` defines:

- **ExecStart**: `/usr/bin/libravdbd serve`
- **Restart**: on-failure with 5s delay
- **After**: `network.target`
- **WantedBy**: `default.target`

---

## About LibraVDB

**libravdbd** is the daemon layer for [LibraVDB](https://github.com/xDarkicex/libravdb), the core vector database library.

### LibraVDB Library

| Attribute | Value |
|------|---|
| **Language** | Go (1.25+) |
| **License** | Apache 2.0 |
| **Current version** | 1.0.0 |
| **Repository** | [xDarkicex/libravdb](https://github.com/xDarkicex/libravdb) |

### Core Features

- **Multiple Index Types**: HNSW, IVF-PQ, and Flat algorithms with automatic selection
- **Advanced Quantization**: Product Quantization (8x compression) and Scalar Quantization (4x)
- **Rich Metadata Filtering**: Complex AND/OR/NOT operations with type-safe schemas
- **Streaming Operations**: High-throughput batch processing with backpressure control
- **Memory Management**: Configurable limits, memory mapping (mmap), and automatic optimization
- **Persistent Storage**: Single-file binary persistence with WAL-backed durability and reopen/rebuild support
- **Write Concurrency**: Phase 1 bounded write admission for batch/streaming writers
- **Observability**: Prometheus metrics, health checks, and distributed tracing
- **Built-in Error Recovery**: Circuit breakers, graceful degradation, automatic recovery orchestration

### libravdbd Integration

The daemon exposes libravdb's capabilities via:

- **RPC interface** — remote vector operations (search, insert, delete, query)
- **ML embeddings** — ONNX Runtime-powered text/vector generation
- **Summarization** — automatic text summarization endpoints
- **Model provisioning** — `provision.sh` handles downloading and configuring ML models
- **Zero-config** — sensible defaults with `systemctl --user` lifecycle management

---

## Version History

| Version | Notes |
|---|---|
| **1.4.25** | Latest release — latest daemon binary |
| 1.4.24 | Previous release |
| 1.4.23 | Previous release |
| ... | ... |
| 1.4.17 | Earliest available |

---

*This repository provides a convenience AUR package for Arch Linux users. The libravdbd daemon is licensed separately — see the upstream [LibraVDB](https://github.com/xDarkicex/libravdb) project for library details.*
