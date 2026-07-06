# No.07 テクスチャをブレンドして自然な地形を表示する

https://nn-hokuson.hatenablog.com/entry/2016/10/27/185618

## 元Shaderの概要

Surface Shader でメインテクスチャとサブテクスチャをマスクテクスチャの値で lerp ブレンドし、草地と土のような地形の自然な混合を表現するシェーダ。

## 設計方針

ライティングや影などの機能は実装しない
ブレンド結果をそのまま出力するUnlitシェーダとして実装
3枚のテクスチャそれぞれに TRANSFORM_TEX を適用し、Tiling/Offset に対応

## メモ

Surface Shader版は3枚とも uv_MainTex でサンプリングしているため、Sub/Mask の Tiling/Offset は無視されるが、VF版は各テクスチャの _ST を使うので、テクスチャごとのTiling設定が反映される

lerp(c1, c2, p) の p は fixed4 なのでRGBAチャンネルごとに独立してブレンドされる。マスクがグレースケールなら実質単一係数と同じ。
