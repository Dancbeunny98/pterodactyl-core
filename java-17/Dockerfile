FROM openjdk:17-jdk-buster

RUN printf "deb [arch=amd64] https://apt.bell-sw.com/ stable main" > /etc/apt/sources.list.d/bellsoft.list

RUN wget -q -O - https://download.bell-sw.com/pki/GPG-KEY-bellsoft | apt-key add - \
    && echo "deb [arch=amd64] https://apt.bell-sw.com/ stable main" | tee /etc/apt/sources.list.d/bellsoft.list \
    && apt update -y \
    && apt upgrade -y \
    && apt install openssl -y \
    && apt install lib32z1 -y \
    && apt install bellsoft-java11-full -y \
    && ln -s /usr/lib/jvm/bellsoft-java17-full-amd64/bin/java /usr/lib/jvm/default-java \
    && apt install -y openjfx curl ca-certificates openssl git tar bash sqlite fontconfig \
    && adduser -D -h /home/container container

USER container
ENV  USER=container HOME=/home/container

WORKDIR /home/container

COPY ./entrypoint.sh /entrypoint.sh

CMD ["/bin/bash", "/entrypoint.sh"]
