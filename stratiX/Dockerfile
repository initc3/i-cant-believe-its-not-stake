FROM ubuntu:16.04
RUN apt-get update
RUN apt-get install -y build-essential libtool autotools-dev automake pkg-config libssl-dev libevent-dev bsdmainutils git cmake libboost-all-dev
RUN apt-get install -y software-properties-common
RUN add-apt-repository -y ppa:bitcoin/bitcoin
RUN apt-get update
RUN apt-get install -y libdb4.8-dev libdb4.8++-dev
RUN apt-get install -y libqrencode-dev
RUN git clone https://github.com/stratisproject/stratisX.git
WORKDIR /stratisX
RUN git checkout 8dd4601d9089dd66132d127a98bfbc035e3b5aab
RUN git submodule update --init --recursive

WORKDIR ./src


RUN apt-get install -y libminiupnpc-dev 
RUN sed -i '107i\    inline bool RegTest() {\ return Params().NetworkID() == CChainParams::REGTEST;\ }' chainparams.h 
RUN sed -i '74i\    if (RegTest()) return true;' checkpoints.cpp
RUN sed -i '84i\    if (RegTest()) return true;' checkpoints.cpp
RUN sed -i '63s/TestNet()/TestNet() || RegTest()/' main.h
RUN sed -i '2465s/TestNet()/TestNet() || RegTest()/' main.cpp
RUN sed -i '2062,2063{s/^/\/\//}' main.cpp # This removes a check for nBits


RUN make -f makefile.unix

WORKDIR ../

ADD test/ /stratisX/test/
ADD ./stratisx-nothingatstake.py /stratisX/test/functional/
# nothing at stake
CMD [ "python3", "-u","./test/functional/stratisx-nothingatstake.py" ]
# CMD tail -f /dev/null