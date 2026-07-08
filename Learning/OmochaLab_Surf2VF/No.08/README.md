# No.08 円やリングをかっこよく動かす方法

https://nn-hokuson.hatenablog.com/entry/2016/11/14/203745

## 元Shaderの概要

Surface Shader でワールド原点からの距離を distance() で求め、sin(距離 − 時間) の絶対値を閾値判定することで、原点から広がる同心円状のリングをアニメーション表示するシェーダ。

## 設計方針

ライティングや影などの機能は実装しない
リングの色をそのまま出力するUnlitシェーダとして実装
ワールド座標は頂点シェーダで unity_ObjectToWorld から計算して補間する

## メモ

Surface Shader の Input に worldPos と書くだけで取れていたワールド座標は、VFでは mul(unity_ObjectToWorld, v.vertex).xyz を自分で書く。

リングはワールド原点(0,0,0)基準
