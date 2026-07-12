# No.12 トゥーンシェーダを自作してみる

https://nn-hokuson.hatenablog.com/entry/2017/03/27/204255

## 元Shaderの概要

Surface Shader のカスタムライティング関数(LightingToonRamp)を定義し、ハーフランバート(dot(N,L)*0.5+0.5)の値でランプテクスチャを引いて陰影を段階化するトゥーンシェーダ。

## 設計方針

この回はライティングを実装
ForwardBase パスでメインのディレクショナルライト1灯のみを扱う
影・追加ライト(ForwardAdd)・アンビエントは実装しない

## メモ

ライトの情報を使うには Pass に Tags { "LightMode"="ForwardBase" } が必要。これが無いと _WorldSpaceLightPos0 や _LightColor0 の値が保証されない。

_WorldSpaceLightPos0 は、ディレクショナルライトでは「方向」(w=0)、ポイントライトでは「位置」(w=1)。ForwardBaseのメインライトは必ずディレクショナルなので .xyz をそのまま方向として使える。

_LightColor0 は Lighting.cginc の include で使えるようになる。

ハーフランバート d = dot(N,L)*0.5+0.5 は [-1,1]→[0,1] の変換。ランプテクスチャのUV(d, 0.5)として使うため、WrapModeはClamp推奨。
