FROM openjdk:11-jre-slim as builder
WORKDIR application
ADD maven/mssc-inventory-failover-0.0.1-SNAPSHOT.jar mssc-inventory-failover-0.0.1-SNAPSHOT.jar
RUN java -Djarmode=layertools -jar mssc-inventory-failover-0.0.1-SNAPSHOT.jar extract

FROM openjdk:11-jre-slim
LABEL PROJECT_NAME=mssc-inventory-failover \
      PROJECT=guru.sfg.brewery:mssc-inventory-failover:jar:0.0.1-SNAPSHOT

EXPOSE 8083

WORKDIR application
COPY --from=builder application/dependencies/ ./
COPY --from=builder application/spring-boot-loader/ ./
COPY --from=builder application/snapshot-dependencies/ ./
COPY --from=builder application/application/ ./
ENTRYPOINT ["java", "-Djava.security.egd=file:/dev/./urandom", "org.springframework.boot.loader.JarLauncher"]
