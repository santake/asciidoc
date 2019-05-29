# asciidoc の動作確認

markdownとの違いとか確認したいので動作確認
syntax等についてtest.adocを参照．

### 使える拡張子
.ad, .adoc, .asc, .asciidoc
(adocが一般的ぽい)

## Reference etc
このへんか
https://asciidoctor.org/docs/asciidoc-syntax-quick-reference/


# Plugin etc
いくつか試す．
VSCodeのPreview機能，AtomのPreview, Asciidoctor.js Live Preview，
それぞれ見えかたが若干異なるので，どれをデファクトにしていいか困る．

例： includeの機能(他adocファイルを取り込む)が，Asciidoctor.js live Previewだと
ハイパーリンクになってしまう．一方VSCodeのPreviewではちゃんとインクルードされる．

比較的安定感があるのは，Atom + Asciidoctor plugins かもしれない… と思ったが，
Syntaxハイライトが，Atomの場合は，途中で力つきて，一色だけになってしまう場合がある．
何かがトリガになって一色化している可能性もある．(ただ同ファイルをVSCodeで見ても問題なくハイライトさせている)

Syntaxハイライトという面ではVSCodeが安定．ただしPreviewがしょぼいのでAtomで見たほうがいい．


*結局，どれ使っても困るってこと*




## for Atom
Atom + Asciidoctorという組み合わせが有名らしいが，Atomが重い．
https://atom.io/users/asciidoctor
Atom用asciidoctorプラグインは4つくらいあるので，とりあえず全部入りにする．

## for VS Code
AsciiDoc: joaompinto.asciidoctor-vscode  (ver.2.7.4 for now)
※ 同じ名称でdepcrecatedのextensionもあるので注意のこと．


## Asciidoctor.js Live Preview
for Chrome and Firefox
※ Chrome用が正しく動いてない????
※ Firefoxもアップデートがはいってから動作せず
※ Safari用はみあたらず

## Github Preview
GithubがasciidocのPreviewに対応しているというirony．


# asciidocのフォーマット変換ツール

## asciidoctor
https://asciidoctor.org/docs/install-asciidoctor-macos/

asciidocに関する各種utilities．

```
$ brew install asciidoctor
```

## Pandoc
Pandoc: https://pandoc.org

Wordなどの他フォーマットに変換する(もしくはWordからadocに変換する)のに使用．

```
$ brew install pandoc
```


# Convert Word file to asciidoc file (for test purpose)

```
$ pandoc --from=docx --to=asciidoc --wrap=none --atx-headers --extract-media=media input.docx > output.adoc
```

mediaファイルがtiffになってるので，これらをpngに変更し，
adocファイルの拡張子も.tiffから.pngに変更しておくと，
ツールの「preview」で画像も表示できるようになる．

### adocファイルの分割
chapter毎にsplit






# Convert Asciidoc with other formats

## a) adoc to HTML

```
$ asciidoctor -D [outputdir] INPUT.adoc --backend html5
```
e.g
```
asciidoctor -D OUTPUT/ all.adoc --backend html5 --doctype book
```
これだけだとimageへの参照が切れてしまうので，画像フォルダをコピーする：
```
cp -r src/media OUTPUT/.
```
これでHTMLとしては動作する．


### CLI options of 'asciidoctor'
https://asciidoctor.org/docs/user-manual/#cli-options


asciidoctor -D OUTPUT/ all.adoc --backend html5 --doctype
asciidoctor -D OUTPUT/ all.adoc --backend html5 --doctype




## b) adoc to docx (word)
下記参考：
https://rmoff.net/2018/08/22/converting-from-asciidoc-to-ms-word/

```
$ asciidoctor --backend docbook --out-file - [INPUT.adoc] | pandoc --from docbook --to docx --toc --standalone --output [OUTPUT.docx]
```
e.g.
```
asciidoctor --backend docbook --out-file - all.adoc | pandoc --from docbook --to docx --toc --standalone --output OUTPUT/out.docx
```


※ --tocを付けないと ToC (目次) がWord内に生成されないので注意．
ただしWordファイルのTOCがこわれかけた状態で生成されてしまう．
警告ダイアログでupdate > YESとしておく必要がある(今後どうなるか不明)．

--standaloneをつけてもリンク切れ?の警告は生じる．
