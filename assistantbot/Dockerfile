FROM node:jessie

ARG botname
ENV botname ${botname}
RUN apt-get update && apt-get install git mysql-client -y
RUN git clone https://github.com/BakaKiller/discord-assistantbot.git /etc/${botname}
COPY ./config.json /etc/${botname}/config.json
RUN cd /etc/${botname} && npm install
RUN chmod +x /etc/${botname}/bot.js
CMD /etc/${botname}/bot.js