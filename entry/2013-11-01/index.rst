C++ テンプレートメタプログラミング
================================================================================

C++ テンプレートメタプログラミングという本を読んでいろいろ勉強していた．
ちょっと知ったことをまとめようと思う．

まず， C++ テンプレートメタプログラミングではクラステンプレートのことを
メタ関数という．クラステンプレートというのは，


.. code-block:: c++

   template <args>
   struct function_name
   {
       // body
   };

のような形をした struct ということである． C++ ではテンプレートの引数として
型だけでなく値も渡せる．さらに，テンプレートの特殊化は値によってパターンマッチ
しているように振る舞う．だから，

* テンプレートの引数 = 関数の引数
* テンプレートの特殊化 = 分岐
* 構造体のメンバ = 戻り値

のようにして，コンパイル時にプログラミングできるというわけである．
たとえば，コンパイル時に足し算をするには次のように書く．

.. literalinclude:: plus.cpp
   :language: c++
   :lines: 3-14

引数のないメタ関数は，単なる構造体として書く．たとえば，

.. literalinclude:: nullary_metafunction.cpp
   :language: c++
   :lines: 4-16

多値を戻す関数を書くこともできる．しかも，見ようによれば
キーワードで戻している．ちょうど JavaScript で ``return { a: x, b: y }`` みたいに
するようだ．

.. literalinclude:: multiple_values.cpp
   :language: c++
   :lines: 3-15

部分適用などは MPL を使えばできるらしい．

.. literalinclude:: inc.cpp
   :language: c++
   :lines: 10

*Last updated:* |today|