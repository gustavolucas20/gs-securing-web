FROM eclipse-temurin:21-alpine

ENV TZ=America/Sao_Paulo

RUN apk --update --no-cache add curl tzdata && \
	ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone && \
	adduser -D -h /app -s /bin/bash someuser && \
	mkdir /app/log && chown someuser /app/log

USER someuser

COPY build/libs/securing-web-0.0.1-SNAPSHOT.jar /app/app.jar

EXPOSE 8080

HEALTHCHECK --interval=30s --timeout=3s --start-period=60s --retries=3 \
	CMD curl -f http://localhost:8080/actuator/health || exit 1

ENTRYPOINT ["java"]
CMD ["-jar", "app.jar"]