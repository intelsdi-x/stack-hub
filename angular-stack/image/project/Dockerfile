FROM bitnami/node:12 as builder

ENV NG_CLI_ANALYTICS=false

COPY --chown=1001 user-app /project/user-app

WORKDIR /project/user-app

COPY package*.json ./

RUN npm install

# COPY . .

RUN npm run build

#STAGE2
FROM bitnami/nginx:1.16

ADD ./nginx.conf /opt/bitnami/nginx/conf/nginx.conf

COPY --from=builder --chown=1001 /project/user-app/dist/* /opt/bitnami/nginx/html/
