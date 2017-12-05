FROM alpine:3.3
RUN apk --update add git && rm -rf /var/cache/apk/*
RUN git clone https://github.com/emqtt/emq-relx.git
RUN apk --update add build-base gcc abuild binutils binutils-doc gcc-doc
RUN apk --update add erlang perl && rm -rf /var/cache/apk/*
RUN apk --update add erlang-dev erlang-erl-interface erlang-dev erlang-parsetools erlang-tools && rm -rf /var/cache/apk/*
RUN apk --update add erlang-crypto erlang-syntax-tools erlang-parsetools \
                     erlang-inets erlang-ssl erlang-public-key \
                     erlang-eunit && rm -rf /var/cache/apk/*
RUN apk --update add bsd-compat-headers && rm -rf /var/cache/apk/*
RUN cd emq-relx && make

FROM alpine:3.3
RUN apk --update add erlang && rm -rf /var/cache/apk/*
COPY --from=0 /emq-relx .
CMD ["cd _rel/emqttd && ./bin/emqttd console"]
