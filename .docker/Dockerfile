FROM node:20.13.0-alpine as build

WORKDIR /app

ENV PNPM_HOME="/pnpm"
ENV PATH="$PNPM_HOME:$PATH"
RUN corepack enable

COPY package.json /app
COPY pnpm-lock.yaml /app

RUN --mount=type=cache,id=pnpm,target=/pnpm/store pnpm install --frozen-lockfile

COPY . /app

RUN pnpm run build

FROM gcr.io/distroless/nodejs20

WORKDIR /app

COPY --from=build /app/.output /app

EXPOSE 3000/tcp

CMD ["/app/server/index.mjs"]
