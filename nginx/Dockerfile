FROM nginx:stable


RUN apt-get update \
&& apt-get install -y --no-install-recommends iputils-ping curl \
&& rm -rf /var/lib/apt/lists/*


COPY nginx.conf /etc/nginx/nginx.conf


EXPOSE 8080
CMD ["nginx", "-g", "daemon off;"]
