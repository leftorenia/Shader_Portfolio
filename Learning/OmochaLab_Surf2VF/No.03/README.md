# No.03 リムライティングのシェーダを作る

https://nn-hokuson.hatenablog.com/entry/2016/10/11/191324

## 元Shaderの概要

Surface Shader を用いて、視線ベクトルと法線の内積からリム(縁)の強さを計算し、Emission に設定することでオブジェクトの輪郭を発光させるシェーダ。pow() の指数でリムの幅(減衰の鋭さ)を調整する。

## 設計方針

ライティングや影などの機能は実装しない
Standardライティングが行っていた「Emissionをライティング結果に加算する」処理を、ベースカラー + リム色 × リム強度 の加算として再現
不透明シェーダなので、No.01/02の透明用設定(ZWrite Off / Blend / Queue=Transparent)は持ち込まない

## メモ

EmissionはStandardライティングに依存しない加算項なので、リム発光部分はSurf版と同じ見た目になる。差が出るのはベースカラー部分(Surf版は陰影とGIが乗る)のみ。

saturate(dot()) を外すと、法線が視線と逆を向いたとき内積が負になり rim が1を超え、pow() の結果が破綻する。

視線ベクトルは _WorldSpaceCameraPos − ワールド座標 で自前計算できる(UnityWorldSpaceViewDir() と同じ式)。

不透明オブジェクトでは FallBack "Diffuse" のShadowCasterパスが「影を落とす」「カメラのデプステクスチャに書き込む」ために機能する。半透明だったNo.01/02とは逆に、残す判断になる。
