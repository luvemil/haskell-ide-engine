FROM haskell:8.8.4

RUN stack upgrade && stack --resolver ghc-8.8.4 setup

RUN apt-get update -qq -y && apt-get -y install \
    libicu-dev libtinfo-dev libgmp-dev git

RUN git clone https://github.com/haskell/haskell-language-server.git --recurse-submodules

WORKDIR /haskell-language-server

# Ghc x.x.x -> Ghc 8.8.4 (lts-16.19)
RUN sed -i "s/lts-[0-9][0-9].[0-9][0-9]/lts-16.19/" install/stack.yaml
RUN sed -i "s/lts-[0-9][0-9].[0-9][0-9]/lts-16.19/" stack.yaml

# Some reason shake is older version or something...
RUN echo "allow-newer: true" >> /root/.stack/config.yaml

RUN stack ./install.hs hls-8.8.4 \
    && stack install hoogle \
    && stack ./install.hs data \
    && stack clean \
    && rm -r /root/.stack/pantry /root/.stack/snapshots
