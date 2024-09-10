FROM node:20.9.0 as builder

WORKDIR /build_dir

COPY src/portal /build_dir


RUN npm install -g npm@10.8.3
RUN npm install
RUN node --max_old_space_size=2048 'node_modules/@angular/cli/bin/ng' build --configuration production

FROM nginx:1.17



COPY --from=builder /build_dir/dist /usr/share/nginx/html
COPY src/portal/docker-build/nginx.conf /etc/nginx/nginx.conf

EXPOSE 8080
VOLUME /var/cache/nginx /var/log/nginx /run

STOPSIGNAL SIGQUIT

HEALTHCHECK CMD curl --fail -s http://127.0.0.1:8080 || exit 1
USER nginx
CMD ["nginx", "-g", "daemon off;"]
