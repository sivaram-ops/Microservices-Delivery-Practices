# stage 1
FROM node:alpine AS builder
WORKDIR /build-dir
COPY package.json ./
RUN npm install --production

# stage 2
FROM node:alpine
WORKDIR /catalogue
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop
RUN chown roboshop:roboshop /catalogue
USER roboshop
EXPOSE 8080
ENV NODE_ENV=production
ENV MONGO='true' 
COPY --from=builder /build-dir/node_modules ./node_modules
COPY server.js .
CMD ["node", "server.js"]