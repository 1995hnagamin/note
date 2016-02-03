# imcomplete type
# 不完全型
次の型。
* (CV修飾された)void
* 定義がないクラス型, 列挙型
* 不明サイズの配列 (arrays of unknown bound [of <Typename>])
* 不完全型の要素の配列

(CV修飾された)void以外の不完全型は欠けている情報を補うことで完全型にすることができる。

- [IBM Knowledge Center - 不完全型](http://www-01.ibm.com/support/knowledgecenter/ssw_ibm_i_71/rzarg/incotyp.htm#incotyp?lang=ja)
- [不完全な型](https://msdn.microsoft.com/ja-jp/library/200xfxh6.aspx) (MSDN)
- [Type - cppreference.com](http://en.cppreference.com/w/cpp/language/type#Incomplete_type)

# array of unknown bound
不明サイズの配列のこと。
グローバルで定義された不明サイズの配列は後方でサイズを指定した宣言を行うことで完全型にすることができる。
```
int a[]; // global
int a[10];
```
array of unknown boundの宣言をヘッダーに書いておいて、それをインクルードしたファイルで完全型にするという使い方がある。

自動変数はarray of unknown boundであってはならず、後方でサイズを指定して宣言してもredefinition扱いでエラーになる(っぽい)。

clangは関数の引数として与えられたarray of unknown bound of TYPENAMEを`TYPENAME*`として処理するっぽい。

- [Array declaration - cppreference.com](http://en.cppreference.com/w/cpp/language/array#Arrays_of_unknown_bound)

# rvalue

# glvalue
Generalized lvalue。lvalueとxvalue。

          expression
          /        \ 
        glvalue  rvalue
        /    \   /   \
    lvalue  xvalue  prvalue

# xvalue
eXpiring value。

# prvalue

# lvalue

# pointer-to-member expression

