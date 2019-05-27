# asciidoc の確認

markdownとの違いとか確認したいので動作確認
syntax等についてtest.adocを参照．

### 使える拡張子
.ad, .adoc, .asc, .asciidoc
(adocが一般的ぽい)


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



# Reference etc
このへんか
https://asciidoctor.org/docs/asciidoc-syntax-quick-reference/
