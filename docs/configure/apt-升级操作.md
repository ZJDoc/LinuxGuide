
# [apt]升级操作

使用工具`apt`进行应用升级，以`VSCode`为例

## 查询

查询指定应用的升级信息

```
$ apt list --upgradable | grep code

WARNING: apt does not have a stable CLI interface. Use with caution in scripts.

chromium-codecs-ffmpeg-extra/bionic-security,bionic-updates 79.0.3945.79-0ubuntu0.18.04.1 amd64 [可从该版本升级：78.0.3904.108-0ubuntu0.18.04.1]
code/stable 1.41.1-1576681836 amd64 [可从该版本升级：1.40.2-1574694120]
intel-microcode/bionic-security,bionic-updates 3.20191115.1ubuntu0.18.04.2 amd64 [可从该版本升级：3.20191115.1ubuntu0.18.04.1]
libnvidia-decode-440/bionic 440.44-0ubuntu0~0.18.04.1 amd64 [可从该版本升级：440.26-0ubuntu0~gpu18.04.2]
libnvidia-encode-440/bionic 440.44-0ubuntu0~0.18.04.1 amd64 [可从该版本升级：440.26-0ubuntu0~gpu18.04.2]
```

从中可发现`vscode`可以从当前的`1.40.2-1574694120`升级到`1.41.1-1576681836`

## 升级

升级全部的应用

```
$ sudo apt upgrade
```

升级指定的应用

```
$ sudo apt install code
正在读取软件包列表... 完成
正在分析软件包的依赖关系树       
正在读取状态信息... 完成       
下列软件包是自动安装的并且现在不需要了：
  fcitx-libs fonts-liberation2 fonts-opensymbol gstreamer1.0-gtk3 libabw-0.1-1 libboost-date-time1.65.1 libboost-filesystem1.65.1 libboost-iostreams1.65.1
  libboost-locale1.65.1 libcdr-0.1-1 libclucene-contribs1v5 libclucene-core1v5 libcmis-0.5-5v5 libcolamd2 libe-book-0.1-1 libeot0 libepubgen-0.1-1 libetonyek-0.1-1
  libexttextcat-2.0-0 libexttextcat-data libfcitx-qt0 libfreehand-0.1-1 liblangtag-common liblangtag1 libllvm8 libmhash2 libmspub-0.1-1 libmwaw-0.3-3 libmythes-1.2-0
  libneon27-gnutls libodfgen-0.1-1 libopencc2 libopencc2-data liborcus-0.13-0 libpagemaker-0.0-0 libqt4-opengl libqtwebkit4 libraptor2-0 librasqal3 librdf0 librevenge-0.0-0
  libsuitesparseconfig5 libvisio-0.1-1 libwpd-0.10-10 libwpg-0.3-3 libwps-0.4-4 libxmlsec1 libxmlsec1-nss libyajl2 lp-solve uno-libs3 ure
使用'sudo apt autoremove'来卸载它(它们)。
下列软件包将被升级：
  code
升级了 1 个软件包，新安装了 0 个软件包，要卸载 0 个软件包，有 94 个软件包未被升级。
需要下载 57.5 MB 的归档。
解压缩后会消耗 5,707 kB 的额外空间。
```