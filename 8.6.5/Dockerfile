FROM ciantic/haskell-ide-engine:ghc8.6.5

ENV SHELL /bin/bash

RUN chmod o+x /root/.local/bin
RUN cp /root/.local/bin/hie* /usr/local/bin
RUN useradd -ms /bin/bash jack