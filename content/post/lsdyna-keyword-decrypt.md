---
title: "LSDYNA K文件加密与解密技术"
date: 2020-05-13T21:15:15+08:00
lastmod: 2020-05-13T21:15:15+08:00
#draft: true
keywords: []
description: "LS-DYNA k文件加密与解密"
tags: ["ls-dyna", ""]
categories: ["CAE技术"]
author: "J哥"

# You can also close(false) or open(true) something for this content.
# P.S. comment can only be closed
# comment: false
toc: false
autoCollapseToc: false
postMetaInFooter: false
hiddenFromHomePage: false
# You can also define another contentCopyright. e.g. contentCopyright: "This is another copyright."
# contentCopyright: false
reward: false
mathjax: false
mathjaxEnableSingleDollar: false
mathjaxEnableAutoNumber: false

# You unlisted posts you might want not want the header or footer to show
hideHeaderAndFooter: false

# You can enable or disable out-of-date content warning for individual post.
# Comment this out to use the global config.
#enableOutdatedInfoWarning: false

flowchartDiagrams:
  enable: false
  options: ""

sequenceDiagrams: 
  enable: false
  options: ""

---
按照下述步骤进行LS-DYNA k文件的加密操作:

首先, 你需要安装免费的GPG加密软件. 假如你使用的是Linux系统，大概率已经预装了.  如果不是，可以访问www.gnupg.org获取。

接着, 你需要将下面的LSTC public key导入GPG加密软件。复制包括`-----BEGIN` 和 `-----END` 之间的所有字符到文本文件并保存。导入命令为`gpg --import <filename>`, `<filename\>` 是保存public key的文件名。
```
-----BEGIN PGP PUBLIC KEY BLOCK-----
Version: GnuPG v2.0.19 (GNU/Linux)

mQGiBFM61ScRBACgqz7q7kytYuuRpa+1DTD9J3Kn8s3kMHO7zPtLu8bsb1L1I4UQ
CC6HRL2fMVRtBQZuy445eqsot5npcnzpQ6rcvsQZTVCqXH/gx5O5xs6/W8ktaJXn
hBrxGabk6IzlOXYvmQ2+jOATfQs29pt4+e/+oXFI9EfKBHao2dEgtOWS6wCg+9gi
9azFZOUIHV0EJDPFQJZrRFUD/11AG23e7964MN0HTWAWCIvPs8johwB7NOF6UjRR
xuqD/ZqiQ1hhmQzJR89Weg0TeFFCVP+yK2tgPOgsXry/r7WF/RnO9S/7yvtTWHr8
QPVxCur7vcKX/Lis6ByiyyDvihavBB6RgMYl5HkrEstTY/j3O09woxtQ4Pae5yZ2
woj0BACI87Lk6aO/9wAVXBDYyufqX9bea/lbMEuQZ7qzBO7xjSwchYeoLUbCK5sh
iGI+nT3+liqUZW8+KXd/6I+xsN+YXuS9olmeN5L391VF7ZnWcsOKLbr3tnA3TKJb
Q/txpFhI/2CM2u0VU6w6DAAGlxic5Gf1Cdc8/mA5KaNEuq24PrRDTGl2ZXJtb3Jl
IFNvZnR3YXJlIFRlY2hub2xvZ3kgQ29ycG9yYXRpb24gKExTVEMpIDxzdXBwb3J0
QGxzdGMuY29tPohVBBMRAgAVAhsDAh4BAheABQJTOtVDAgsHAhYAAAoJECATgx5l
rsCu0P4An2f9h8YuWfW+mNY1gm29nIs+kbeZAJ44HMvNgfOVtqUxUCyTlCLjwR6O
CbkBDQRTOtUnEAQA4Q4D0F6l77N0e6XCIH49b7MHFyjkq3OdgHE4vylubEAXVeeX
FD4Vrojn3t/I1QqAUG4ipZZAlLVrSYruzQLYaLhjYP124Py/b6vRo0FcyVsLbazj
BxnGs+fFTrYspLaWfBK2dIrQ9ze9QSLhNous36W3em+fhx8hzGgcUUZRQOcAAwUD
/RkrdN+Mbim6H6MNnEKhoXlpogzriCUB+hpxfQSP+go6+Np2RGkQfTEu+W51vrFA
cW36cncp3OLpsvKzaQgTTT1rqb11Hoe/YpH3T9ngz4NX7a4OSDhHDKC1Q1BuzTEJ
3A3RXeAgRaMV8+hFm91g2KWZuMeqd+nSo2sb5EvpFhW9iEkEGBECAAkFAlM61ScC
GwwACgkQIBODHmWuwK7BaQCfUovuhS6oXuh+1sSqkGCxzHEGER8AniHYve/Kn6CL
SoAeXMxSC7F44Ood
=R0pG
-----END PGP PUBLIC KEY BLOCK-----
```

假设需要加密的文件名为`input.key`，加密命令如下:
```
gpg -e -a --rfc2440 --textmode --cipher-algo AES --compress-algo 0 -r 0x65AEC0AE input.key
```

假如你所使用的gpg软件是2.0以前的版本,`--rfc2440` 标志可能不会被识别，可以尝试用`--openpgp`替代.

命令执行后将会生成`input.key.asc`文件，可以通过`*INCLUDE`关键字导入主文件。

<!--more-->
如果觉得加密强度不够，可以使用下述2048bits的public key替换上述1024bits的key（实际上没什么用，该被破解的还是会被破解）:
```
-----BEGIN PGP PUBLIC KEY BLOCK-----
Version: GnuPG v2.0.19 (GNU/Linux)

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
=xfll
-----END PGP PUBLIC KEY BLOCK-----
```

使用2048bits的public key时，需要把上面加密命令里的`-r 0x65AEC0AE`替换为`-r 0x60C0435A`

Windows用户使用提示: 

* 将LSTC public key保存为lstcpgp.txt，假设保存到了d:\lstc_public_key\lstcpgp.txt
* 安装 Gpg4win，假设安装到C:\Program Files (x86)\GNU\GnuPG\
* 通过Win+R，输入cmd打开Dos命令行
* 通过cd命令进入input.key文件存放的文件夹
* 执行以下命令导入public key
```
"C:\Program Files (x86)\GNU\GnuPG\gpg2.exe"  --import d:\lstc_public_key\lstcpgp.txt
```
* 运行以下命令加密文件
```
"C:\Program Files (x86)\GNU\GnuPG\gpg2.exe" -e -a --rfc2440 --textmode --cipher-algo AES --compress-algo 0 -r 0x65AEC0AE input.key
```

### 加密容易解密难，如有加密k文件破解/解密需求的话请邮件联系 uzjtech@126.com，提供有偿解密服务。
