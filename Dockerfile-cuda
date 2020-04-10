FROM nvidia/cuda:10.1-cudnn7-runtime-ubuntu18.04

WORKDIR /katago-cuda

RUN groupadd -r katago && useradd -r -g katago katago

RUN apt-get update && apt-get install -y \
    wget \
    unzip \
    libzip-dev \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/* \
  && chown katago:katago /katago-cuda

USER katago

RUN wget -nv https://github.com/lightvector/KataGo/releases/download/v1.3.5/katago-v1.3.5-cuda10.1-linux-x64.zip -O katago-release.zip \
  && wget -nv https://github.com/lightvector/KataGo/releases/download/v1.3.4/g170-b30c320x2-s2271129088-d716970897.bin.gz -O ktnetwork.bin.gz \
  && unzip katago-release.zip \
  && rm -f katago-release.zip \
  && chmod a+x katago

CMD ./katago gtp -config default_gtp.cfg -model ./ktnetwork.bin.gz
