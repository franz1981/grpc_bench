FROM hseeberger/scala-sbt:11.0.7_1.3.13_2.11.12 as BUILDER

WORKDIR /app
COPY scala_zio_bench /app
COPY proto/helloworld/helloworld.proto /app/src/main/protobuf/helloworld.proto

RUN sbt assembly

FROM eclipse-temurin:20.0.1_9-jdk-jammy

ENV GC "-XX:+UseParallelGC"
ENV _JAVA_OPTIONS "${GC} -XX:MinRAMPercentage=70 -XX:MaxRAMPercentage=70"

COPY --from=builder /app/target/scala-2.13/zio-grpc-quickstart-scala-assembly-1.0.jar .

ENTRYPOINT ["java", "-jar", "zio-grpc-quickstart-scala-assembly-1.0.jar"]
