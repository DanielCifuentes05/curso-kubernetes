FROM eclipse-temurin:21-jdk-alpine as builder

WORKDIR /app/msvc-gateway

COPY ./pom.xml /app
COPY ./msvc-gateway/.mvn ./.mvn
COPY ./msvc-gateway/mvnw .
COPY ./msvc-gateway/pom.xml .

#RUN ./mvnw clean package -Dmaven.test.skip -Dmaven.main.skip -Dspring-boot.repackage.skip && rm -r ./target/
RUN ./mvnw dependency:go-offline # esta es una alternativa de la instruccion de arriba, no descarga todas las dependencias

COPY ./msvc-gateway/src ./src

RUN ./mvnw clean package -DskipTests


FROM eclipse-temurin:21-jdk-alpine

WORKDIR /app

RUN mkdir ./logs
COPY --from=builder /app/msvc-gateway/target/msvc-gateway-0.0.1-SNAPSHOT.jar .

EXPOSE 8090

CMD ["java","-jar","msvc-gateway-0.0.1-SNAPSHOT.jar"]