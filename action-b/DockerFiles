FROM debian:9.5-slim

ADD entrypoint.sh /entrypoint.sh
RUN chmod -x entrypoint.sh
RUN echo 'must lowcase for f'
ENTRYPOINT ["/entrypoint.sh"]
