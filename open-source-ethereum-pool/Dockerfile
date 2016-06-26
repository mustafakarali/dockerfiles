FROM golang:1.6

RUN apt-get install git
RUN export GOPATH=$HOME/go \
    && go get github.com/ethereum/ethash \
    && go get github.com/ethereum/go-ethereum/common \
    && go get github.com/gorilla/mux \
    && go get gopkg.in/redis.v3 \
    && go get github.com/yvasiyarov/gorelic
    
RUN export GOPATH=$HOME/go \
    && git clone https://github.com/sammy007/open-ethereum-pool.git \
    && cd open-ethereum-pool \
    && go build -o ether-pool main.go

WORKDIR open-ethereum-pool

ENV threads="2" coin="eth" name="main" \
    proxyenabled="true" proxylisten="0.0.0.0:8888" proxylimitheaderssize="1024" proxylimitbodysize="256" proxybehindreverseproxy="false" \
    stratumenabled="true" stratumlisten="0.0.0.0:8008" stratumtimeout="120s" stratummaxconn="8192" \
    blockrefreshinterval="120ms" stateupdateinterval="3s" difficulty="2000000000" healthCheck="true" maxfails="100" hashrateexpiration="3h" \
    policyworkers="8" resetinterval="60m" refreshinterval="1m" \
      policybanningenabled="false" policybanningipset="blacklist" policybanningtimeout="1800" policybanninginvalidpercent="30" policybanningchecktreshold="30" policybanningmalformedlimit="5" \
      policylimitsenabled="false" policylimitslimit="30" policylimitsgrace="5m" policylimitslimitjump="10" \
    apienabled="false" apilisten="0.0.0.0:8080" apistatscollectinterval="5s" apipurgeinterval="10m" apihashratewindow="30m" apihashratelargewindow="3h" apipayments="50" apiblocks="50" apipurgeonly="false" \
    upstreamcheckinterval="5s" \
    redisendpoint="127.0.0.1:6379" redispoolsize="10" redisdatabase="0" redispassword="" \
    unlockerenabled="false" unlockerpoolfee="1.0" unlockerdonate="true" unlockerdepth="120" unlockerimmaturedepth="20" unlockerinterval="10m" unlockerdeamon="http://127.0.0.1:8545" unlockertimeout="10s" \
    payoutsenabled="false" payoutsrequirepeers="25" payoutsinterval="12h" payoutsdeamon="http://127.0.0.1:8545" payoutstimeout="10s" payoutsadress="0x0" payoutsautogas="true" payoutsgas="21000" payoutsgasprice="50000000000" payoutstreshold="500000000" payoutsbgsave="false"

ADD ./startup.sh .
RUN chmod +x ./startup.sh

ENTRYPOINT ["./startup.sh"]

