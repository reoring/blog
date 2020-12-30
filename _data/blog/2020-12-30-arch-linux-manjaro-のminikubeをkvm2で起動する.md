---
template: BlogPost
path: /linux/arch/minikube
date: 2020-12-30T08:40:10.660Z
title: Arch Linux(Manjaro)のminikubeをKVM2で起動する
thumbnail: /assets/Manjaro_logo_text.png
---
## 必要なパッケージのインストール
﻿
```
yay -S minikube kubectl docker-machine-driver-kvm2 libvirt qemu-headless ebtables
```
﻿
## libvirtdを有効にする
﻿
```
sudo systemctl enable libvirtd.service
sudo usermod -a -G libvirt $(whoami)
```
﻿
## libvirtのdefaultネットワークを有効にする
﻿
```
sudo virsh net-autostart default
```
﻿
## minikubeがデフォルトでkvm2を使うようにする
﻿
```
minikube config set vm-driver kvm2
```
﻿
﻿
## 搭載メモリの1/4をminikubeに割り当てる
﻿
もしManjaroを使っているならfreeコマンドをデフォルトのfreeコマンドにする。
﻿
```
unalias free
```
﻿
﻿
```
MEMORY_FRACTION=4
minikube config set memory "$(($(free --mega | head -n2 | tail -n1 | cut -c15-27)/$MEMORY_FRACTION))"
```
﻿
## 起動して確認する
﻿
```
minikube start
kubectl cluster-info
```
