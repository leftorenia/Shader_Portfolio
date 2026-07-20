# No.13 頂点カラーを表示するシェーダを作る

https://nn-hokuson.hatenablog.com/entry/2017/03/29/195041

## 元Shaderの概要

メッシュの頂点カラーを表示するシェーダ。

## 設計方針

ライティングや影などの機能は実装しない
頂点カラーをそのまま出力するUnlitシェーダとして実装
appdata に color : COLOR セマンティクスを宣言して直接受け取る

## メモ

Surface Shaderでは uv_ 系以外の頂点データ(頂点カラー等)を surf に渡すには vertex:vert と UNITY_INITIALIZE_OUTPUT が必要だったが、VFでは appdata に COLOR を1行足すだけで済む。

COLOR セマンティクスは通常0〜1に丸められる前提で扱う(HDR的な値を運ぶならTEXCOORDを使う)
