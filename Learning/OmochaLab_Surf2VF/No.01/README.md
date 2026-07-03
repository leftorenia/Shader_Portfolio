# No.01 透明なシェーダを作る

https://nn-hokuson.hatenablog.com/entry/2016/10/05/201022

## 元Shaderの概要

Surface Shader を用いて半透明のオブジェクトを描画するシンプルなシェーダ。ユーザーはアルベド色とアルファ値を設定するだけで簡易的な半透明表現を実現できる。

## 設計方針

ライティングや影などの機能は実装しない
色と透明度のみを出力するUnlitシェーダとして実装

## メモ

UnityObjectToClipPos()　は、昔の記事だと　mul(UNITY_MATRIX_MVP, v.vertex)　と書かれている。

Surface Shaderの自動処理の項目にFogもある。




