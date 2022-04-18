FROM openjdk:8-jre-alpine
LABEL version=1.0

# OpenRefine 3.4.1 as a based application
ENV OR_URL https://github.com/OpenRefine/OpenRefine/releases/download/3.4.1/openrefine-linux-3.4.1.tar.gz

WORKDIR /or


ENV EXT_LOCAL_FILE_SYSTEM "/or/files"
RUN mkdir /or/files
ADD workspace-files/* /or/files/

RUN set -xe && apk add --no-cache bash curl grep tar && curl -sSL ${OR_URL} | tar xz --strip 1

ADD ./or-configuration/refine.ini /or

ADD ./or-configuration/extensions/ /or/webapp/extensions/
RUN cd /or/webapp/ && ls -l

WORKDIR /or/data
VOLUME /or/data

EXPOSE 3333
ENTRYPOINT ["/or/refine"]
CMD ["-i", "0.0.0.0", "-p", "3333", "-d", "/or/data"]
