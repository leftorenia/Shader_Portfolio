# No.09 シェーダで作るノイズ５種盛り

https://nn-hokuson.hatenablog.com/entry/2017/01/27/195659

## 元Shaderの概要

Surface Shader で5種類のノイズを実装する。
- Random: frac(sin(dot(uv, 定数)) * 大きな数) によるハッシュ的な乱数
- Block: UVを floor で格子に量子化してから乱数を引く
- Value: 格子点の乱数を smoothstep 補間(f*f*(3-2f))で滑らかに繋ぐバリューノイズ
- Perlin: 格子点に勾配ベクトル(random2)を置き、距離ベクトルとの内積を補間するパーリンノイズ
- fBm: パーリンノイズを周波数2倍・振幅1/2ずつ4オクターブ重ねる非整数ブラウン運動

## 設計方針

ライティングや影などの機能は実装しない
ノイズ値をグレースケールでそのまま出力するUnlitシェーダとして実装
ノイズ関数(random / noise / valueNoise / random2 / perlinNoise / fBm)はSurf版と一字一句同じものを使用

## メモ

関数は同じなので特筆事項は無し。
