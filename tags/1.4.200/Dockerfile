FROM gcr.io/distroless/java:11

ADD https://repo1.maven.org/maven2/com/h2database/h2/1.4.200/h2-1.4.200.jar /app/h2.jar

WORKDIR /app

ENTRYPOINT ["/usr/bin/java", "-cp" , "/app/h2.jar", "org.h2.tools.Server"]

CMD ["-?"]
