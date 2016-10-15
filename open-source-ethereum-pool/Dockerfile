FROM golang:1.6

RUN apt-get update && apt-get install -y git software-properties-common && \
    add-apt-repository -y ppa:ethereum/ethereum && \
    add-apt-repository -y ppa:ethereum/ethereum-dev && \
    apt-get update && \
    apt-get install -y ethereum

     
RUN git clone https://github.com/sammy007/open-ethereum-pool.git && \
    cd open-ethereum-pool && \
    make


RUN ./build/bin/open-ethereum-pool config.json 



WORKDIR open-ethereum-pool

ADD ./startup.sh .
RUN chmod +x ./startup.sh

ENTRYPOINT ["./startup.sh"]

