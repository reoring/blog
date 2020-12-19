---
template: BlogPost
path: /k8s/k3s/how_to_change_coredns_resolver
date: 2020-12-19T09:57:14.520Z
title: Kubernetesのk3s実装でDNSがうまく解決できない問題を解消する
---
k3sのdashboardやkubectlから、corednsのconfigmapを変更する。

```
forward . /etc/resolve.conf
```

/etc/resolve.confを参照している場合うまく解決できないときがあるようだ。下記のようにネームサーバを指定すると解消する。


```
forward . 8.8.8.8
```
