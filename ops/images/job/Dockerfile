FROM python:3.7-alpine
# Specify label-schema specific arguments and labels.
ARG BUILD_DATE
ARG VCS_REF
ARG VERSION="NA"

LABEL org.label-schema.build-date=$BUILD_DATE \
    org.label-schema.name="industrycoin Job" \
    org.label-schema.description="The job image provides a utility for running administrative tasks in a deployment." \
    org.label-schema.url="https://idtoken.pro" \
    org.label-schema.vcs-ref=$VCS_REF \
    org.label-schema.vcs-url="https://github.com/industrycoinco/web/ops/images/job" \
    org.label-schema.vendor="industrycoin" \
    org.label-schema.version=$VERSION \
    org.label-schema.schema-version="1.0"
ENV LANG en_US.utf8
RUN apk add --no-cache --update bash dumb-init postgresql-client py3-magic && \
    pip install awscli s3cmd && \
    mkdir -p /jobs/backups
WORKDIR /jobs
COPY entry.sh /bin/entry.sh
ENTRYPOINT ["/usr/bin/dumb-init", "--"]
CMD ["/bin/entry.sh"]
