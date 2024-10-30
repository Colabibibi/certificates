# Xcode 项目证书和配置文件同步指南

本文档详细说明如何清空 Xcode 项目的本地证书和配置文件，并通过 `fastlane` 重新同步最新的证书。适用于重新配置证书或在新的开发环境中设置证书的情况。

## 前提条件

- 您的项目已经配置了 `fastlane`。
- 具有 `Apple Developer` 账号和对应的 API Key。
- `Matchfile` 和 `Fastfile` 配置正确。

---

## 操作步骤

### 1. 安装 `fastlane`

如果您的系统尚未安装 `fastlane`，请在终端中运行以下命令以进行安装：

```bash
sudo gem install fastlane -NV
```

安装完成后，通过以下命令验证 `fastlane` 是否成功安装：

```bash
fastlane --version
```

### 2. 清空本地证书和配置文件

为确保同步的文件是最新的，请先清空本地证书和配置文件。

- **删除 `fastlane` 缓存的本地证书和配置文件**：

```bash
rm -rf ~/.fastlane
```

- **删除项目本地的旧 `certificates` 文件夹（可选）**：

```bash
rm -rf ./fastlane/certificates
```

- **删除 Xcode 的 `Provisioning Profiles`**：

```bash
rm -rf ~/Library/MobileDevice/Provisioning\ Profiles/*
```

### 3. 导航到项目的 `fastlane` 文件夹

在终端中进入 iOS 项目的 `fastlane` 文件夹：

```bash
cd path/to/your/project/ios
```

### 4. 执行 `fastlane match_all` 同步证书和配置文件

运行以下命令同步 `development` 和 `adhoc` 证书和配置文件到本地：

```bash
fastlane match_all
```

此操作将从远程 `match` Git 仓库下载 `development` 和 `adhoc` 类型的证书，并将它们安装到本地，以供 Xcode 使用。

---

## 配置示例

### Matchfile 配置示例

确保您的 `Matchfile` 正确配置了 Git 仓库和应用标识符：

```ruby
git_url("git@github.com:yourusername/your-certificates-repo.git")
app_identifier(["com.yourcompany.yourapp"])
type("development", "adhoc")
```


## 完成验证

执行 `fastlane match_all` 后，打开 Xcode 并确认项目的 **Signing & Capabilities** 中已选择正确的 `Provisioning Profiles`，并确保项目可以正常编译和运行。

通过上述步骤，您已成功同步最新的 `development` 和 `adhoc` 配置文件和证书，从而保证项目的签名设置与远程仓库一致。

---
