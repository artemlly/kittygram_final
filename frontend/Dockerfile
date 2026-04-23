FROM node:18 AS build
WORKDIR /app

COPY package.json package-lock.json ./
RUN npm ci

COPY . .
RUN npm run build

# Простой HTTP сервер для статики
FROM node:18
WORKDIR /app
RUN npm install -g serve
COPY --from=build /app/build ./build

EXPOSE 8000
CMD ["serve", "-s", "build", "-l", "8000"]