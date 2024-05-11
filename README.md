<p align="center">
  <a href="https://solana.com">
    <img alt="Solana" src="https://i.imgur.com/0vfIMHo.png" width="250" />
  </a>
</p>

[![Solana crate](https://img.shields.io/crates/v/solana-core.svg)](https://crates.io/crates/solana-core)
[![Solana documentation](https://docs.rs/solana-core/badge.svg)](https://docs.rs/solana-core)
[![Build status](https://badge.buildkite.com/8cc350de251d61483db98bdfc895b9ea0ac8ffa4a32ee850ed.svg?branch=master)](https://buildkite.com/solana-labs/solana/builds?branch=master)
[![codecov](https://codecov.io/gh/solana-labs/solana/branch/master/graph/badge.svg)](https://codecov.io/gh/solana-labs/solana)

# 构建

## **1. 安装 rustc, cargo 和 rustfmt。**

```bash
$ curl https://sh.rustup.rs -sSf | sh
$ source $HOME/.cargo/env
$ rustup component add rustfmt
```

构建 master 分支时，请确保通过运行以下命令使用最新的稳定 Rust 版本：

```bash
$ rustup update
```

构建特定发布分支时，应检查 `ci/rust-version.sh` 中的 Rust 版本，如有必要，通过运行以下命令安装该版本：

```bash
$ rustup install VERSION
```
请注意，如果这不是您机器上的最新 Rust 版本，可能需要使用 [override](https://rust-lang.github.io/rustup/overrides.html) 以确保使用正确的版本。

在 Linux 系统上，您可能需要安装 libssl-dev, pkg-config, zlib1g-dev, protobuf 等。

在 Ubuntu 上：

```bash
$ sudo apt-get update
$ sudo apt-get install libssl-dev libudev-dev pkg-config zlib1g-dev llvm clang cmake make libprotobuf-dev protobuf-compiler
```

在 Fedora 上：

```bash
$ sudo dnf install openssl-devel systemd-devel pkg-config zlib-devel llvm clang cmake make protobuf-devel protobuf-compiler perl-core
```

## **2. 下载源代码。**

```bash
$ git clone https://github.com/foxxcn/agave.git
$ cd agave
```

## **3. 构建。**

```bash
$ ./cargo build
```

# 测试

**运行测试套件：**

```bash
$ ./cargo test
```

### 启动本地测试网

在本地启动您自己的测试网，具体操作请参见[在线文档](https://docs.solanalabs.com/clusters/benchmark)。

### 访问远程开发集群

* `devnet` - 稳定的公共开发集群，通过 devnet.solana.com 访问。全天候运行。了解更多关于[公共集群](https://docs.solanalabs.com/clusters)的信息。

# 基准测试

首先，安装 Rustc 的夜间构建版本。`cargo bench` 需要使用仅在夜间构建中可用的不稳定功能。

```bash
$ rustup install nightly
```

运行基准测试：

```bash
$ cargo +nightly bench
```

# 发布流程

该项目的发布流程在[此处](RELEASE.md)描述。

# 代码覆盖率

生成代码覆盖率统计：

```bash
$ scripts/coverage.sh
$ open target/cov/lcov-local/index.html
```

为什么强调覆盖率？虽然大多数人将覆盖率视为代码质量指标，我们主要将其视为开发者生产力指标。当开发者对代码库进行更改时，通常是为了解决某个问题。我们的单元测试套件是我们编码解决代码库问题的方式。运行测试套件应表明您的更改没有侵犯其他人的解决方案。添加测试可以保护您的解决方案免受未来更改的影响。如果您不明白为什么存在某行代码，尝试删除它并运行单元测试。最近的测试失败应告诉您该代码解决了什么问题。如果没有测试失败，那么提交一个 Pull Request，询问“这段代码解决了什么问题？”另一方面，如果测试失败，并且您能想到一个更好的解决同一问题的方法，一个包含您解决方案的 Pull Request 无疑非常受欢迎！同样，如果重写测试能更好地传达它保护的代码，请向我们发送该补丁！