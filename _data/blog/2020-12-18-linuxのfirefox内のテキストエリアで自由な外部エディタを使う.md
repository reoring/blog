---
template: BlogPost
path: /linux/firefox/textarea
date: 2020-12-18T07:57:38.541Z
title: LinuxのFirefox内のテキストエリアで自由な外部エディタを使う
---
## Textern Add-onのインストール

まずはFirefoxに [Textern – Get this Extension for 🦊 Firefox (en-US)](https://addons.mozilla.org/en-US/firefox/addon/textern/) というAdd-onを入れます。

## Textern Nativeのインストール

[jlebon/textern: A Firefox add-on for editing text in your favourite external editor!](https://github.com/jlebon/textern)

```
git clone --recurse-submodules https://github.com/jlebon/textern
cd textern
sudo make native-install
```

## addonの設定

デフォルトではgeditが起動するようになっています。これをgvimに変更するには下記の設定をtextern addonの設定に入れます。

```
["gvim", "-f", "+call cursor(%l,%c)"]
```
