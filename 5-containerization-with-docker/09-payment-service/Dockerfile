FROM python:3.9.18-alpine3.19
WORKDIR /app
RUN apk add python3-dev build-base linux-headers pcre-dev
COPY requirements.txt .
RUN pip install -r requirements.txt
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop
COPY *.py /app/
COPY payment.ini /app/
EXPOSE 8080
CMD ["uwsgi", "--ini", "payment.ini"]