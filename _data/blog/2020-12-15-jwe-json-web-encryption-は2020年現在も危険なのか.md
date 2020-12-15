---
template: BlogPost
path: /security/jwe
date: 2020-12-15T08:47:50.348Z
title: JWE(JSON Web Encryption)は2020年現在も危険なのか?
---
## 概要

* [JOSEは、絶対に避けるべき悪い標準規格である | POSTD](https://postd.cc/jwt-json-web-tokens-is-bad-standard-that-everyone-should-avoid/)
* [JSON Web Encryption (JWE) の解説 - Qiita](https://qiita.com/ono_matope/items/938a98fb111a297b68b9)

いくつかの記事でJWEは避けるべき、脆弱性がある。という指摘があるが、これらが議論されていたのは2017年頃だ。2020年においてまだ該当記事の脆弱性が実際に存在するか調査した結果を記録する。私はJWEのエキスパートではないし、RFC-7516を全て読み込んでもいないため間違っている部分があるかもしれない。もしこの調査結果に対してフィードバックがあれば編集リクエストを送ってほしい。

## 結論

現在は脆弱性は修正され、安全なようだ。脆弱性に対応していないライブラリを使っている場合はもちろん危険なので使用しているライブラリが対応されているか調査する必要がある。

## 調査内容

### go-joseの修正

[oss-sec: CVE request: multiple issues in go-jose package](https://seclists.org/oss-sec/2016/q4/319) ここでCVE番号のリクエストと、パッチへのリンクが提供されている。

[Critical Vulnerability in JSON Web Encryption? · Issue #141 · square/go-jose](https://github.com/square/go-jose/issues/141) これはgo-joseライブラリの質問。

https://github.com/square/go-jose/issues/141#issuecomment-286887765 このコメントでその脆弱性は1.1.0で修正されているよ。と書かれている。

## 脆弱性の概要

攻撃の名称は、Classic Invalid Curve Attack.というらしい。

この脆弱性にさらされると、攻撃者はJWE with Key Agreement with Elliptic Curve Diffie-Hellman Ephemeral Static (ECDH-ES)を使用して、送信者が受信者の秘密鍵を取り出すことができるようになってしまうよ、ということらしい。

[Critical Vulnerability in JSON Web Encryption](https://auth0.com/blog/critical-vulnerability-in-json-web-encryption/) ここが詳しい。

## Auth0のAntonioとIETFチームのやりとり

[[jose] Use of ECDH-ES in JWE](https://mailarchive.ietf.org/arch/msg/jose/oGme8BaRErp8qN3PK1gMEBnq2t4/)このメーリングリストでやり取りしている。

IETFの人もCurve Attackについては言及されていないとしながらも、本文は修正することができないため、Errata(正誤表)に記載してほしいとなり、Antonioが正誤表に投稿する旨で決着していました。ただ、[RFC Errata Report » RFC Editor](https://www.rfc-editor.org/errata_search.php?rfc=7516&rec_status=15&presentation=records)この正誤表検索で該当のエントリは見つからないため、投稿されていないか、レビューされていない可能性がありそうだ。

## JWEの利用実績

* KubernetesのDashboardとブラウザ間の通信で実際に利用されている。Kubernetes Dashboardの該当部分はgo-joseが使われている。
