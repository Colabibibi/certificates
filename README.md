Xcode 项目证书和配置文件同步指南
本文档详细说明如何清空 Xcode 项目的本地证书和配置文件，并通过 fastlane 重新同步最新的证书。适用于重新配置证书或在新的开发环境中设置证书的情况。

前提条件
您的项目已经配置了 fastlane。
具有 Apple Developer 账号和对应的 API Key。
Matchfile 和 Fastfile 配置正确。
操作步骤
1. 安装 fastlane
如果您的系统尚未安装 fastlane，请在终端中运行以下命令以进行安装：

bash
复制代码
sudo gem install fastlane -NV
安装完成后，通过以下命令验证 fastlane 是否成功安装：

bash
复制代码
fastlane --version
2. 清空本地证书和配置文件
为确保同步的文件是最新的，请先清空本地证书和配置文件。

删除 fastlane 缓存的本地证书和配置文件：
bash
复制代码
rm -rf ~/.fastlane
删除项目本地的旧 certificates 文件夹（可选）：
bash
复制代码
rm -rf ./fastlane/certificates
删除 Xcode 的 Provisioning Profiles：
bash
复制代码
rm -rf ~/Library/MobileDevice/Provisioning\ Profiles/*
3. 导航到项目的 fastlane 文件夹
在终端中进入 iOS 项目的 fastlane 文件夹：

bash
复制代码
cd path/to/your/project/ios/fastlane
4. 执行 fastlane match_all 同步证书和配置文件
运行以下命令同步 development 和 adhoc 证书和配置文件到本地：

bash
复制代码
fastlane match_all
