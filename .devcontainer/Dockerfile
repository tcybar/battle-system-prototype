FROM ubuntu:22.04

# ==============================
# 必要なパッケージのインストール
# git   コード管理のため
# curl  nodejsバージョン管理のnpmをインストールするため
# sudo  node_modulesの権限変更のため
# ==============================
RUN apt update && apt install -y \
    git \
    curl \
    sudo

# ==============================
# 開発用ユーザーを設定
ARG USERNAME=tcybar
ARG GROUPNAME=tcybar
ARG UID=1000
ARG GID=1000
RUN groupadd -g ${GID} ${GROUPNAME} && \
    useradd -m -s /bin/bash -u ${UID} -g ${GID} ${USERNAME}
RUN echo ${USERNAME} ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/${USERNAME} \
    && chmod 0440 /etc/sudoers.d/${USERNAME}
USER ${USERNAME}
# ==============================

# ==============================
# シェルの設定
# ==============================
SHELL ["/bin/bash", "-c"]


# ==============================
# nodejsのインストール
# ==============================
ARG NVM_VERSION=0.39.7
ARG NODE_VERSION=20.12.2
RUN curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v${NVM_VERSION}/install.sh | bash \
    && . $HOME/.nvm/nvm.sh \
    && nvm install ${NODE_VERSION} \
    && nvm use ${NODE_VERSION}
# ==============================

# 作業ディレクトリの設定
WORKDIR /home/${USERNAME}/workspace

ENTRYPOINT ["/bin/bash"]