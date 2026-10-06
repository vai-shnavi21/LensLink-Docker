FROM node:20-alpine AS build

WORKDIR /app
COPY package*.json ./
RUN npm ci

ARG REACT_APP_API_URL=http://localhost:8000
ARG REACT_APP_GOOGLE_CLIENT_ID=
ENV REACT_APP_API_URL=$REACT_APP_API_URL \
    REACT_APP_GOOGLE_CLIENT_ID=$REACT_APP_GOOGLE_CLIENT_ID

COPY . ./
RUN npm run build

FROM nginx:1.27-alpine
COPY nginx.conf /etc/nginx/conf.d/default.conf
COPY --from=build /app/build /usr/share/nginx/html
EXPOSE 80
