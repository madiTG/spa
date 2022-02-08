FROM ubuntu:latest

RUN apt-get update

RUN apt-get install -y git

RUN apt-get install -y curl

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && \
    apt-get install -yq tzdata && \
    ln -fs /usr/share/zoneinfo/Europe/Warsaw /etc/localtime && \
    dpkg-reconfigure -f noninteractive tzdata

RUN cd /tmp

RUN curl -fsSL https://deb.nodesource.com/setup_12.x | bash -

RUN apt-get install -y nodejs

RUN apt-get install -y curl

ADD "https://api.github.com/repos/madiTG/spa/commits?per_page=1" latest_commit

RUN git clone https://github.com/madiTG/spa.git

RUN cd spa && npm install && npm install -g @angular/cli@9.1.15 && npm audit fix && ng --version && ng build --prod

RUN cd spa && \
    git config --global user.email "tomasz.gaska@gmail.com" && \
    git config --global user.name "Tomasz Gaska" && \
    git checkout -b build_`date +"%H%M%d%m%y"` && mv dist build && git add build* --all && git commit -m "build `date`" && git push https://token:$TOKEN@github.com/madiTG/spa.git



