# wechaty ubuntu运行环境

基于[wechaty](https://github.com/wechaty/wechaty) 0.65.15 docker 镜像提取出来的Ubuntu运行环境

## 运行说明

1. 下载代码

   ```shell
   git clone https://github.com/IronXiao/wechaty-env-ubuntu.git
   ```

2. 安装依赖

   ```shell
   apt-get update \
     && apt-get install -y --no-install-recommends \
       apt-utils \
       autoconf \
       automake \
       bash \
       build-essential \
       ca-certificates \
       curl \
       coreutils \
       ffmpeg \
       figlet \
       git \
       gnupg2 \
       jq \
       libgconf-2-4 \
       libtool \
       moreutils \
       python-dev \
       shellcheck \
       sudo \
       tzdata \
       vim \
       wget \
       libxtst6 \
     && apt-get purge --auto-remove \
     && rm -rf /tmp/* /var/lib/apt/lists/*
   
   curl -sL https://deb.nodesource.com/setup_14.x | sudo -E bash - \
       && apt-get update && apt-get install -y --no-install-recommends nodejs \
       && apt-get purge --auto-remove \
       && rm -rf /tmp/* /var/lib/apt/lists/*
   
   # https://github.com/GoogleChrome/puppeteer/blob/master/docs/troubleshooting.md
   # https://github.com/ebidel/try-puppeteer/blob/master/backend/Dockerfile
   # Install latest chrome dev package.
   # Note: this also installs the necessary libs so we don't need the previous RUN command.
   wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add - \
     && sh -c 'echo "deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google.list' \
     && apt-get update \
     && apt-get install -y --no-install-recommends \
       google-chrome-unstable \
     && apt-get purge --auto-remove \
     && rm -rf /tmp/* /var/lib/apt/lists/* \
     && rm -rf /usr/bin/google-chrome* /opt/google/chrome-unstable
   ```

3. 运行

   ```shell
   export WECHATY_LOG="verbose"
   export WECHATY_PUPPET="wechaty-puppet-padlocal"
   # http://pad-local.com/ 申请
   export WECHATY_PUPPET_PADLOCAL_TOKEN="puppet_padlocal_XXXXXXXXXXXX"
   export WECHATY_PUPPET_SERVER_PORT="8878"
   # uuidgen
   export WECHATY_TOKEN="yyyyyyyyyyyyyyyyyyyyyyyyy"
   export WECHATY_PUPPET_SERVICE_NO_TLS_INSECURE_CLIENT="true"
   export WECHATY_PUPPET_SERVICE_NO_TLS_INSECURE_SERVER="true"
   ```

   ```shell
   ./bin/entrypoint.sh
   ```

## Troubleshoting

1. gitpod 运行出错

   ```shell
   which node
   
   rm -rf /home/gitpod/.nvm/versions/node/
   ```


