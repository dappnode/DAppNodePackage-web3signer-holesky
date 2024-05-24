ARG FLYWAY_VERSION
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

##########
# FLYWAY #
##########
ARG FLYWAY_VERSION
FROM flyway/flyway:${FLYWAY_VERSION}-alpine
ARG WEB3SIGNER_VERSION

RUN apk update && apk --no-cache add postgresql-client
COPY entrypoint.sh /usr/local/bin/entrypoint.sh
RUN chmod +x /usr/local/bin/entrypoint.sh && rm -rf /flyway/sql/*
COPY --from=postgres-migrations /usr/src/app/web3signer-${WEB3SIGNER_VERSION}/slashing-protection/src/main/resources/migrations/postgresql/* /flyway/sql/
ENTRYPOINT ["entrypoint.sh"]
