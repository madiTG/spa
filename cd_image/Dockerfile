FROM public.ecr.aws/nginx/nginx:latest
COPY /build/hello-spa/* /usr/share/nginx/html/
RUN chown -R nginx.nginx /usr/share/nginx/html/*
