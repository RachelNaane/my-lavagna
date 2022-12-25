FROM maven:3.6.1-jdk-8 AS builder

WORKDIR /app
COPY ./project /app

RUN mvn verify

#

FROM openjdk:8u92-jre-alpine

WORKDIR /app
COPY --from=builder /app/target /app/target
COPY ./entrypoint.sh .

ENV DB_DIALECT MYSQL
ENV DB_URL jdbc:mysql://db:3306/lavagna
ENV DB_USER root
ENV DB_PASS "root"
ENV SPRING_PROFILE dev

ENTRYPOINT sh entrypoint.sh