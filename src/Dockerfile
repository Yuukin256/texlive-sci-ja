FROM buildpack-deps:bookworm-scm

ARG TEXLIVE_MIRROR=https://tug.ctan.org/systems/texlive/tlnet

ENV PATH=/usr/local/texlive/bin:$PATH

WORKDIR /texlive-install

COPY ./texlive.profile .

# texliveをインストール
RUN wget ${TEXLIVE_MIRROR}/install-tl-unx.tar.gz \
  && tar -xf install-tl-unx.tar.gz --strip-components 1 \
  && ./install-tl -profile texlive.profile --location ${TEXLIVE_MIRROR} \
  && ln -sf /usr/local/texlive/*/bin/* /usr/local/texlive/bin

# latexmk, latexindent, newtx, svg, mintedのインストール
RUN tlmgr update --self --all && \
  tlmgr install \
  latexmk \
  latexindent \
  newtx \
  svg \
  minted

# jlisting.sty を配置
COPY ./jlisting.sty /usr/local/texlive/texmf-local/tex/latex/jlisting/jlisting.sty

# GhostscriptとGnuplot、latexindentに必要なパッケージをインストール
RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
  && apt-get -y install --no-install-recommends ghostscript gnuplot \
  libyaml-tiny-perl libfile-homedir-perl libunicode-linebreak-perl \
  nodejs npm \
  && rm -rf /var/lib/apt/lists/*

WORKDIR /usr/local/texlive/texmf-local/tex/latex/gnuplot

# gnuplot-lua-tikzをインストール
RUN gnuplot -e 'set term tikz createstyle' \
  && mktexlsr

WORKDIR /

# textlintをインストール
RUN npm install -g textlint  textlint-filter-rule-comments \
  textlint-rule-preset-ja-spacing textlint-rule-preset-ja-technical-writing \
  textlint-plugin-latex2e

RUN rm -rf /texlive-install