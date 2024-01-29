FROM node:20-alpine as build

WORKDIR /app

RUN corepack enable

COPY package.json /app
COPY pnpm-lock.yaml /app

RUN pnpm install

COPY . /app

RUN pnpm run build

FROM gcr.io/distroless/nodejs20

WORKDIR /app

COPY --from=build /app/.output /app

EXPOSE 3000/tcp

CMD ["/app/server/index.mjs"]
