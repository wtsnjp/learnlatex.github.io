---
layout: "lesson"
lang: "ja"
title: "文書クラスを利用したデザインの変更"
description: "このレッスンでは文書クラスとは何で、それがどのように文書のレイアウトに寄与するのかについて説明します。そしてTeXディストリビューションに含まれる主な文書クラスを紹介します。"
toc-anchor-text: "文書クラス"
toc-description: "文書の基本的なレイアウト設定"
---

# 文書クラス

<span class="summary">このレッスンでは文書クラスとは何で、それがどのように文書のレイアウトに寄与するのかについて説明します。そしてTeXディストリビューションに含まれる主な文書クラスを紹介します。</span>

## 文書クラスの役割

賢明な読者は、既にすべてのLaTeX文書は文書クラスを宣言する`\documentclass`から開始され、さらに言えば`\documentclass{jlreq}`が一般的な選択肢であるということにお気付きでしょう。お察しの通り、この宣言はあらゆるLaTeX文書で必須のもので、（ほとんどの場合）常にファイルの先頭に置くべきものです。

<!-- TODO: plautopatchについてはここで言及？ -->

文書クラスは、これから作成する文書の全般的なレイアウトを設定します。具体的には、以下のようなものが設定されます。

* デザイン：余白、フォント、スペーシングなど
* 「章」の構造を利用可能にするか否か
* タイトルを独立ページに出力するか否か

文書クラスは、もっと広範に各種の新しいコマンドを追加する場合もあります。この傾向は、特に特殊な用途のクラス（例えばプレゼンテーション用のスライドを作成するためのもの）で顕著です。

文書クラスの宣言では、さらに文書全体に適用される**グローバル・オプション**を設定することもできます。これらは角カッコ内に列挙する形で与えることができます：`\documentclass[<オプション>]{<文書クラス>}`。角カッコで省略可能なオプションを与えるこの書式はLaTeXのさまざまなコマンドでも同様に採用されています。

## 基本の文書クラス（和文用）

本チュートリアルでは`jlreq`を基本の文書クラス（和文用）として採用しています。この文書クラスは`10pt`, `11pt`, `12pt`などのフォントサイズを変更するオプションや、文書を2段組に変更する`twocolumn`オプションを受け付けます。

<!-- TODO: 日本語の標準文書クラスやjsclassesなどについて追記 -->

## 基本の文書クラス（欧文用）

<!-- TODO: LaTeX標準の文書クラス（欧文用）もここで扱うべきか再検討 -->

ここでLaTeX標準で提供されているクラスについても紹介しておきます。これらはいずれも欧文用の文書クラスで、和文組版には適しません。

* `article`: 章のない短めの欧文文書
* `report`: 章のある長めの欧文文書、片面印刷
* `book`: 章のある長めの欧文文書、両面印刷、前付け・後付けあり（たとえば索引）
* `letter`: セクション構造のない欧文の手紙
* `slides`: プレゼンテーション用（ただし後述の注意を参照）

`article`, `report`, `book`クラスでも、基本的には`jlreq`と似たようなコマンドが利用可能です。手紙用の`letter`クラスでも多くのコマンドが利用できますが、少し異なる点もあります。

```latex
\documentclass{letter}
\begin{document}

\begin{letter}{Some Address\\Some Street\\Some City}

\opening{Dear Sir or Madam,}

The text goes Here

\closing{Yours,}

\end{letter}

\end{document}
```

住所の各行が`\\`によって区切られていることに注目してください。改行については[もう少し後](lesson-11)で扱います。また`letter`クラスが1通の「手紙」のために`letter`環境を作成し、またいくつかの特別なコマンドを定義している点にも注意してください。

ところで、欧文用のarticle, report, bookクラスでもやはり`10pt`, `11pt`, `12pt`などのフォントサイズを変更するオプションや、文書を2段組に変更する`twocolumn`オプションが利用できます。

## 高機能な文書クラス（欧文用）

上で紹介した標準的な文書クラスはとても安定しているのですが、一方でデザインも使用可能なコマンドも極めて保守的です。これまでに、より強力な文書クラスも多数作成されてきました。そうした文書クラスを用いると、（いずれ本チュートリアルでも[紹介](lesson-11)するように）自分で一からコードを書かなくても、簡単にデザインを変更することが可能になります。

### 欧文用のクラス

アメリカ数学学会（American Mathematical Society; AMS）は、伝統的な数学ジャーナルの見た目により近いデザインを実現する標準文書クラスの変種`amsart`, `amsbook`を提供しています。

大規模かつ人気のある二大「拡張」文書クラスはKOMA-Scriptバンドルとmemoirクラスです。KOMA-Scriptは3種類の標準文書クラスに「対応」するような3つのクラス`scrartcl`, `scrreprt`, `scrbook`, `scrlttr2`を提供しています。一方`memoir`クラスは単独の文書クラスで`book`クラスの拡張に相当します。

こうした拡張文書クラスは数多くのカスタマイズ用フックを提供しています。そのいくつかを、本レッスンの練習問題で扱います。こうしたクラスにどのようなフックが用意されているかを把握する方法は[後のレッスン](lesson-16)で扱います（もちろん、途中を飛ばして先に見てしまっても構いません）。

## プレゼンテーション

欧文用標準文書クラスの1つに`slides`があります。この文書クラスは1980年代中頃に物理的なスライドを作成するために開発されたものでPDFベースのインタラクティブなスライドを作成するための機能は一切ありません。現代では、そうした機能をもつより現代的なスライド用の文書クラスも存在します。それらは一般的なLaTeX文書と比べると幾分特殊な部類に属するので、本レッスンの[追加解説](more-05)で扱います。

## 練習問題

文書クラスを変更する方法を試してみましょう。次の欧文LaTeX文書のクラスをKOMAバンドルに含まれる文書クラスや`memoir`クラスに変更すると、最終的な見た目がどのように変化するでしょうか。

```latex
\documentclass{article} % ここのクラスを変更します

\begin{document}

\section{Introduction}

This is a sample document with some dummy
text\footnote{and a footnote}. This paragraph is quite
long as we might want to see the effect of making the
document have two columns.

\end{document}
```

さらにクラスオプション`twocolumn`を追加して、レイアウトがどのように変化するか確認してみましょう。

上記の欧文文書ソースについて使用クラスを`scrreprt`に変更し、さらに`\section`を`\chapter`に置き換えてみましょう。さらに次のクラスオプションを使用するとどうなるか確認してみてください。

- `chapterprefix`
- `headings=small`
- `headings=big`
- `numbers=enddot`
