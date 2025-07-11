---
title: HTML に関する質問
---

[Front-end Job Interview Questions - HTML Questions](https://github.com/h5bp/Front-end-Developer-Interview-Questions/blob/master/src/questions/html-questions.md) の回答集です。提案や訂正のプルリクエストは大歓迎です！

import TOCInline from '@theme/TOCInline';

<TOCInline toc={toc} />

### `DOCTYPE` は何のためにあるものですか？

`DOCTYPE` は "document type" の略です。これは、標準モードと[後方互換(quirks)モード](https://quirks.spec.whatwg.org/#history)を区別するために HTML で使用される宣言です。これがあると、標準モードで Web ページをレンダリングするようにブラウザに指示します。

教訓 - ページの先頭には `<!DOCTYPE html>` を追加しましょう。

###### 参考

- https://stackoverflow.com/questions/7695044/what-does-doctype-html-do
- https://www.w3.org/QA/Tips/Doctype
- https://quirks.spec.whatwg.org/#history

### どのようにすれば複数の言語のコンテンツを含むページを提供できますか？

この質問は少し曖昧なので、最も一般的なケース、つまり複数の言語で利用可能なコンテンツを提供する方法を聞かれているとします。1 つのページ内のコンテンツは 1 つの言語でのみ表示されるべきです。

HTTP リクエストがサーバに対して行われるとき、リクエストしているユーザエージェントは通常 `Accept-Language` ヘッダのような言語設定に関する情報を送信します。サーバーはこの情報を使用して適切な言語のバージョンで文書を返すことができます。返された HTML 文書においても `<html lang="ja">...</html>` のような `<html>` タグで `lang` 属性を宣言するべきです。

バックエンドでは、HTML マークアップには YML 形式または JSON 形式で格納された各言語の `i18n` プレースホルダとコンテンツを含めることができます。サーバーは通常、バックエンドフレームワークの助けを借りて各言語のコンテンツを含む HTML ページを動的に生成します。

###### 参考

- https://www.w3.org/International/getting-started/language

### 多言語サイトを設計・開発する際には、どんなことに注意を払わなければならないですか？

- HTML に `lang` 属性を使います。
- ユーザーを母国語に誘導する - ユーザーが困難なく、国/言語を簡単に変更できるようにします。
- 画像によるテキストを使用することはスケーラブルな方法ではない - 確かに画像にテキストを配置することは、システムに無い見栄えの良いフォントをあらゆるコンピュータに表示させるための一般的な方法です。しかし、画像によるテキストを翻訳するにはテキストごとに各言語用の別々の画像が必要になります。このような画像の変換はほんの少しならいいものの、増えてくるとすぐに管理できなくなってしまいます。
- 制限的な言葉/文章の長さ - 別の言語で書くとコンテンツの長さが変わるので、デザインのレイアウトやオーバーフローの問題に注意します。テキスト量でデザインを決めるのは避けるべきです。文字数は、見出し、ラベル、ボタンなどのものがあります。それらは、本文やコメントなど自由に流れるテキストの問題ではありません。
- 色がどのように認識されているかに注意します。色は言語や文化によって違って見えます。デザインは適切に色を使用する必要があります。
- 日付と通貨の書式設定 - カレンダーの日付が異なる方法で表示されることがあります。例えば。米国の "May 31, 2012" とヨーロッパの "31 May 2012" です。
- 翻訳された文字列を連結しない - `"今日の日付は" + date` のことです。異なる言語で単語の順序は変化するのです。かわりに各言語のパラメータ置換を伴うテンプレート文字列を使用します。たとえば、次の 2 つの文章をそれぞれ日本語と英語で見てみましょう： `私は{% date %}に旅行します` と `I will travel on {% date %}` です。変数の位置は、言語の文法規則によって異なることに注意する必要があります。
- 言語の読む方向 - 英語では、左から右、上から下へ向かって読みますが、日本語では伝統的に、上から下へ、右から左へ向かって読みます。

###### 参考

- https://www.quora.com/What-kind-of-things-one-should-be-wary-of-when-designing-or-developing-for-multilingual-sites

### `data-` 属性は何のために使われるのですか？

JavaScript フレームワークが普及する前に、フロントエンドの開発者は、非標準属性、DOM の余分なプロパティなどの他のハッキングなしで、DOM 内に余分なデータを格納する `data-` 属性を使用しました。カスタムデータをページやアプリケーションに格納する際に、適切な属性や要素が存在しない時のために利用するものです。

しかし近頃は `data-` 属性を使うことは推奨されていません。その理由の 1 つは、ユーザーがブラウザの「検証」を使用してデータ属性を簡単に変更できることです。データモデルは JavaScript 自体の中に保存されるのが良く、ライブラリやフレームワークによるデータバインディングによって DOM とともに更新された状態に保たれることが望ましいです。

###### 参考

- http://html5doctor.com/html5-custom-data-attributes/
- https://www.w3.org/TR/html5/dom.html#embedding-custom-non-visible-data-with-the-data-*-attributes

### HTML5 をオープンウェブプラットフォームとして考えたときに、HTML5 とはどんな要素から成るものですか？

- セマンティクス - コンテンツを正確に記述できるようにします。
- 接続性 - 新しく革新的な方法でサーバーと通信することができます。
- オフラインとストレージ - ウェブページにクライアント側のデータをローカルに格納し、オフラインでより効率的に操作できるようにします。
- マルチメディア - オープンウェブでビデオとオーディオを第一級オブジェクトにする。
- 2D/3D グラフィックスとエフェクト - より多様なプレゼンテーションオプションを可能にします。
- パフォーマンスと統合 - より高速な最適化とコンピュータハードウェアの使い方を提供します。
- デバイスアクセス - さまざまな入出力デバイスの使用を許可します。
- スタイリング - 製作者はより洗練されたテーマを書くことができます。

###### 参考

- https://developer.mozilla.org/en-US/docs/Glossary/HTML5 (英語)

### `cookie`、`sessionStorage`、`localStorage` の違いを教えてください。

これらの技術は、クライアント側の key-value ストレージメカニズムです。彼らは文字列として値を格納することだけができます。

|  | `cookie` | `localStorage` | `sessionStorage` |
| --- | --- | --- | --- |
| イニシエータ | クライアントかサーバ。サーバは `Set-Cookie` ヘッダ使用可 | クライアント | クライアント |
| 有効期限 | 手動で設定　 | 永続　 | タブを閉じるまで |
| ブラウザセッション間で保持するか | 有効期限が設定されているかどうかによって異なります | はい | いいえ |
| すべての HTTP リクエストでサーバーに送信 | クッキーは自動的に `Cookie` ヘッダ経由で送信されます | いいえ | いいえ |
| ドメインごとの容量 | 4kB | 5MB | 5MB |
| アクセシビリティ | ウィンドウ全て | ウィンドウ全て | 同じタブ |

###### 参考

- https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies (英語)
- https://developer.mozilla.org/ja/docs/Web/HTTP/Cookies (日本語)
- http://tutorial.techaltum.com/local-and-session-storage.html

### `<script>`、`<script async>`、`<script defer>` の違いを教えてください。

- `<script>` - HTML 解析がブロックされ、スクリプトがフェッチされてすぐに実行され、スクリプトの実行後に HTML 解析が再開されます。
- `<script async>` - スクリプトは HTML 解析と並行して取得され、利用可能になるとすぐに（HTML 解析が完了する前に）実行されます。スクリプトがページ上の他のスクリプト（アナリティックスなど）と独立している場合は、`async` を使用します。
- `<script defer>` - スクリプトは HTML 解析と並行して取得され、ページの解析が完了すると実行されます。複数のスクリプトがある場合、各遅延スクリプトはドキュメント内で遭遇した順序で実行されます。スクリプトが完全に解析された DOM に依存している場合、`defer` 属性は HTML が実行前に完全に解析されることを保証するのに役立ちます。`<body>` の最後に通常の `<script>` を置くことと大した違いはありません。遅延されたスクリプトは `document.write` を含んではいけません。

注意： `src` 属性を持たないスクリプトでは `async` と `defer` 属性は無視されます。

###### 参考

- http://www.growingwiththeweb.com/2014/02/async-vs-defer-attributes.html
- https://stackoverflow.com/questions/10808109/script-tag-async-defer
- https://bitsofco.de/async-vs-defer/

### なぜ一般的に、CSS の `<link>` を `<head></head>` の間に、JS の `<script>` を `</body>` の直前に置くことが良いと言われているのでしょうか？こうすべきでない例外を知っていますか？

**`<link>` を `<head>` に置く**

`<link>` を頭に置くことは仕様の一部です。それに加えて、上部に配置するとページが徐々にレンダリングされ、ユーザーエクスペリエンスが向上します。ドキュメントの下部にスタイルシートを置くことの問題は、Internet Explorer を含む多くのブラウザでは、プログレッシブレンダリングが禁止されていることです。一部のブラウザでは、スタイルが変更された場合にページの要素を再描画しないようにレンダリングをブロックしています。ユーザーが空白の白いページを見ている。これは、スタイルのないコンテンツのフラッシュを防ぎます。

**`<script>` を `</body>` の直前に置く**

`<script>` は、ダウンロードされて実行されている間に HTML 解析をブロックします。スクリプトを最下部にダウンロードすると、HTML を解析して最初にユーザーに表示することができます。

下に `<script>` の位置付けることの例外は、あなたのスクリプトに `document.write()` が含まれているときですが、最近は `document.write()` を使うのは良い習慣ではありません。また、`<script>` を一番下に置くことは、ドキュメント全体が解析されるまでブラウザがスクリプトのダウンロードを開始できないことを意味します。1 つの回避策は、`<head>` に `<script>` を入れ、`defer` 属性を使うことです。

###### 参考

- https://developer.yahoo.com/performance/rules.html#css_top

### プログレッシブレンダリングとは何ですか？

プログレッシブレンダリングは、ウェブページのパフォーマンスを向上させる（特に、感覚的な読み込み時間を改善する）ために使用される技術に与えられた名前であり、できるだけ早く表示するためにコンテンツをレンダリングします。

ブロードバンドインターネットの普及以前に使われてきましたが、モバイルデータ接続の普及（および信頼性低下）が進んでいる現在、現代的な開発にはまだ役立ちます。

このような技術の例：

- 画像の遅延読み込み - ページ上の画像が一度に読み込まれないようにします。ユーザーが画像を表示するページの部分にスクロールすると、JavaScript が使用されて画像がロードされます。
- 目に見えるコンテンツの優先順位付け（または折り畳みの上のレンダリング） - できるだけ早く表示するためにユーザーのブラウザでレンダリングされるページの量に必要な最小の CSS/コンテンツ/スクリプトのみを含める。スクリプトを呼び出すか、`DOMContentLoaded`/`load` イベントが他のリソースやコンテンツを読み込むのを待ちます。
- 非同期 HTML フラグメント - HTML の一部をブラウザにフラッシュし、ページがバックエンド上に構築されます。この技術の詳細は[こちら](http://www.ebaytechblog.com/2014/12/08/async-fragments-rediscovering-progressive-html-rendering-with-marko/)にあります。

#### References

- https://stackoverflow.com/questions/33651166/what-is-progressive-rendering
- http://www.ebaytechblog.com/2014/12/08/async-fragments-rediscovering-progressive-html-rendering-with-marko/

### img タグに `srcset` 属性を使用する理由は？この属性をもつ要素を評価するときにブラウザが行うプロセスを説明してください。

デバイスの表示幅に応じて異なるイメージをユーザーに提供したい場合は、`srcset` 属性を使用します。Retina ディスプレイに高品質のイメージを表示することでユーザー体験を向上させ、ローエンドのデバイスに低解像度のイメージを提供することでパフォーマンスとデータ量削減に貢献します（ローエンドでは高品質イメージを提供しても綺麗になりません）。例：`<img srcset="small.jpg 500w, medium.jpg 1000w, large.jpg 2000w" src="..." alt="">` はブラウザに小、中、大のいずれかを表示するように指示します。クライアントの解像度に応じて「jpg」グラフィックを表示します。最初の値はイメージ名で、2 番目の値はイメージのピクセル単位の幅です。320px のデバイス幅の場合、次の計算が行われます。

- 500/320 = 1.5625
- 1000/320 = 3.125
- 2000/320 = 6.25

クライアントの解像度が 1x の場合、1.5625 が最も近く、`small.jpg` に対応する `500w` がブラウザによって選択されます。

解像度が Retina（2 倍）の場合、ブラウザは最小以上の最も近い解像度を使用します。つまり、1 より大きく画像が悪く見えるかもしれないので、500w（1.5625）は選択しないということです。ブラウザは得られた比率が 2 に近い 1000w（3.125）の画像を選択します。

`srcset` は、画面の狭いデバイスには、デスクトップディスプレイのような巨大な画像を必要としないため、小さな画像ファイルを配信したいという問題を解決します。また、高密度/高密度スクリーンで異なる解像度の画像を表示させることもできます。

###### 参考

- https://stackoverflow.com/questions/33651166/what-is-progressive-rendering
- http://www.ebaytechblog.com/2014/12/08/async-fragments-rediscovering-progressive-html-rendering-with-marko/

### HTML テンプレート言語をいくつか使用した経験はありますか？

はい。例をあげると、Pug (旧 Jade)、ERB、Slim、Handlebars、Jinja、Liquid を使ったことがあります。私の意見では、これらはおおよそ同じようなものであり、表示されるデータを操作するためのエスケープするコンテンツや役立つフィルタと同様の機能を提供します。ほとんどのテンプレートエンジンでは、表示前にカスタム処理が必要なイベントに独自のフィルタを挿入することもできます。

### 他の方の回答集

- https://neal.codes/blog/front-end-interview-questions-html/
- http://peterdoes.it/2015/12/03/a-personal-exercise-front-end-job-interview-questions-and-my-answers-all/
