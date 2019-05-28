# asciidoc の確認

markdownとの違いとか確認したいので動作確認
syntax等についてtest.adocを参照．

### 使える拡張子
.ad, .adoc, .asc, .asciidoc
(adocが一般的ぽい)

## Reference etc
このへんか
https://asciidoctor.org/docs/asciidoc-syntax-quick-reference/



# Plugin etc

いくつか試すと，VSCodeのPreview機能と，Asciidoctor.js Live Previewの
見えかたが異なる場合がある．またそれぞれ若干表示機能がpoorだったりする．

例： includeの機能(他adocファイルを取り込む)が，Asciidoctor.js live Previewだと
ハイパーリンクになってしまう．一方VSCodeのPreviewではちゃんとインクルードされる．

安定感のあるのはAtom + Asciidoctor plugins (複数個ある) かもしれない．


## for Atom
Atom + Asciidoctorという組み合わせが有名らしいが，Atomが重い．
https://atom.io/users/asciidoctor

## for VS Code
AsciiDoc: joaompinto.asciidoctor-vscode  (ver.2.7.4 for now)
※ 同じ名称でdepcrecatedのextensionもあるので注意のこと．

## Asciidoctor.js Live Preview
for Chrome and Firefox
※ Chrome用が正しく動いてない????
※ FirefoxはOK
※ Safari用はみあたらず

## Github Preview
GithubがasciidocのPreviewに対応しているというirony．



# Install asciidoctor
https://asciidoctor.org/docs/install-asciidoctor-macos/

```
$ brew install asciidoctor
```

## Install Pandoc
Pandoc: https://pandoc.org
```
$ brew install pandoc
```



## Convert Word file to asciidoc file (for test purpose)

```
$ pandoc --from=docx --to=asciidoc --wrap=none --atx-headers --extract-media=media input.docx > output.adoc
```

mediaファイルがtiffになってるので，これらをpngに変更し，
adocファイルの拡張子も.tiffから.pngに変更しておくと，
ツールの「preview」で画像も表示できるようになる．

### adocファイルの分割
chapter毎にsplit




## a) adocからHTMLの生成

```
$ asciidoctor -D [outputdir] INPUT.adoc --backend html5
```
e.g
```
asciidoctor -D OUTPUT/ all.adoc --backend html5
```
これだけだとimageへの参照が切れてしまうので，画像フォルダをコピーする：
```
cp -r src/media OUTPUT/.
```
これでHTMLとしては動作する．


## b) adocからWORDファイル生成
下記参考：
https://rmoff.net/2018/08/22/converting-from-asciidoc-to-ms-word/

```
$ asciidoctor --backend docbook --out-file - [INPUT.adoc] | pandoc --from docbook --to docx --toc --standalone --output [OUTPUT.docx]
```
e.g.
```
asciidoctor --backend docbook --out-file - all.adoc | pandoc --from docbook --to docx --toc --standalone --output OUTPUT/out.docx
```


※ --tocを付けないと ToC (目次) が生成されないので注意．
  --standaloneをつけてもリンク切れ?の警告は生じる．(Word開くときに謎のwarning発生)．
  これらの回避方法は，不明．
