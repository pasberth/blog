全称型, System F
================================================================================

単純型付きラムダ計算で， id 関数は無限にある．

* .. texfigure:: eachid1.tex
* .. texfigure:: eachid2.tex
* .. texfigure:: eachid3.tex
* ...

全称型は，これらをひとまとめにして扱う型で， ∀ とか， forall という記号を使って
あらわされる．全称型を使うと，このように書くことができる

* .. texfigure:: eachid.tex

全称型は，型システム入門の 23章 で触れられている．読んでみてほしい．

全称型
--------------------------------------------------------------------------------

Haskell などのプログラミング言語に慣れた人には退屈に思えるかもしれない．要するに，
全称型というのは次のような，普通の型のことなのだ．

.. code-block:: haskell

   id :: a -> a

Haskell は， forall を省略してもよいことになっている．より明示的に書けば
こうなる．

.. code-block:: haskell

   id :: forall a. a -> a

System F
--------------------------------------------------------------------------------

System F では，型の表現が第一級に持ち上げられている．
それ以外に特殊なものはないように見える．
System F ではないだろうけど，似たような表現ができる
Coq で id を書いてみよう．

.. code-block:: coq

    Definition id (T : Type) (x : T) : T := x.

Coq を読めない人は多いかもしれない． コロンの左が引数の名前，
右が引数の型になっている．第一引数は Type 型の T で，第二引数は T 型の
x だ．全体として， T 型の戻り値を持つ．定義は x ．

使い方はこう． Coq インストールしてない人はインストールしてね (ステマ)．
第一引数として型 (nat) を渡し，第二引数として 42 を渡している．
依存型を知っていれば，とくに不思議に思うことはないはずだ．

.. code-block:: coq

    Coq < Eval compute in id nat 42.
         = 42
         : nat

*Last updated:* |today|