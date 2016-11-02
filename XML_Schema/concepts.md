# データ型

* 単純型
  * ビルトインデータ型
  * ユーザー派生データ型
* 複合型
  * 単純型内容を持った複合型
  * 複合型内容を持った複合型

# 単純型
=simple type

要素と属性の宣言に使えるデータ型。
単純型は子要素や属性をもたない。

# 複合型
=complex type

単純型でないデータ型。
複合型はxsd:complexType要素で定義する。
[たのしいXML: Schema(スキーマ) データ型: 単純型と複合型](http://www6.airnet.ne.jp/manyo/xml/schema/step4.html)

# ビルトインデータ型

46個ある。

* integer 整数全体
* nonNegativeInteger 非負整数全体
* positiveInteger 正整数全体
* long [-9223372036854775808, 9223372036854775807]
* int [-2147483648, 2147483647]

[たのしいXML: Schema(スキーマ) データ型: 単純型について](http://www6.airnet.ne.jp/manyo/xml/schema/step5.html)

# ユーザー派生データ型

# 派生

* 制限
* ユニオン
* リスト

# 制限
=restriction

    <xsd:simpleType name="SomeTypeName1">
      <xsd:restriction base="SomeTypeName2">
        (いくつかの制約ファセット)
      </xsd:restriction>
    </xsd:simpleType>

# 制約ファセット

制限による派生を行う時に使う。
valueで値を指定する。

* 数値の制約
  * minInclusive/maxInclusive 以上,以下
  * minExclusive/maxExclusive 超過,未満
  * totalDigits 最大桁数
  * fractionDigits 小数部の最大桁数
* 文字列,リストの制約
  * length 文字数
  * minLength/maxLength 最小,最大文字数
  * 正規表現による文字列の制約
* 列挙による制約

例:

    <!-- 非負整数 -->
    <xsd:restriction base="xsd:int">
      <xsd:minInclusive value="0" />
    </xsd:restriction>

    <!-- 郵便番号 -->
    <xsd:restriction base="xsd:string">
      <xsd:pattern value="\d{3}-\d{4}" />
    </xsd:restriction>

    <!-- 血液型 -->
    <xsd:restriction base="xsd:string">
      <xsd:restriction value="A" />
      <xsd:restriction value="B" />
      <xsd:restriction value="O" />
      <xsd:restriction value="AB" />
    </xsd:restriction>

# ユニオン

直和。

    <!--
     Flat Z CPO ( \mathbb{Z}_{\bot} )の定義。
     "_|_", "0", "1", "-1", "2", "-2", ... を受理する。
    -->
    <xsd:simpleType name="FlatIntegerCPO">
      <xsd:union memberTypes="Bottom xsd:integer" />
    </xsd:simpleType> <xsd:simpleType name="Bottom"> <xsd:restriction base="xsd:string">
        <xsd:enumeration value="_|_" />
      </xsd:restriction>
    </xsd:simpleType>

[たのしいXML: Schema(スキーマ) ユニオン(union)データ派生型](http://www6.airnet.ne.jp/manyo/xml/schema/step10.html)

# リスト

# 空要素のデータ型

子要素及び属性をもたないをもたないデータ型は次のように定義する。

    <xsd:complexType name="SomeTypeName" />

# 単純型内容を持った複合型

子要素をもたないが、属性を持つデータ型。
これらはxsd:simpleContentで定義できる。

    <xsd:complexType name="SomeTypeName1">
      <xsd:simpleContent>
        <xsd:extension base="xsd:string">
          <xsd:attribute name="SomeAttr"
            type="SomeTypeName2" use="required"/>
        </xsd:extension>
      </xsd:simpleContent>
    </xsd:complexType>

[たのしいXML: Schema(スキーマ) 単純型内容を持った複合型 - 定義の基本](http://www6.airnet.ne.jp/manyo/xml/schema/step13.html)
