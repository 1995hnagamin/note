# xsd:element

データ型を宣言する
xsd:schemaの直下に記述する

## 属性
* name:       データ型の名前
* ref:        データ型を外部で定義するときに指定する名前
* maxOccurs:  同要素を最大何回繰り返すか("unbounded"で上限なし)
* minOccurs:  同要素を最低何回繰り返すか

    <xsd:element name="customer">
      <xsd:complexType>
        <xsd:sequence>
          <xsd:element name="name" type="xsd:string"/>
          <xsd:element name="address" type="xsd:string"/>
        </xsd:sequence>
      </xsd:complexType>
    </xsd:element>

は次のようなデータを表す。

    <customer>
      <name>Alice</name>
      <address>NY</address>
    </customer>

See http://www.atmarkit.co.jp/ait/articles/0401/07/news072.html

# xsd:complexType

複雑型を宣言する
xsd:elementの直下に記述する

# xsd:sequence

子要素の順番を指定する

# xsd:attribute

要素が持つべき属性を指定する
xsd:complexType の直下に記述する

## 属性
* type 属性のデータ型名
* use 属性の特性。required/optional
  * "required"  必須であることを表す
  * "optional"  任意であることを表す
  * "prohibited" 属性の存在が禁止されていることを表す
* default   use="optional"の場合(if and only if)、属性のデフォルト値をを表す
* fixed     固定値を表す

default属性とfixed属性は同時に指定されてはいけない。

    <xsd:attribute name="id" type="xsd:string" />

    <xsd:attribute name="SomeAttr" type="SomeType" fixed="SomeValue" />

    <xsd:attribute name="SomeAttr" type="SomeType"
      default="SomeValue" use="optional" />

[XMLテクニック集(7):XML Schemaで単純型要素を定義する(3/3)](http://www.atmarkit.co.jp/ait/articles/0311/12/news001_3.html)

# xsd:choice

データ型が複数の表現を持つとき、その表現を指定する

    <xsd:element  name="orderItem">
      <xsd:complexType>
        <xsd:choice>
          <xsd:element name="name" type="xsd:string" />
          <xsd:element name="id" type="xsd:string" />
        </xsd:choice>
      </xsd:complexType>
    </xsd:element>

は次のいずれも受理する。

    <orderItem>
      <name>A Great Item</name>
    </orderItem>

    <orderItem>
      <id>12345</id>
    </orderItem>

