FROM debian

RUN apt-get update

# Needed for debian repositories added below.
RUN apt-get install -y curl gnupg

# Installs node.
RUN curl -sL https://deb.nodesource.com/setup_14.x | bash - && \
    apt-get install -y nodejs

# Installs yarn.
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - && \
    echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list && \
    apt-get update && apt-get install -y yarn

# Installs VS Code build deps.
RUN apt-get install -y build-essential \
                   libsecret-1-dev \
                   libx11-dev \
                   libxkbfile-dev

# Installs envsubst.
RUN apt-get install -y gettext-base

# Misc build dependencies.
RUN apt-get install -y jq git rsync

# Installs shellcheck.
RUN curl -L https://github.com/koalaman/shellcheck/releases/download/v0.7.1/shellcheck-v0.7.1.linux.$(uname -m).tar.xz | \
    tar -xJ && \
    mv shellcheck*/shellcheck /usr/local/bin && \
    rm -R shellcheck*

# Install Go dependencies
RUN ARCH="$(dpkg --print-architecture)" && \
    curl "https://dl.google.com/go/go1.14.2.linux-$ARCH.tar.gz" | tar -C /usr/local -xz
ENV PATH=/usr/local/go/bin:/root/go/bin:$PATH
ENV GO111MODULE=on
RUN go get mvdan.cc/sh/v3/cmd/shfmt
RUN go get github.com/goreleaser/nfpm/cmd/nfpm
