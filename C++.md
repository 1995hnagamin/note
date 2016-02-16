# imcomplete type
# 不完全型
次の型。
* (CV修飾された)void
* 定義がないクラス型, 列挙型
* 不明サイズの配列 (arrays of unknown bound [of TYPENAME])
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

# lvalue
関数またはオブジェクトのこと。

lvalueの例:

* lvalueのメンバ変数
* 変数
* ポインタのデリファレンス
* 関数呼び出しの戻り値であって、型がlvalue referenceであるもの
* 文字列リテラル

- [何が lvalue で何が rvalue なのか - iorate's blog](http://iorate.hatenablog.com/entry/20111207/1323280542)
- [C++11: Syntax and Feature](http://ezoeryou.github.io/cpp-book/C++11-Syntax-and-Feature.xhtml#basic.lval) 

# xvalue
expiring value(消失値)。寿命が近いオブジェクトのこと。

xvalueの例:

* 関数呼び出しの戻り値であって、型がrvalue referenceであるもの
  * std::moveの戻り値
* rvalue referenceへの明示的なキャスト

# rvalue
xvalueとprvalueのこと。

# glvalue
generalized lvalue。lvalueとxvalueのこと。

# prvalue
pure rvalue。rvalueのうちxvalueではないもの。

prvalueの例:

* prvalueのメンバ変数
* 一時オブジェクト
* 文字列リテラル以外のリテラル
* 特定のオブジェクトに関連付けされていない値
  * 関数呼び出しの戻り値であって、型がリファレンスでないもの

# value category
式の属性の一つ。

全ての式はlvalue、xvalue、prvlueのうちどれか一つに属する。

          expression
          /        \
        glvalue  rvalue
        /    \   /   \
    lvalue  xvalue  prvalue


# pointer-to-member expression

# nested-name-specifier

qualified-idが`/(([:alpha:]+::)+)::[:alpha:]+$/`にマッチした時の`$1`( `([:alpha:]+::)+` )に当たる部分。

# unnamed namespace
# 無名名前空間

    namespace { 本体 }

名前のない名前空間。
無名名前空間で定義された名前は、宣言場所(point of declaration)から翻訳単位の終わりまで有効である。

* (C++03まで) 無名名前空間内で宣言された名前は、*extern指定子の有無にかかわらず*内部リンケージをもつ。
* (C++11から) 無名名前空間および無名名前空間内で直接的・間接的に宣言された名前空間は内部リンケージをもつ。

上のプログラムは次と等価な振る舞いをする。ここで、uniqueは翻訳単位で一意な名前である。

    namespace unique {}
    using namespace unique;
    namespace unique { 本体 }

static指定子より無名名前空間を使うほうが望ましい。
static指定子は無名名前空間と違い、名前のあるクラスなどを内部リンケージにすることはできない。
C++11でstaticはdeprecatedになる予定だったが、Cとの互換性のためundeprecatedされた。

- [無名（匿名）名前空間の不思議な定義 - yohhoyの日記](http://d.hatena.ne.jp/yohhoy/20121130/p1)
- [Namespaces - cppreference.com](http://en.cppreference.com/w/cpp/language/namespace#Unnamed_namespaces)
- [C++11: Syntax and Feature](https://ezoeryou.github.io/cpp-book/C++11-Syntax-and-Feature.xhtml#namespace.unnamed)
- [C++ Standard Core Language Defect Reports and Accepted Issues](http://www.open-std.org/jtc1/sc22/wg21/docs/cwg_defects.html#1012)

# inline namespace
# inline名前空間

    inline namespace 名前 { 本体 }

inline名前空間は、それを直接包む名前空間に対して透過的になる。
すなわち、inline名前空間で宣言された名前は、あたかも1つ上の名前空間においても宣言されたかのように見える。
あるinline名前空間を包む名前空間もまたinline名前空間であった場合、2つ上の、3つ上の、…と続く。

`#ifndef`ディレクティブでコンパイル時に提供する機能を切り替えるなどの使い方がある。

    #if __cplusplus < 1997L
      inline
    #endif
      namespace pre_cxx_1997 {
        template<class T> __vector_impl;
        // ...
      }

    #if __cplusplus >= 1997L
      #if __cplusplus == 1997L
        inline
      #endif
        namespace cxx_1997 {
          template<class T, class Alloc=std::allocator<T> >
          class vector : pre_cxx_1997::__vector_impl<T> {
            // ...
          }
        }
    #endif

- [What are inline namespaces for? - Stack Overflow](http://stackoverflow.com/questions/11016220/what-are-inline-namespaces-for)
