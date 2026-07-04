# No.06 uvスクロールで水面を動かす

https://nn-hokuson.hatenablog.com/entry/2016/10/20/201111

## 元Shaderの概要

Surface Shader でサンプリング前のUV座標に _Time に比例した値を加算し、テクスチャをスクロールさせて水面の流れを表現するシェーダ。

## 設計方針

ライティングや影などの機能は実装しない(シリーズ共通)
テクスチャ色をそのまま出力するUnlitシェーダとして実装
時間は _Time.x を明示して使い、Surf版の実効値と速度を一致させる(No.14と同じ方式)
TRANSFORM_TEX で Tiling/Offset に対応する(2026-07-04修正で導入)

## メモ

_Time は float4 で (t/20, t, t*2, t*3)。Surf版の「uv.x += 0.1 * _Time;」はスカラーへの暗黙の切り捨てで _Time.x(t/20)が使われる。

frac() を挟まなくても、テクスチャのWrapModeがRepeatならUVが1を超えてもループする。
