6- payment (python):
---
# stage 1
FROM python:3.9.18-alpine3.19 AS builder
WORKDIR /install
RUN apk add --no-cache python3-dev build-base linux-headers pcre-dev
COPY requirements.txt .
RUN pip install --target=/dependencies -r requirements.txt
# stage 2
FROM python:3.9.18-alpine3.19
WORKDIR /app
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop
USER roboshop
EXPOSE 8080
ENV PYTHONUNBUFFERED=1
COPY --from=builder /dependencies /usr/local/lib/python3.9/site-packages/
COPY *.py /app/
COPY payment.ini /app/
CMD ["uwsgi", "--ini", "payment.ini"]
---
command:
docker run -d --name payment --network=networkname -p 8080 -e AMQP_USER=roboshop -e AMQP_PASS=roboshop123 imagename:version


9- mysql:
---
FROM mysql:5.7
ENV MYSQL_DATABASE=cities MYSQL_ROOT_PASSWORD=RoboShop@1 MYSQL_USER=shipping MYSQL_PASSWORD=RoboShop@1
COPY shipping.sql /docker-entrypoint-initdb.d/shipping.sql
---
command:
docker run -d --name mysql --network networkname -e MYSQL_DATABASE=cities -e MYSQL_ROOT_PASSWORD=RoboShop@1 -e MYSQL_USER=shipping -e MYSQL_PASSWORD=RoboShop@1 imagename:version


10- rabbitmq:
---
FROM rabbitmq
ENV RABBITMQ_DEFAULT_USER=roboshop RABBITMQ_DEFAULT_PASS=roboshop123
---
command:
docker run -d --name mysql --network networkname -e RABBITMQ_DEFAULT_USER=roboshop -e RABBITMQ_DEFAULT_PASS=roboshop123 imagename:version