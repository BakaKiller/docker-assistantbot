FROM node:jessie

ARG botname
ENV botname ${botname}

RUN apt-get update && apt-get install git mysql-client -y
RUN git clone https://github.com/BakaKiller/discord-assistantbot.git /etc/${botname}

COPY ./config.json /etc/${botname}/config.json
COPY ./startscript /startscript
RUN chmod +x /etc/${botname}/bot.js
RUN chmod +x /etc/${botname}/installdb
RUN chmod +x /startscript

RUN cd /etc/${botname} && npm install

ARG dbhost
ARG dbname
ARG dbuser
ARG dbpwd

ARG config_roles
ARG config_prefix
ARG config_token
ARG config_debugchan
ARG config_askchan
ARG config_askadminchan
ARG config_lang
ARG config_timezone

ENV dbhost ${dbhost}
ENV dbname ${dbname}
ENV dbuser ${dbuser}
ENV dbpwd ${dbpwd}

ENV config_timezone ${config_timezone}

RUN ln -snf /usr/share/zoneinfo/${config_timezone} /etc/localtime && echo ${config_timezone} > /etc/timezone

RUN sed -i "s~CONFIGROLES~${config_roles}~g" /etc/${botname}/config.json
RUN sed -i s~CONFIGPREFIX~${config_prefix}~g /etc/${botname}/config.json
RUN sed -i s~CONFIGTOKEN~${config_token}~g /etc/${botname}/config.json
RUN sed -i s~CONFIGDEBUGCHAN~${config_debugchan}~g /etc/${botname}/config.json
RUN sed -i s~CONFIGASKCHAN~${config_askchan}~g /etc/${botname}/config.json
RUN sed -i s~CONFIGASKADMINCHAN~${config_askadminchan}~g /etc/${botname}/config.json
RUN sed -i s~CONFIGLANG~${config_lang}~g /etc/${botname}/config.json
RUN sed -i s~DBHOST~${dbhost}~g /etc/${botname}/config.json
RUN sed -i s~DBNAME~${dbname}~g /etc/${botname}/config.json
RUN sed -i s~DBUSER~${dbuser}~g /etc/${botname}/config.json
RUN sed -i s~DBPWD~${dbpwd}~g /etc/${botname}/config.json
RUN sed -i s~TIMEZONE~${config_timezone}~g /etc/${botname}/config.json

ENTRYPOINT ["/startscript"]
CMD /etc/${botname}/bot.js
