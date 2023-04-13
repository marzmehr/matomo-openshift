FROM redhat/ubi8
# FROM nginx:stable
USER root

RUN yum remove -y nodejs
COPY docker/nginx/nginx.repo /etc/yum.repos.d/

# Required for HTTP Basic feature
RUN yum update -y 
RUN yum install -y openssl ca-certificates

RUN yum install -y nginx
RUN rm -rf /var/lib/apt/lists/*

# support running as arbitrary user which belogs to the root group
RUN chmod g+rwx /var/cache/nginx /var/run /var/log/nginx

# users are not allowed to listen on priviliged ports
RUN sed -i.bak 's/listen\(.*\)80;/listen 8080;/' /etc/nginx/conf.d/default.conf

# Copy config from source to container
ADD docker/nginx/nginx.conf /etc/nginx/

EXPOSE 8080

# Switch to usermode
USER 104