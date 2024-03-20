FROM mongo:7

ARG MONGO_INITDB_ROOT_USERNAME
ARG MONGO_INITDB_ROOT_PASSWORD
ARG MONGO_PORT

ENV MONGO_INITDB_ROOT_USERNAME=${MONGO_INITDB_ROOT_USERNAME}
ENV MONGO_INITDB_ROOT_PASSWORD=${MONGO_INITDB_ROOT_PASSWORD}

#  Auth key file
COPY example-replica.key /data/replica.key

RUN ls -l /data

# Needed permissions for keyFile : https://www.mongodb.com/docs/v7.0/tutorial/enforce-keyfile-access-control-in-existing-replica-set/
RUN chmod 400 /data/replica.key
RUN chown 999:999 /data/replica.key

RUN ls -l /data

EXPOSE ${MONGO_PORT}

CMD ["mongod", "--bind_ip_all", "--replSet", "dbrs", "--keyFile", "/data/replica.key"]
