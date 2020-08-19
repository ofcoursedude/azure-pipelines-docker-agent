FROM ubuntu:20.04

# To make it easier for build and release pipelines to run apt-get,
# configure apt to not require confirmation (assume the -y argument by default)
ENV DEBIAN_FRONTEND=noninteractive
RUN echo "APT::Get::Assume-Yes \"true\";" > /etc/apt/apt.conf.d/90assumeyes

RUN apt-get update \
&& apt-get install -y --no-install-recommends \
        ca-certificates \
        curl \
        jq \
        git \
        iputils-ping \
        libcurl4 \
        libunwind8 \
        netcat \
        libssl1.0 \
&& rm -rf /var/lib/apt/lists/*

# install docker cli
RUN apt-get update \
&& apt-get install docker.io \
&& rm -rf /var/lib/apt/lists/* 

# install node
RUN curl -sL https://deb.nodesource.com/setup_12.x | bash -
RUN apt-get update \
&& apt-get install -y nodejs \
&& rm -rf /var/lib/apt/lists/*

# install .netcore sdk
RUN curl https://packages.microsoft.com/config/ubuntu/20.04/packages-microsoft-prod.deb -o packages-microsoft-prod.deb \
&& dpkg -i packages-microsoft-prod.deb
RUN apt-get update \
&& apt-get install dotnet-sdk-3.1 \
&& rm -rf /var/lib/apt/lists/*

# install build essentials
RUN apt-get update \
&& apt-get install build-essential \
&& rm -rf /var/lib/apt/lists/*

# install golang 1.15
RUN curl -L https://golang.org/dl/go1.15.linux-amd64.tar.gz --output go.tar.gz \
&& tar -C /usr/local -xzf go.tar.gz \
&& rm go.tar.gz
# setup go path
ENV PATH="$PATH:/usr/local/go/bin"

WORKDIR /azp

COPY ./start.sh .
RUN chmod +x start.sh

CMD ["./start.sh"]
