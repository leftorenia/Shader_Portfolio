# No.04 テクスチャを表示する

https://nn-hokuson.hatenablog.com/entry/2016/10/12/203902

## 元Shaderの概要

Surface Shader を用いて、Propertiesで受け取った _MainTex を tex2D でサンプリングしてAlbedoに設定する、テクスチャ表示の基本シェーダ。

## 設計方針

ライティングや影などの機能は実装しない(シリーズ共通)
テクスチャの色をそのまま出力するUnlitシェーダとして実装
UVは頂点入力(TEXCOORD0)から補間してフラグメントで使う
TRANSFORM_TEX で Tiling/Offset に対応する

## メモ

Surface Shaderの Input で uv_MainTex と書くと「TEXCOORD0の取得 + Tiling/Offset(_MainTex_ST)の適用」が自動で行われる。VFでは appdata に uv : TEXCOORD0 を自分で宣言し、float4 _MainTex_ST; + TRANSFORM_TEX(v.uv, _MainTex) でTiling/Offsetを適用する。
