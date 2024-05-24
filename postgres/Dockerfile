##############
# MIGRATIONS #
##############
FROM alpine:3.15.10 as postgres-migrations
ARG WEB3SIGNER_VERSION
WORKDIR /usr/src/app

# Install wget and other dependencies, if necessary
RUN apk --no-cache add wget

# Get migrations from ConsenSys web3signer repository
RUN wget -q https://github.com/ConsenSys/web3signer/archive/refs/tags/${WEB3SIGNER_VERSION}.tar.gz && \
    tar -xvf ${WEB3SIGNER_VERSION}.tar.gz && \
    rm ${WEB3SIGNER_VERSION}.tar.gz

############
# POSTGRES #
############
FROM postgres:14.1-alpine3.15

ARG WEB3SIGNER_VERSION

ENV POSTGRES_PASSWORD=password \
    PGPASSWORD=password \
    POSTGRES_USER=postgres \ 
    POSTGRES_DB=web3signer \
    INITDB_DIR=/docker-entrypoint-initdb.d/

COPY rename_files.sh /usr/local/bin/rename_files.sh

COPY --from=postgres-migrations /usr/src/app/web3signer-${WEB3SIGNER_VERSION}/slashing-protection/src/main/resources/migrations/postgresql/* ${INITDB_DIR}

RUN /usr/local/bin/rename_files.sh

USER postgres

CMD ["postgres"]