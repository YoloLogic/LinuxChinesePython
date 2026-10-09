# LinuxChinesePython（Linux 直接可用版）

**说中文的 Python**：中文关键字 + 中文标准库 API + 中文报错显示层；与英文**可混写**，英文原名一直可用。
本包是 **ChinesePython 0.1.1** 的 **Linux x86-64 直接可用构建**，与 Windows 版**同一份源码**
（身份 `73da4c3ea6fe6978…`，`./bin/python3 --build-info` 可自查）。

## 直接就用

```bash
tar xzf LinuxChinesePython-0.1.1-linux-x86_64.tar.gz
cd LinuxChinesePython-0.1.1-linux-x86_64
./bin/python3                    # 进中文 REPL（退出：Ctrl+D）
./bin/python3 你的脚本.py         # 跑脚本
./bin/pip3 install 包名          # 装第三方库（第三方库本身仍是英文 API）
```
想全局敲 `python`：把 `<解包目录>/bin` 加进 `PATH`，或
`ln -s <解包目录>/bin/python3 ~/.local/bin/python3`。

## 运行要求（重要）

* **glibc ≥ 2.39** —— 本包在 **Ubuntu 24.04** 上构建。Ubuntu 24.04+ / Debian 13+ / Fedora 40+ 等较新发行版可直接用；
  **Ubuntu 22.04、Debian 12 等较老系统跑不了**，那些系统请从源码构建（见下）。
* 解释器本体只依赖 **libc / libm**（libpython 静态链进 `bin/python3`，所以整目录搬走也能跑）。
* 扩展模块用到系统里这些常见库：`libssl3`/`libcrypto3`、`libbz2`、`liblzma`、`libsqlite3`、`libffi`、
  `libexpat`、`zlib`、`libzstd`、`libreadline`/`libncursesw`、`libdb`、`libgdbm`、**系统 tcl/tk 8.6**（tkinter 用）
  与若干 X11 库（无桌面的服务器上 tkinter 用不了，属正常）。

## 与 Windows 版的差别

| | Windows 版 | 本包 |
|---|---|---|
| 形态 | 绿色目录 + **两个单文件 exe** + 一键安装 + 代码签名 | 解包即用的目录（`bin/python3`）|
| 图形界面 | 自带 Tcl/Tk 9 | 用**系统** tcl/tk 8.6 |
| 官方测试套 | 带（`Lib\test`）| **不带**（要跑请用源码构建）|
| 静态库 | 带 `libs/python314.lib` | 不带 `libpython3.14.a`（要嵌入/静态链接请用源码构建）|

其余（中文关键字、**157 个中文库**、中文报错三档、`--build-info` 身份、`pip` 预装）一致。

## 从源码自己构建（其它发行版 / 其它架构）

```bash
sudo apt install build-essential zlib1g-dev libffi-dev libssl-dev libbz2-dev \
     liblzma-dev libreadline-dev libsqlite3-dev uuid-dev libdb-dev libgdbm-dev tk-dev libzstd-dev
bash tools/linux/构建并冒烟.sh        # 配置 + 构建 + 冒烟 + 判据
```
（脚本在开发仓里；本仓只放给你直接用的东西。）

## 许可与再分发

* ✅ **能用它写程序卖钱**：用它开发、运行、发布、销售**你自己的程序** —— 个人或公司、开源或闭源都行；
  **产出完全归使用者**，本许可不附加任何条件；
* ❌ **不许重新打包发布**：不得把本发行包（或修改版）重新打包、改名换标、上架、随产品/硬件捆绑，
  或当付费服务提供（除事先取得作者书面许可，QQ 1396257961）；
* ✅ **非营利、原封不动地整体转发可以**（教学 / 社团 / 非营利镜像；四个条件：一个字节不改 /
  不收费不带广告 / 不暗示是自己的 / 保留官方来源链接）；
* ❌ **名字不能用**：不得用 `ChinesePython` / `LinuxChinesePython` 的名称与图标发布衍生版本
  （即使尚未注册商标，这条作为许可条款同样有效）。

正文见 `LICENSE`，范围判定见 `LICENSE-SCOPE.md`，名称条款见 `TRADEMARK.md`，第三方披露见 `NOTICE.txt`。
派生自 **CPython 3.14.7** 的部分按 **PSF 许可**（`LICENSE-PSF.txt`，逐字节未改）。
这是 **source-available（源码可见）**，**不是** OSI 意义上的开源。

## 身份自查

```bash
./bin/python3 --build-info     # 改动文件联合哈希（唯一身份）+ 版本 + 两仓 HEAD
```

> ⚠ GitHub 的 **Assets 区块默认可能是折叠的** —— 看不到附件时点一下「Assets」。
