# No.11 テクスチャの両面を描画する方法

https://nn-hokuson.hatenablog.com/entry/2017/03/03/202309

## 元Shaderの概要

Cull Off で背面カリングを無効にし、ポリゴンの裏側にもテクスチャを描画するシェーダ。

## 設計方針

フォグ対応(multi_compile_fog + フォグマクロ3点)

## メモ

カリングは Cull Back(デフォルト)/ Front / Off の3種。Cull Off は両面描画だが、裏面は法線が反転しないためライティングありのシェーダでは裏面が暗くなる

フォグ対応: #pragma multi_compile_fog、v2fに UNITY_FOG_COORDS(N)、頂点で UNITY_TRANSFER_FOG(o, o.pos)、フラグメントで UNITY_APPLY_FOG(i.fogCoord, col)
