FROM pddg/latex:3.1.0

ARG USERNAME
ARG UID
ARG GID

# Dev Container内ではMakefileでDockerを使う機能を無効にする
ENV USE_DOCKER=no

WORKDIR /workspace

RUN curl -sL https://deb.nodesource.com/setup_lts.x | bash \
    && re
    && apt-get install -y --no-install-recommends \
    build-essential \
    git \
    nodejs \
    cpanminus \
    && apt-get clean \
    && apt-get autoremove -y \
    && rm -rf /var/lib/apt/lists/*

RUN cpanm -n YAML::Tiny File::HomeDir Unicode::GCString

## 追加のパッケージをインストールしたい場合はここに記述
RUN tlmgr update --self && \
    tlmgr install latexindent

RUN useradd -u $UID -o -m $USERNAME
RUN groupmod -g $GID -o $USERNAME
RUN cp /.latexmkrc /home/${USERNAME}/
