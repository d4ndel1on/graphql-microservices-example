# Multistage build
FROM node:carbon-alpine as builder

WORKDIR /app

COPY . /app
RUN npm install

# Final image
FROM node:carbon-alpine

WORKDIR /app

COPY --from=builder /app /app

# Do not run application as root user
RUN addgroup -g 1001 appuser && \
    adduser -D -u 1001 -G appuser appuser
RUN chown -R appuser:appuser /app
USER appuser

EXPOSE 8080
CMD ["npm", "run", "start"]
