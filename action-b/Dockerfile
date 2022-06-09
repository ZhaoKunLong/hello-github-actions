FROM debian:9.5-slim

ADD test.sh /test.sh
ADD sayHello.sh /sayHello.sh
RUN chmod +x /sayHello.sh
RUN ls -all
ENTRYPOINT ["sh","-C", "/test.sh"] 