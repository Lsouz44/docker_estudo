# importa o maven para build
FROM maven:3.8.4-jdk-8 AS build

# copia os arquivos do src para o /app/src do container docker
COPY src /app/src
# copia o arquivo pom.xml para o /app do container docker
COPY pom.xml /app

# retorna ao /app
WORKDIR /app
# roda o maven no container para instalar todas as dependencias
RUN mvn clean install

# importa um container com o jdk
FROM openjdk:8-jre-alpine

# copia de dentro da build o arquivo .jar para /app/app.jar 
COPY --from=build /app/target/spring-boot-2-hello-world-1.0.2-SNAPSHOT.jar /app/app.jar

# retorna ao /app
WORKDIR /app

# identifica a porta que o container irá utilizar
EXPOSE 8080

# comandos que irá executar ao iniciar o container docker
CMD ["java", "-jar", "app.jar"]