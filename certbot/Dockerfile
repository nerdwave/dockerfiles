FROM alpine:latest
MAINTAINER Jessie Frazelle <jess@linux.com>

RUN apk --no-cache add \
	python \
	py-cffi \
	py-configargparse \
	py-configobj \
	py-cryptography \
	py-dialog \
	py-enum34 \
	py-idna \
	py-ipaddress \
	py-mock \
	py-openssl \
	py-parsedatetime \
	py2-pip \
	py-requests \
	py-rfc3339 \
	py-setuptools \
	py-six \
	py-tz \
	py-zope-component \
	py-zope-event \
	py-zope-interface

RUN pip install acme

ENV CERTBOT_VERSION 0.9.3

RUN buildDeps=' \
		git \
	' \
	set -x \
	&& apk --no-cache add $buildDeps \
	&& git clone --depth 1 --branch "v$CERTBOT_VERSION" https://github.com/certbot/certbot /usr/src/certbot \
	&& cd /usr/src/certbot \
	&& python2 setup.py build || return 1 \
	&& python2 setup.py install --prefix=/usr || return 1 \
	&& rm -rf /usr/src/certbot \
	&& apk del $buildDeps \
	&& echo "Build complete."

ENTRYPOINT [ "certbot" ]
