FROM node:20.19.6-alpine3.21 AS build
WORKDIR /opt/server
COPY *.js .
# this may add extra cache memory
COPY package.json .
RUN npm install 

FROM node:20.19.6-alpine3.21
WORKDIR /opt/server
# Create a group and user
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop && \
    chown -R roboshop:roboshop /opt/server
EXPOSE 8080
LABEL com.project="roboshop" \
      component="user" \
      created_by="NareshU"

ENV MONGO="true" \
    REDIS_URL="redis://redis:6379" \
    MONGO_URL="mongodb://mongodb:27017/users"
COPY --from=build --chown=roboshop:roboshop /opt/server /opt/server
USER roboshop

CMD ["server.js"]
ENTRYPOINT ["node"]


# FROM node:20
# WORKDIR /opt/server
# EXPOSE 8080
# COPY package.json .
# COPY *.js .
# RUN npm install
# ENV MONGO="true" \
#     REDIS_URL="redis://redis:6379" \
#     MONGO_URL="mongodb://mongodb:27017/users"
# CMD ["node", "server.js"]