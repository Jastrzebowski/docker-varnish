FROM buildpack-deps:jessie

MAINTAINER Karol Jastrzebowski <karol.jastrzebowski@gmail.com>

RUN curl https://repo.varnish-cache.org/GPG-key.txt | apt-key add -

ENV VARNISH_VERSION 4.0

RUN echo "deb http://repo.varnish-cache.org/debian/ jessie varnish-$VARNISH_VERSION" >> \
  /etc/apt/sources.list.d/varnish-cache.list

RUN apt-get update && apt-get install -y --no-install-recommends \
  varnish \
  varnish-agent \
  && rm -rf /var/lib/apt/lists/*

EXPOSE 6081 6085

RUN echo varnish:agent > /etc/varnish/agent_secret

ENTRYPOINT ["varnishd", "-F"]

CMD ["-n", "varnish", "-a", ":6081", "-f", "/etc/varnish/boot.vcl"]
