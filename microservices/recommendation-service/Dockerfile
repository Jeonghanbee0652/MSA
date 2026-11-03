FROM eclipse-temurin:24_36-jre-noble AS builder
WORKDIR extracted
ADD ./build/libs/*.jar app.jar
RUN java -Djarmode=tools -jar app.jar extract --layers --launcher --destination extracted

FROM eclipse-temurin:24_36-jre-noble
WORKDIR application
COPY --from=builder extracted/extracted/dependencies/ ./
COPY --from=builder extracted/extracted/spring-boot-loader/ ./
COPY --from=builder extracted/extracted/snapshot-dependencies/ ./
COPY --from=builder extracted/extracted/application/ ./

EXPOSE 8080

ENTRYPOINT ["java", "org.springframework.boot.loader.launch.JarLauncher"]
