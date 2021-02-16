# prisma-base-arm

## Usage

First, build the image

```bash
docker build -t prisma-base-arm:v1.0 .
```

Now you can use it in `Dockerfile`

```
FROM prisma-base-arm:v1.0

RUN mkdir -p /app
WORKDIR /app

ENV PRISMA_QUERY_ENGINE_BINARY=/prisma-arm/query-engine
ENV PRISMA_INTROSPECTION_ENGINE_BINARY=/prisma-arm/introspection-engine
ENV PRISMA_MIGRATION_ENGINE_BINARY=/prisma-arm/migration-engine
ENV PRISMA_FMT_BINARY=/prisma-arm/prisma-fmt

COPY package.json .

RUN npm i

COPY . .

RUN cp /prisma-arm/query-engine /app/node_modules/.prisma/client/query-engine-darwin

RUN npx prisma -v

EXPOSE 4000
```
