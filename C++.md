# 不完全型
=imcomplete type

次の型。
* (CV修飾された)void
* 定義がないクラス型, 列挙型
* 不明サイズの配列 (arrays of unknown bound [of TYPENAME])
* 不完全型の要素の配列

(CV修飾された)void以外の不完全型は欠けている情報を補うことで完全型にすることができる。

links:
- [IBM Knowledge Center - 不完全型](http://www-01.ibm.com/support/knowledgecenter/ssw_ibm_i_71/rzarg/incotyp.htm#incotyp?lang=ja)
- [不完全な型](https://msdn.microsoft.com/ja-jp/library/200xfxh6.aspx) (MSDN)
- [Type - cppreference.com](http://en.cppreference.com/w/cpp/language/type#Incomplete_type)


# array of unknown bound

不明サイズの配列のこと。
グローバルで定義された不明サイズの配列は後方でサイズを指定した宣言を行うことで完全型にすることができる。

  int a[]; // global
  int a[10];

array of unknown boundの宣言をヘッダーに書いておいて、それをインクルードしたファイルで完全型にするという使い方がある。

自動変数はarray of unknown boundであってはならず、後方でサイズを指定して宣言してもredefinition扱いでエラーになる(っぽい)。

clangは関数の引数として与えられたarray of unknown bound of TYPENAMEを`TYPENAME*`として処理するっぽい。

links:
- [Array declaration - cppreference.com](http://en.cppreference.com/w/cpp/language/array#Arrays_of_unknown_bound)


# オブジェクト
=object

オブジェクトは定義やnew式、実装[^object.1]によって生成される。関数はオブジェクトではない。
すべてのオブジェクトはストレージの有効期間(storage duration)、型(type)をもつ。

[^object.1]:
  実装は必要に応じて一時オブジェクト(temporary object)を生成するが、省略することもある。

links:
- N3337
  -  1.8 [intro.object]
  - 12.2 [class.temporary]


# ポリモーフィッククラス
=polymorphic class

仮想関数を宣言または継承しているクラス。

links:
- N3337 10.3 [class.virtual]


# lvalue

関数またはオブジェクトのこと。

lvalueの例:

* lvalueのメンバ変数
* 変数
* ポインタのデリファレンス
* 関数呼び出しの戻り値であって、型がlvalue referenceであるもの
* 文字列リテラル

links:
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


# 無名名前空間
=unnamed namespace

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

links:
- [無名（匿名）名前空間の不思議な定義 - yohhoyの日記](http://d.hatena.ne.jp/yohhoy/20121130/p1)
- [Namespaces - cppreference.com](http://en.cppreference.com/w/cpp/language/namespace#Unnamed_namespaces)
- [C++11: Syntax and Feature](https://ezoeryou.github.io/cpp-book/C++11-Syntax-and-Feature.xhtml#namespace.unnamed)
- [C++ Standard Core Language Defect Reports and Accepted Issues](http://www.open-std.org/jtc1/sc22/wg21/docs/cwg_defects.html#1012)

# inline名前空間
=inline namespace

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

links:
- [What are inline namespaces for? - Stack Overflow](http://stackoverflow.com/questions/11016220/what-are-inline-namespaces-for)


# 標準レイアウトクラス
=standard-layout class

あるクラスが標準レイアウトクラスであるとは、次のすべてを満たすこと。
* 最初の非staticデータメンバの型は、基本クラスのどれでもない。
* 次のようなメンバをもたない。
  * 仮想関数
  * 標準レイアウトクラスでない非staticメンバ、リファレンス、配列
  * アクセス指定子が異なる複数の非staticデータメンバ (つまり、非staticデータメンバのアクセス指定子は全て同じでなくてはならない)
  * (基本クラスが非staticデータメンバをもつとき)非staticデータメンバ
* 次のような基本クラスをもたない。
  * 仮想基本クラス
  * 標準レイアウトクラスでないクラス


# trivially copyable class

あるクラスがtrivially copyable classであるとは、trvialなデストラクタをもち、かつ非trivialなコピーコンストラクタ、ムーブコンストラクタ、
コピー代入演算子、ムーブ代入演算子をもたないこと。


# trivial class

trivially copyable classであって、非trivialなデフォルトコンストラクタをもたないもの。

Trivial classは次をもたない:
* 非trivialなデフォルトコンストラクタ
* 非trivialなコピーコンストラクタ
* 非trivialなムーブコンストラクタ
* 非trivialなコピー代入演算子
* 非trivialなムーブ代入演算子

Trivial classはtrivialなデストラクタをもつ。


# POD構造体
=POD struct

Plain Old Data struct。標準レイアウトクラスかつtrivial classであって、さらにPODではないクラスを非staticデータメンバにもたないクラス。

非staticデータメンバをもつPOD構造体は、次の制約を満たす:
* その非staticデータメンバはPOD構造体である。
* その非staticデータメンバのアクセス指定子は全て同じである。
* 最初のデータメンバは基本クラスのいずれでもない。
* 基本クラスは標準レイアウトクラスである。
* 基本クラスは非staticデータメンバをもたない。

POD構造体は仮想基本クラスや非標準レイアウトクラスを基本クラスにもたない。
POD構造体はtrivialなデストラクタをもつ。
