# texlive-sci-ja

TeX Live のイメージです．日本語と理数系，プログラミング系のパッケージが導入されています．また，文章のチェックを行うために textlint を導入しています．VS Code の開発コンテナで使用する目的で作成しています．

導入パッケージ一覧

```
collection-basic
collection-fontsrecommended
collection-langcjk
collection-langjapanese
collection-latex
collection-latexextra
collection-latexrecommended
collection-mathscience
collection-pictures

latexindent
newtx
svg
minted
```

## 開発コンテナのセットアップ

1. VS Code に[Dev Containers](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers)のインストールが必要．
2. `リモートメニューから開発コンテナー構成ファイルを追加`を選択．
3. テンプレート選択画面で次を入力．

```
ghcr.io/yuukin256/texlive-sci-ja/template
```

4. 必要であれば機能を追加し，作成．
5. 必要であれば`.devcontainer/.latexmkrc`を編集．

## Docker Image

GitHub Container Registry

```
docker pull ghcr.io/yuukin256/texlive-sci-ja:latest
```
