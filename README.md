<h1>WPI i.MX Repo Manifest README</h1>

<a>此資源庫是基於 [NXP i.MX Linux BSP Software \[imx-manifest\]](https://github.com/nxp-imx/imx-manifest) 並加上 WPI 客製化 Layer 所建立而成，用於下載各種 WPI i.MX BSP 版本的 manifest。</a>

<a>各個分支都是根據 Linux 的版本去命名的，例如：``imx-linux-kirkstone`` 內的 manifest 都會跟 ``Kirkstone`` 版本相關，其他具體說明則會包含在分支內的 README</a>


* i.MX Linux Yocto Project 釋出的分支皆會以 ``imx-linux-`` 作為前綴詞

## 安裝 ``repo`` 

為了透過 manifest 去下載所有需要的資源，``repo`` 是必須安裝的。

```!
$ mkdir ~/bin
$ curl http://commondatastorage.googleapis.com/git-repo-downloads/repo > ~/bin/repo
$ chmod a+x ~/bin/repo
$ PATH=${PATH}:~/bin
```

## 下載 Yocto Project BSP

```!
$ mkdir <release>
$ cd <release>
$ repo init -u https://github.com/nxp-imx/imx-manifest -b <branch name> [ -m <release manifest>]
$ repo sync
```

各個分支內的 README 會包含相應的指令範例。

## 範例

下載 5.15.71-2.2.0 版本

```!
$ repo init -u https://github.com/WPI-ATU/wpi-manifest.git -b imx-linux-kirkstone -m imx-5.15.71-2.2.0.xml
```

## 建立編譯環境

這主要是說明建立環境編譯時的參數。

```!
$ [MACHINE=<machine>] [DISTRO=fsl-imx-<backend>] source ./imx-setup-release.sh -b bld-<backend>

<machine>   defaults to `imx6qsabresd`
<backend>   Graphics backend type
    xwayland    Wayland with X11 support - default distro
    wayland     Wayland
    fb          Framebuffer (not supported for mx8)
```

Example:

* 建立 OP-Killer 編譯環境 (XWayland)

```!
$ DISTRO=fsl-imx-xwayland MACHINE=opkiller source imx-setup-release.sh -b build
```

## 建立映像檔

```
$ bitbake <image recipe>
```

WPI 常用的映像檔選項

| \<image recipe\> | 說明 |
| - | - |
| imx-image-core | 最基本的開機檔案 |
| imx-image-multimedia | 具備 GUI 並包含多媒體工具 |
| imx-image-full | 具備 GUI、多媒體工具、QT 及 Machine Learning 所需的函式庫 |

## ATU Support

* [NXP i.MX8 大大通技術索引](https://hackmd.io/@WPI-ATU-TW1/Bk3zvW0Ts/https%3A%2F%2Fhackmd.io%2FXC9STgFjSs6_vadDkO0YSA%3Fboth?utm_source=preview-mode&utm_medium=rec)

<img src="https://hackmd.io/_uploads/Hy773SVvn.png"  width="200" height="200">

如果你有任何需求，請聯絡 WPI 的 [TW ATU](mailto:wpi.atu.github@wpi-group.com) 團隊
