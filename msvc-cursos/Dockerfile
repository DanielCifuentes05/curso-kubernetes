FROM eclipse-temurin:21-jdk-alpine as builder

WORKDIR /app/msvc-cursos

COPY ./pom.xml /app
COPY ./msvc-cursos/.mvn ./.mvn
COPY ./msvc-cursos/mvnw .
COPY ./msvc-cursos/pom.xml .

#RUN ./mvnw clean package -Dmaven.test.skip -Dmaven.main.skip -Dspring-boot.repackage.skip && rm -r ./target/
RUN ./mvnw dependency:go-offline # esta es una alternativa de la instruccion de arriba, no descarga todas las dependencias

COPY ./msvc-cursos/src ./src

RUN ./mvnw clean package -DskipTests


FROM eclipse-temurin:21-jdk-alpine

WORKDIR /app

RUN mkdir ./logs
COPY --from=builder /app/msvc-cursos/target/msvc-cursos-0.0.1-SNAPSHOT.jar .

EXPOSE 8002

#ENTRYPOINT ["java","-jar","msvc-cursos-0.0.1-SNAPSHOT.jar"]
CMD ["java","-jar","msvc-cursos-0.0.1-SNAPSHOT.jar"]