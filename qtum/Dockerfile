FROM ubuntu:16.04

RUN apt-get update
RUN apt-get install -y build-essential libtool autotools-dev automake pkg-config libssl-dev libevent-dev bsdmainutils git cmake libboost-all-dev
RUN apt-get install -y software-properties-common
RUN add-apt-repository -y ppa:bitcoin/bitcoin
RUN apt-get update
RUN apt-get install -y libdb4.8-dev libdb4.8++-dev

RUN git clone https://github.com/qtumproject/qtum.git
WORKDIR /qtum
RUN git checkout 21e3d401f49f64059eb90d51c5919d4713b93f8f
RUN git submodule update --init --recursive
RUN sed -i '104i\    obj.push_back(Pair("mapBlockIndex-size",        mapBlockIndex.size()));' src/rpc/misc.cpp
RUN ./autogen.sh
RUN ./configure
RUN make

# unit tests
#RUN make check

# regression and integration tests
#RUN python3 test/functional/test_runner.py

ADD ./qtum-nothingatstake.py /qtum/test/functional/
# nothing at stake
CMD [ "python3", "-u","./test/functional/qtum-nothingatstake.py" ]
