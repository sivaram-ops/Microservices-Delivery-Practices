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
ENV AMQP_USER=roboshop AMQP_PASS=roboshop123 PYTHONUNBUFFERED=1
COPY --from=builder /dependencies /usr/local/lib/python3.9/site-packages/
COPY *.py /app/
COPY payment.ini /app/
CMD ["uwsgi", "--ini", "payment.ini"]