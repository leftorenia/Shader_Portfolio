# No.14 シェーダで旗や水面をなびかせる

https://nn-hokuson.hatenablog.com/entry/2017/04/04/201537

## 元Shaderの概要

Surface Shader のカスタム頂点関数(vertex:vert)で、頂点のY座標に sin(時間 + x座標) の振幅を加算し、旗や水面がなびくアニメーションを実現する頂点アニメーションシェーダ。

## 設計方針

ライティングや影などの機能は実装しない
頂点変形はVFの頂点シェーダで、クリップ座標変換(UnityObjectToClipPos)の前に行う

## メモ

頂点変形は必ずオブジェクト空間の座標に対して行い、その後で UnityObjectToClipPos に渡す。変換後のクリップ座標をいじると射影が壊れる。


頂点を動かしても法線は再計算されない。また影は FallBack の ShadowCaster が変形前の頂点で描くため、なびいていない形の影が落ちる。
