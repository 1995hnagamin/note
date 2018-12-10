# 値カテゴリー一覧

注意: サブセクション名の辞書順で並べる

## 関数呼び出し (function call)

* lvalue
  * 返り値型が lvalue リファレンス型のとき
  * 返り値型が関数に対する rvalue リファレンス型のとき
* xvalue
  * 返り値型がオブジェクトに対する rvalue リファレンス型のとき
* prvalue
  * それ以外 (返り値型がリファレンス型でないとき)

cf. [[expr.call]/10](https://timsong-cpp.github.io/cppwp/n3337/expr.call#10)

## 配列要素へのアクセス (subscripting)

常に lvalue ([[expr.sub]/1](https://timsong-cpp.github.io/cppwp/n3337/expr.sub#1))
