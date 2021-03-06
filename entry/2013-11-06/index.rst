部分型
================================================================================

.. include:: /roles.rst

ほとんどのプログラミング言語にはレコード型というものが存在する．
複数の機能を持つ型の機能のひとつとして
使えるというものもある．たとえば Haskell では直和型と同じ構文で宣言できる
( :hs:`data T = T { member :: M }` のようにして宣言する)．
オブジェクト指向言語ではクラスというほうがわかりやすいだろう．レコード型というのは，
いくつかのメンバ(フィールド，プロパティ)を持つような型のこと．たとえば，
{x::Int,y::String} のように書いたとすれば， これは Int 型の x と
String 型の y を持つような型のことになる．

そこで，次のような関数を考えてみる．

.. texfigure:: subt1.tex

r#x というのは， r のメンバ x にアクセスするという意味だ．

そこでこの関数に，

.. texfigure:: subt2.tex

のような引数を適用したとしよう．しかし次のような項は型付けできない．

.. texfigure:: subt3.tex

ラムダが引数の型として ``{x:Nat}`` を要求しているのに対して，
実際の引数は ``{x:Nat,y:Nat}`` という型を持つ．もし型エラーになる
理由がわからないのであれば， ``{x:Nat}`` を Int， ``{x:Nat,y:Nat}`` を
String などと置き換えて考えてみてほしい． Int を要求しているのに String が
渡されている，というのが型エラーとなる理由だ．これは直観に反している．
``{x:Nat}`` と ``{x:Nat,y:Nat}`` の関係は， Int と
String などとは違い， ``{x:Nat,y:Nat}`` は， 実際に x というメンバを持つから，
``{x:Nat}`` である条件を満たしているじゃないか．

この直観に従った規則が部分型で，部分型を利用すると，上記のような項に型を付けることができる．

部分型は，型システム入門の 15章で触れられている．興味があれば読んでみてほしい．

部分型関係
--------------------------------------------------------------------------------

形式的な議論はしない．厳密な定義は型システム入門を読んでみてほしい．
要約すると，たとえば，

.. texfigure:: subtyping1.tex

は

.. texfigure:: subtyping2.tex

の部分型である，というような関係をいう．
メンバの数が多いほうが部分型なのだ．部分型は．オブジェクト指向言語に慣れ親しんだ
人には，サブクラスと言った方がわかりやすいかもしれない．スーパークラスのほうが
メンバが少なく，サブクラスのほうがメンバが多い．(もちろん，継承は部分型ではない．
くれぐれも注意してほしい．)

S が T の部分型であるとき， S の要素はすべて T でもある．
簡単に言うと， S は T にアップキャストできるというわけだ．( T は S にダウンキャスト
できない ． )

この関係を

.. texfigure:: subtyperel.tex

のように書く．たとえば

.. texfigure:: subtyperelexample.tex

である．

関数の引数や関数の戻り値に部分型を使うとき，どのように操作したら安全かを
指定する必要がある．これは次のように書くのがいちばんわかりやすい．

.. texfigure:: subtypearr.tex

まず左の前提(横線より上の左側)について．これは関数の引数に関する制約を言ってる．
もし T_1 が S_1 の部分型なら， S_1→S_2 は T_1→T_2 の部分型である．
S_1→S_2 は， T_1→T_2 にアップキャストできると言ってる．

例示は理解の試金石だ．具体例で考えよう．
次のように置き換えてみると，わかりやすいと思う．

.. texfigure:: subtypearrex1.tex

この規則が言ってるのは， ``{x:Nat}`` を受け取る関数は，
``{x:Nat,y:Nat}`` も受け取ることができる，ということだ．

「もし T_1 が S_1 の部分型なら， S_1→S_2 は T_1→T_2 の部分型である」
という文章の「なら」の前後で T_1 と S_1 の向きが逆になってる．
このような規則を反変という．

次の右側の前提について．これは関数の戻り値に関する制約を言ってる．
もし S_2 が T_2 の部分型なら， S_1→S_2 は T_1→T_2 の部分型である．

次のように置き換えてみると，わかりやすいと思う．

.. texfigure:: subtypearrex2.tex


この規則が言ってるのは， ``{x:Nat,y:Nat}`` を返す関数は，
``{x:Nat}`` を返す関数とみなすこともできる (キャストできる)，
ということだ．

「もし S_2 が T_2 の部分型なら， S_1→S_2 は T_1→T_2 の部分型である」
という文章の「なら」の前後で T_2 と S_2 の向きは同じだ．
このような規則を共変という．


*Last updated:* |today|