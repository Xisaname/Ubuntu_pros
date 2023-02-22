# Ubuntu_pros
Note the problems and the resolutions while using Ubuntu(20.04):)

# GPG keys error
- [Ubuntu\_pros](#ubuntu_pros)
- [GPG keys error](#gpg-keys-error)
  - [问题描述](#问题描述)
  - [解决方法](#解决方法)
  - [注意](#注意)

## 问题描述
首先在使用`sudo apt(-get) update`命令更新软件缓存时，出现了以错误：

`W: GPG错误: https://storage.googleapis.com/bazel-apt stable InRelease: 由于没有公钥，无法验证下列签名: NO_PUBKEY 3D5919B448457EE0`

`E: 仓库“https://storage.googleapis.com/bazel-apt stable InRelease”没有数字签名。`

## 解决方法
首先要明确一点，这个3D开头的GPG签名是通用的，网上有很多用的其他的公钥，那是其他网站所对应的因此在进行操作时，只需要针对上述公钥即可。

上述数字签名的公钥在`http://bazel.build/bazel-release.pub.gpg`

需要额外注意的是，该密钥文件需要下载下来，不能自己创建一个密钥文件然后将密钥复制进去，这样不起作用。

具体的操作方式为：
`curl -fsSL https://storage.googleapis.com/www.bazel.build/bazel-release.pub.gpg | gpg --dearmor >bazel-archive-keyring.gpg`

`mv bazel-archive-keyring.gpg /usr/share/keyrings/`

在执行完上述命令后，需要检查一下`/usr/share/keyrings/`下`bazel-archive-keyring.gpg`文件是否为乱码，如果不是乱码或者为空，则失败，需要重新进行上述操作。

## 注意
网上针对此类问题大多的解决方法是往keyserver中添加签名，但本文遇到的问题并不能用上述方法解决。