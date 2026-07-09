# No.10 粘性のある液体をシェーダで作る

https://nn-hokuson.hatenablog.com/entry/2017/02/15/210945

## 元Shaderの概要

ShaderToy( https://www.shadertoy.com/view/Xts3WH )の作品をUnityに移植した、垂れ落ちる粘性液体の表現。格子状の乱数を smoothstep 補間し、UVのy方向に時間を減算してスクロールさせ、clamp とオレンジ系の色係数で液体の垂れを描く。

## 設計方針

GLSL→HLSL対応: fract→frac、mix→lerp、iTime→_Time.y、gl_FragCoord/iResolution→UV座標

## メモ

